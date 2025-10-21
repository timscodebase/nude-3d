# Gemini Code Assistant Guidelines

This document provides guidelines for using the Gemini code assistant in this project. Adhering to these guidelines will ensure that the AI-generated code is consistent with the project's style and conventions.

## Project Overview

This is a cross-platform mobile app built with React Native and Expo. It allows users to generate a 3D nude model from a single photo. The app uses on-device AI for privacy and speed, with an optional remote fallback for enhanced accuracy.

## Tech Stack

- **Frontend:** React Native with Expo
- **JavaScript Engine:** Hermes
- **AI/ML:** TensorFlow.js
- **3D Rendering:** Three.js (via `expo-three`)
- **Package Manager:** `pnpm`

## Development Environment

- **Node.js:** v18+
- **Expo CLI:** `pnpm install -g @expo/cli`
- **Dependencies:** `pnpm install`
- **Run:** `pnpm start`

## Coding Style and Conventions

- **Language:** TypeScript
- **Linter:** ESLint (`pnpm run lint`)
- **Component-Based Architecture:** Follow the existing component-based architecture. Create new components in the `components/` directory.
- **Styling:** Use the `constants/theme.ts` file for consistent styling.
- **State Management:** Use React hooks for state management. For more complex state, consider using a state management library like Zustand or Redux.
- **Navigation:** Use Expo Router for navigation.
- **File Naming:** Use kebab-case for file names (e.g., `my-component.tsx`).

## Commits and Pull Requests

- **Commit Messages:** Follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.
- **Pull Requests:** Provide a clear description of the changes and link to any relevant issues.

## Contact

If you have any questions, please contact the project maintainer:

- **Tim Smith:** [tim.smith.hdg@gmail.com](mailto:tim.smith.hdg@gmail.com)