# ⚡ VICK — Personal Sovereign OS (voice dashboard)

A single-file, voice-driven front-end for VICK — Ray's personal governance OS.
Governed by the v11.0 Core Operating Prompt (identity, action-permission tiers,
STARGATE discipline). Runs free on GitHub Pages. Brain + voice + memory are all
configured in-browser; **no keys are ever committed** — they live only in your
browser's `localStorage`.

Live: https://mrreese09-cloud.github.io/Vick-Electric-/
Deploys automatically on every push to `main` (see `.github/workflows/deploy-pages.yml`).

---

## 🧠 Brain — free Gemini (recommended)
1. Go to https://aistudio.google.com → **Get API key** → **Create API key** (free, no credit card).
2. Paste it into the dashboard's **Gemini API Key** field → **💾 Save Settings**.
3. Tap **▶ Start listening** and just talk — no wake word.

Optional paid upgrade: a **Claude** key (`sk-ant-…`, from console.anthropic.com) in the
Claude field gives deeper reasoning. Leave the **Model** field blank to use the free default
(`gemini-2.0-flash`); the cost-tuned cap is 350 output tokens per reply.

## 🎙️ Voice — ElevenLabs (optional Jarvis voice)
1. At https://elevenlabs.io pick a voice (**Voices → Library**) or design one (**Voice Design**,
   e.g. *"calm, intelligent, slightly formal male AI assistant"*). Copy its **Voice ID**.
2. Profile → **API Key**. Paste **API Key** + **Voice ID** → Save.
3. Leave them blank to use your phone's free built-in voice. If ElevenLabs fails or runs out of
   free credits, VICK automatically falls back to the browser voice (low-latency `eleven_turbo_v2_5`).

## ☁️ Memory — External State Layer
- **On-device (automatic, free):** the conversation persists to `localStorage`, so VICK remembers
  across sessions on that device.
- **Cross-device (Supabase, free tier, no card):** make VICK share one brain across all your devices.
  1. Create a free project at https://supabase.com.
  2. In the project's **SQL Editor**, run the SQL below.
  3. Project **Settings → API**: copy the **Project URL** and the **anon public** key.
  4. Paste both into the dashboard's **Supabase Project URL** + **anon key** fields → Save → reload.
  VICK loads recent memory from the cloud on start and writes every exchange back.

```sql
create table if not exists vick_memory (
  id bigint generated always as identity primary key,
  created_at timestamptz default now(),
  role text not null,
  content text not null
);
create table if not exists vick_decisions (
  id bigint generated always as identity primary key,
  created_at timestamptz default now(),
  title text not null,
  detail text,
  status text default 'open',
  tier text
);
alter table vick_memory enable row level security;
alter table vick_decisions enable row level security;
create policy "anon all memory"   on vick_memory   for all to anon using (true) with check (true);
create policy "anon all decisions" on vick_decisions for all to anon using (true) with check (true);
```

> The anon key + URL are public-client credentials and live only in your browser's `localStorage`
> (never committed). For a personal single-user setup the policies above are fine; lock them down
> with Supabase Auth later if you ever share the project. Don't speak true secrets to VICK — per
> SECRET ZERO, passwords/keys never belong in conversation.

## Buttons
- **Start listening / Stop** — mic on/off (talk freely; no wake word by default).
- **Say "Hi Ray"** — speak the greeting (quick voice test).
- **💾 Save Settings / Load Settings** — persist config to this browser.
- **🧠 Clear Memory** — wipe the on-device conversation memory for a fresh start.

## Notes
- Voice **recognition** needs Chrome on Android/desktop over HTTPS. iOS browsers don't support the
  Web Speech recognition API (VICK can talk back there, but not listen).
- This dashboard is VICK's face, brain, and voice. Real autonomous **execution** (sending email,
  booking calendar, scheduled tasks) lives in the separate n8n + connector layer.
