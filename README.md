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

### Trace/Upscale pipeline wiring

By default, the widget now points to Supabase Edge Functions in the same project:

- `https://wbtpizrlayiedgwrtpwl.functions.supabase.co/trace-svg`
- `https://wbtpizrlayiedgwrtpwl.functions.supabase.co/upscale-image`

You can override either endpoint before the app JS runs:

- `window.TCM_TRACE_URL`
- `window.TCM_UPSCALE_URL`

Expected contracts:

- Trace endpoint: accepts `{ imageBase64, mimeType, style, traceDetail, output }`, returns `{ svg }`
- Upscale endpoint: accepts `{ imageBase64, mimeType, scale }`, returns `{ bytesBase64Encoded, mimeType }`

The status line now includes a pipeline mode tag:

- `trace:server | upscale:server` when server endpoints are active
- `trace:fallback` and/or `upscale:fallback` when browser fallback path is used

If server functions return `501` (not configured), the app automatically falls back in-browser for continuity.
