# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Architecture

This is a cross-platform mobile app built with Expo and React Native that allows users to generate 3D nude models from photos. The app uses on-device AI for privacy and speed, with an optional fallback to a remote server for more complex processing.

Key technologies used:
- **Frontend**: Expo, React Native
- **On-device AI**: TensorFlow.js, MediaPipe, ONNX Runtime
- **3D Rendering**: Three.js (via expo-three)
- **Optional Backend**: FastAPI on AWS Lambda

The application structure is as follows:
- `app/`: Contains the main application code, using Expo Router for navigation.
- `components/`: Reusable React components.
- `constants/`: Global constants like colors and styles.
- `hooks/`: Custom React hooks.
- `assets/`: Static assets like images and fonts.
- `scripts/`: Helper scripts for development.

## Common Commands

- **Start the development server**: `npm start` or `expo start`
- **Run on Android**: `npm run android` or `expo start --android`
- **Run on iOS**: `npm run ios` or `expo start --ios`
- **Run on web**: `npm run web` or `expo start --web`
- **Run linter**: `npm run lint` or `expo lint`
- **Run tests**: `npm test`
