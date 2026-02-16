# Ted Creative Metals — Etched Mockup Widget (MVP)

First widget MVP for tedcreativemetals.com.

## What it does

- Upload an SVG (or choose built-in vector samples)
- Generates a photoreal etched metal mockup (brass/stainless) via image model
- Keeps geometry faithful to the uploaded vector mask
- Download result PNG

## Stack

- Static HTML/JS frontend (GitHub Pages friendly)
- Backend model call via Supabase Edge Function proxy:
  - `https://wbtpizrlayiedgwrtpwl.functions.supabase.co/gemini-proxy`

## Run locally

Open `index.html` in a browser or serve with any static server.
