# Project Planning Document

## Project Vision
Develop a mobile app that generates parametric 3D nude models from single photos using efficient on-device AI. Goal: MVP in 3-6 months, focusing on privacy (no persistent image storage) and usability. Target: iOS 14+/Android 10+ devices with ML hardware. Leveraging React Native 0.82 for native performance and Expo for streamlined development/deployments.

## Phases and Timeline

### Phase 1: Research & Setup (Weeks 1-4)
- **Objectives:**
  - Validate model feasibility: Test Ultraman/DeepHuman on sample images for single-view reconstruction accuracy (>80% pose match) using TensorFlow.js.
  - Select tech stack: Expo (SDK 51+) with React Native 0.82 and Hermes enabled. Integrate tfjs-react-native for ML.
  - Ethical proxy datasets: Use synthetic SMPL-X scans (e.g., from AMASS dataset) for nudity texturing training.
- **Milestones:**
  - Wireframes in Figma.
  - Proof-of-concept: Script to process one image end-to-end on laptop (using PyTorch → export to tfjs/ONNX), then test in Expo snack.
- **Resources:** 1 ML Engineer, 1 UI Dev. Budget: $0 (open-source models). Expo account for builds.

### Phase 2: Prototyping (Weeks 5-10)
- **Objectives:**
  - Implement core pipeline:
    - Camera integration with pose estimation (MediaPipe via @mediapipe/tasks-vision).
    - 3D fitting: Load quantized model via tfjs; input keypoints + image features → output SMPL params.
    - Basic texturing: ControlNet diffusion for skin (prompt: "realistic nude body texture") using tfjs backend.
  - Basic UI: Capture → Load → 3D View with React Native components.
- **Milestones:**
  - Runnable prototype via `expo start` (latency <5s).
  - Unit tests for each module (e.g., pose accuracy >0.7) using Jest.
- **Risks & Mitigations:**
  - Model size (>200MB): Quantize to 8-bit, use Expo's asset bundling.
  - Pose errors: Add UX prompt for full-body, front-facing shots.

### Phase 3: Development & Enhancement (Weeks 11-18)
- **Objectives:**
  - Remote fallback: API for multi-view synthesis (PSHuman on GPU).
  - Polish: AR overlay (expo-three with ARKit/ARCore), export formats, settings (quality toggles).
  - Optimization: Hermes for faster JS execution, NPU offload via tfjs delegates.
- **Milestones:**
  - Beta build: Test on 5 physical devices via Expo Go/EAS.
  - Integration tests: End-to-end success rate >90%.
- **Resources:** Add QA tester. Tools: Expo Analytics for crashes, Sentry for monitoring.

### Phase 4: Testing & Launch (Weeks 19-22)
- **Objectives:**
  - Comprehensive testing: Edge cases (diverse body types, lighting), security audit (no data leaks).
  - Deployment: Use EAS Build for App Store/Play Store submission (note: May require content review).
- **Milestones:**
  - Public beta release via Expo publish.
  - Post-launch: Monitor usage, iterate on feedback with OTA updates.
- **Risks & Mitigations:**
  - App rejection: Frame as "3D avatar generator" with optional nudity; include age gates.

## Technical Specs
- **Models:**
  | Model | Purpose | Size (Quantized) | Source/Integration |
  |-------|---------|------------------|--------------------|
  | MediaPipe BlazePose | Pose Detection | 10MB | @mediapipe/tasks-vision (tfjs) |
  | DeepHuman/Ultraman | 3D Reconstruction | 50MB | tfjs or ONNX Runtime RN |
  | Mobile Stable Diffusion | Nudity Texturing | 80MB | tfjs (LoRA fine-tune) |
- **Performance Targets:**
  - On-device: 3-5s total, <100MB RAM (Hermes optimizations).
  - Remote: <10s round-trip, encrypted uploads.
- **Data Handling:** Auto-delete photos post-process; anonymize keypoints (no faces). Use Expo's SecureStore for any local keys.

## Budget & Team
- **Team:** 2-3 devs (React Native/ML focus).
- **Costs:** $500/month cloud (AWS for remote); Expo EAS (~$29/month for builds).
- **Metrics for Success:** 1k downloads in month 1, <5% crash rate.

## Appendix: Model Training Notes
- Fine-tune diffusion on synthetic data only (e.g., render clothed/nude pairs from SMPL).
- Evaluation: FID score <20 for texture realism.
- RN 0.82 Notes: Leverage New Architecture (Fabric/TurboModules) for better ML perf.

Updates tracked in GitHub Issues.