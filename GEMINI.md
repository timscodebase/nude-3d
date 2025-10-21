# GEMINI.md: Integrating Google Gemini API

## Overview

This document outlines the integration of Google's Gemini API (Gemini 1.5 Pro or Flash) into the 3D Nude Model Generator App for enhanced remote processing. Gemini serves as a lightweight, multimodal LLM for tasks like:

- Generating precise prompts for diffusion-based texturing (e.g., "Generate a detailed skin texture description for a [body type] nude model in [lighting]").
- Image captioning to refine pose estimation (e.g., describe clothing/occlusions for better "undressing").
- Fallback reasoning: Analyze low-confidence on-device outputs and suggest user actions (e.g., "Reposition for full-body view").

**Why Gemini?**

- Multimodal: Handles images + text, ideal for photo analysis.
- Low-latency: Flash model (~200ms responses) fits remote fallback.
- Cost-effective: Free tier (15 RPM) for prototyping; scales to $0.35/1M tokens.
- JS SDK: Seamless with React Native via `@google/generative-ai`.

**Scope**: Remote-only (privacy-focused); on-device remains TF.js/MediaPipe. Estimated integration time: 1-2 weeks.

## Setup and Authentication

1. **API Key**:
   - Get from [Google AI Studio](https://aistudio.google.com/app/apikey).
   - Store securely: Use Expo's `expo-constants` + `.env` (via `dotenv`):

     ```bash
     # .env (add to .gitignore!)
     GEMINI_API_KEY=your_api_key_here
     ```

   - In code: `import Constants from 'expo-constants'; const apiKey = Constants.expoConfig.extra.geminiApiKey;`

2. **Install SDK**:

```bash
  npx expo install @google
  /generative-ai
```

- Compatible with RN 0.82/Hermes; no native modules needed.

3. **Basic Config** (in `src/services/gemini.ts`):

```typescript
import { GoogleGenerativeAI } from '@google/generative-ai';

const genAI = new GoogleGenerativeAI(process.env.GEMINI_API_KEY || '');
const model = genAI.getGenerativeModel({ model: 'gemini-1.5-flash' });

export async function generatePrompt(imageUri: string, bodyDesc: string): Promise<string> {
  const prompt = `Analyze this photo of a ${bodyDesc} person. Generate a detailed, photorealistic prompt for nude skin texturing on a 3D SMPL-X model. Focus on skin tone, lighting, and anatomy. Output only the prompt.`;
  
  const result = await model.generateContent([
    prompt,
    { inlineData: { data: imageUri, mimeType: 'image/jpeg' } }  // Base64 or URI
  ]);
  return result.response.text();
}
```
