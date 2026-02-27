# Ted Creative Metals — Etched Mockup Widget (MVP)

First widget MVP for tedcreativemetals.com.

## What it does

- Upload an SVG (or choose built-in vector samples)
- **AI pattern pipeline (Foundry flow):** Prompt → Image → Upscale 2× → Trace to SVG
- Generates a photoreal etched metal mockup (brass/stainless) via image model
- Keeps geometry faithful to the uploaded vector mask
- Download result PNG(s)

## Stack

- Static HTML/JS frontend (GitHub Pages friendly)
- Backend model call via Supabase Edge Function proxy:
  - `https://wbtpizrlayiedgwrtpwl.functions.supabase.co/gemini-proxy`

## Run locally

Open `index.html` in a browser or serve with any static server.

### Optional pipeline endpoints (for full Foundry flow)

This app is static. For true server-grade upscale/trace, set globals before app JS runs:

- `window.TCM_UPSCALE_URL` — POST endpoint returning `{ bytesBase64Encoded, mimeType }`
- `window.TCM_TRACE_URL` — POST endpoint returning `{ svg }`

If `TCM_UPSCALE_URL` is not set, upscale falls back to local canvas 2×.
If `TCM_TRACE_URL` is not set, trace step is disabled with a helpful error.
