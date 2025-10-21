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