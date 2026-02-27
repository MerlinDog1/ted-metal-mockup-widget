# Ted Creative Metals — Etched Mockup Widget (MVP)

First widget MVP for tedcreativemetals.com.

## What it does

- Step 1 source options:
  - Upload SVG or image
  - Pick Ted pattern library asset
  - Prompt a new design (Foundry flow)
- Foundry flow: Prompt → Image → Upscale 2× → Trace to SVG → Use as source
- Step 2 material/finish + optional direction
- Step 3 scene selection (square/main, lobby wall, lift, panel-bank variant)
- Step 4 generate mockups + download outputs

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
If `TCM_TRACE_URL` is not set, trace falls back to an in-browser binary SVG approximation.
