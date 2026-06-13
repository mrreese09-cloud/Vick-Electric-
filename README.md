# ⚡ Vick Electric — Tech Futurist Dashboard (GitHub Deploy)

This package is **ready for GitHub Pages** deployment.

## 🌐 Publish Steps

1. Go to https://github.com and create a new repository named `vick-electric`.
2. Upload all files (index.html, .nojekyll, README.md) into the repo root.
3. In GitHub:
   - Go to **Settings → Pages**.
   - Under “Build and deployment,” choose:
     - Source: Deploy from branch
     - Branch: main → /(root)
4. Press **Save**.

Your site will go live at:
```
https://<yourusername>.github.io/vick-electric/
```

## ✅ Once Live
- Open in Chrome.
- Allow Microphone + Sound.
- Tap **Start Vick**.
- You’ll hear “Hi Ray — my listening engine is fully online and awaiting your command.”

## 🔧 Embedded Settings
- Webhook: https://vickcore.app.n8n.cloud/webhook/ee5cd857-5e62-4a04-ad1e-d7396eeedd05
- Prompt: Tech Futurist — respond intelligently and conversationally to Ray.
- Wake phrase: “hey vick”
- Theme: Electric (blue/green energy lines)
- Autostart: enabled on desktop; tap-to-start on mobile.

## 🎙️ Give Vick a Real (Jarvis) Voice — ElevenLabs
By default Vick talks through the browser's built-in voice (robotic). To use a real ElevenLabs voice:

1. **Create / pick the voice** at https://elevenlabs.io
   - Easiest: open **Voices → Library**, pick a deep/calm male voice, and **Add to My Voices**.
   - Custom "Jarvis": use **Voice Design** — describe it (e.g. *"calm, intelligent, slightly formal British male AI assistant, warm but precise"*) and save it.
2. **Get the Voice ID** — open the voice → its ID looks like `21m00Tcm4TlvDq8ikWAM`.
3. **Get your API key** — ElevenLabs → Profile → **API Key** (`xi-...`).
4. In the dashboard, paste the **API Key** and **Voice ID** into their fields, press **💾 Save Settings**, then **“Say Hi Ray”** to test. The Voice chip turns green when configured.

**Security:** the key is stored only in your browser's `localStorage` and is **never** written into `index.html` or committed to this repo. If Vick can't reach ElevenLabs (bad key, quota, offline), it automatically falls back to the browser voice so it never goes silent.

> Note: ElevenLabs free tier has a monthly character limit; long replies use more credits. The build uses the low-latency `eleven_turbo_v2_5` model for snappy, conversational responses.
