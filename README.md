# 3D Nude Model Generator App

## Overview

This cross-platform (iOS/Android) mobile app allows users to capture a photo of a person and generate a 3D nude model using on-device AI for privacy and speed, with optional remote fallback for enhanced accuracy. The pipeline includes pose estimation, 3D body reconstruction, and generative texturing to simulate nudity.

**Key Features:**

- Single-photo capture with real-time pose detection.
- On-device 3D mesh fitting (using SMPL-X parametric models).
- AI-driven "undressing" via diffusion-based skin texturing.
- Interactive 3D viewer with export options (GLB/OBJ).
- Fallback to cloud processing for low-confidence inputs.

**Tech Stack:**

- Frontend: Expo with React Native 0.82 (Hermes JS engine enabled for performance).
- AI/ML: TensorFlow.js (tfjs) for on-device models (MediaPipe via @mediapipe/tasks-vision, Ultraman/DeepHuman via ONNX Runtime React Native, lightweight Stable Diffusion via tfjs for texturing).
- Backend (optional): FastAPI on AWS Lambda for remote inference.
- Rendering: React Native Three.js (via expo-three) for 3D visualization.
- Development: Expo CLI for easy builds and over-the-air updates.

**Disclaimer:** This project is for educational/experimental purposes. Users must ensure consent and comply with local laws regarding image processing and nudity simulation. Ethical use is strongly encouraged.

## Quick Start

### Prerequisites

- Node.js (v18+): [Install Guide](https://nodejs.org/)
- Expo CLI: `npm install -g @expo/cli`
- Android Studio (for Android) or Xcode (for iOS).
- Git for cloning the repo.
- Hermes: Enabled by default in RN 0.82; no extra setup needed.

### Installation

1. Clone the repository:

  ```bash
  git clone https://github.com/yourusername/3d-nude-model-app.git
  cd 3d-nude-model-app
  ```

2. Install dependencies:

  ````bash
  npm install
  ```

3. For AI models: Download pre-quantized models from Hugging Face and place in `assets/models/` (see `PLANNING.md` for details). Use `expo install` for Expo-compatible packages like `expo-camera`, `expo-gl`.
4. Start the development server:

```bash
  npx expo start
````

- Scan QR code with Expo Go app on iOS/Android for testing.
- For iOS: Ensure you have a provisioning profile for ARKit.
- For Android: Target API 30+ for NPU support.
- Build standalone: `eas build` (requires Expo account).

### Usage

1. Launch the app via Expo Go or built binary and grant camera permissions.
2. Tap the camera button to snap a photo.
3. The app processes on-device (pose → 3D → texture) in ~3-5 seconds.
4. View and interact with the 3D model; export via share button.
5. If needed, enable remote mode in settings for better results.

## Architecture

- **Frontend Pipeline**: Expo Camera → MediaPipe Pose → DeepHuman Fitting → Diffusion Texturing → Three.js Render.
- **Data Flow**: Images processed locally; only keypoints uploaded remotely if fallback triggered.

For detailed planning, see [PLANNING.md](PLANNING.md).

## Contributing

[CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) for details.

## Contact

Project maintainer: [Tim Smith](mailto:tim.smith.hdg@gmail.com)

---

\*Built with ❤️ by xAI-inspired devs. Putting aside ethics for innovation. Updated for React Native 0.82
