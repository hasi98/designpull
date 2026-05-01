# designpull

> Generate Google Stitch compatible `DESIGN.md` files from any website - bring your own Gemini, OpenAI, Claude, or Ollama key.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Chrome-yellow.svg)
![Status](https://img.shields.io/badge/status-active-brightgreen.svg)

---

## What is this?

**designpull** is an open source Chrome extension that visits any website, extracts its full design system, and generates a `DESIGN.md` file using AI vision — not just CSS token dumps.

Most existing tools do rule-based CSS extraction. designpull sends a full-page screenshot + extracted tokens to your AI of choice, so the output includes real design intent: layout patterns, photography style, brand voice, platform detection, and Do's & Don'ts specific to that site.

The output format follows the **Google Stitch DESIGN.md open specification** (Apache 2.0), making it compatible with Claude Code, Cursor, GitHub Copilot, Windsurf, Google Stitch, and any other AI coding agent that reads markdown.

---

## Features

- **Full page scroll capture** — scrolls the entire page, stitches screenshots, sends it all to the AI
- **AI vision + CSS tokens** — combines computed styles with visual analysis for accurate results
- **Multi-provider support** — Gemini, OpenAI, Claude, or Ollama (local, free)
- **Bring your own API key** — keys stay in your browser, never leave your machine
- **Model picker** — lists available models from your provider after entering your key
- **Platform detection** — detects Squarespace, Webflow, Shopify etc and flags internal CSS variables
- **Google Stitch spec compatible** — output follows the official open DESIGN.md specification
- **Copy & download** — one click to copy or save the generated file
- **Zero backend** — no server, no cost to run, no account needed

---

## What it generates

A `DESIGN.md` with these sections:

1. **Overview** — aesthetic, platform, visual style, target audience
2. **Colors** — semantic roles based on actual visual usage, not token frequency
3. **Typography** — font families, size scale, weights, casing
4. **Spacing & Layout** — dominant layout pattern, grid, spacing scale
5. **Photography & Visual Style** — imagery usage, photographic style, emotional role
6. **Elevation & Shadows** — only what's visually present
7. **Border & Shape** — radius values, dominant shape language
8. **Components** — only components visible in the page
9. **Content Structure Pattern** — prose-driven vs card-driven, section flow
10. **Brand Voice** — specific to the site, with evidence from real copy
11. **Brand Assets & Key Concepts** — coined phrases, named products, content philosophy
12. **Do's and Don'ts** — specific to this brand, not generic advice

---

## Supported AI Providers

| Provider | Free Tier | Model Examples |
|---|---|---|
| Gemini | ✅ Yes (15 req/min) | gemini-2.0-flash, gemini-1.5-pro |
| OpenAI | ❌ Paid | gpt-4o, gpt-4-turbo |
| Claude | ❌ Paid | claude-sonnet-4-6, claude-haiku-4-5 |
| Ollama | ✅ Free (local) | llama3, mistral, any pulled model |

> **Recommended for free usage:** Gemini 2.5 Flash — fast, supports vision, generous free tier.

---

## Installation

This is an open source project. Load it as an unpacked extension:

```bash
git clone https://github.com/yourusername/designpull
cd designpull
```

Then in Chrome:

1. Go to `chrome://extensions`
2. Enable **Developer mode** (top right toggle)
3. Click **Load unpacked**
4. Select the `designpull` folder

---

## Usage

1. Visit any website
2. Click the **designpull** icon in your toolbar
3. On first use, go to ⚙️ Settings:
   - Select your AI provider
   - Enter your API key
   - Click **Load Models** to populate the model dropdown
   - Select your preferred model
   - Save
4. Click **Extract & Generate**
5. Wait 10–30 seconds while it scrolls, captures, and generates
6. Copy or download your `DESIGN.md`

---

## Getting API Keys

**Gemini (free tier available)**
→ https://aistudio.google.com/app/apikey

**OpenAI**
→ https://platform.openai.com/api-keys

**Claude (Anthropic)**
→ https://console.anthropic.com/settings/keys

**Ollama (free, runs locally)**
→ https://ollama.com/download
After installing, run: `ollama pull llama3`
The extension will connect to `http://localhost:11434` automatically.

---

## File Structure

```
designpull/
├── manifest.json           # Chrome MV3 config
├── popup.html              # Extension popup UI
├── popup.css               # Popup styles
├── popup.js                # Popup logic
├── content.js              # Injected into page — extracts CSS tokens
├── background.js           # Service worker — scroll capture + API calls
└── lib/
    ├── adapter.js          # Multi-provider AI adapter layer
    └── extractor.js        # DOM/CSS extraction logic
```

---

## How it works

```
1. User clicks Extract & Generate
2. content.js injected into active tab
3. Extracts computed styles from 50-100 DOM elements
   (colors, fonts, spacing, shadows, border radius, transitions)
4. background.js scrolls the full page and stitches screenshots
5. Full-page image resized to max 2000px longest dimension
6. Tokens + screenshot sent to selected AI provider
7. AI generates DESIGN.md using the refined prompt
8. Output streams back into the popup
9. User copies or downloads the file
```

---

## Why AI instead of just CSS parsing?

Pure CSS extraction misses:
- Full-bleed image layout patterns
- Brand accent color (frequency ≠ visual importance)
- Navigation casing and style
- Photography style and emotional role
- Platform internals (Squarespace, Webflow variables)
- Brand voice, coined concepts, content philosophy
- Do's and Don'ts specific to this brand

designpull combines both — exact token values from CSS, real design intent from AI vision.

---

## DESIGN.md Specification

This project outputs files compatible with the **Google Stitch DESIGN.md open specification**, released under Apache 2.0 in April 2026.

Learn more: https://stitch.withgoogle.com/docs/design-md/overview

---

## Contributing

Contributions welcome. Please open an issue first to discuss before submitting a PR.

Things that would be great contributions:
- Support for additional AI providers
- Firefox extension port
- Improved scroll capture for infinite scroll pages
- Better token extraction for CSS-in-JS sites (styled-components, emotion)
- Output format options (JSON tokens, Tailwind config, CSS variables)

---

## License

MIT — see [LICENSE](./LICENSE)

---

## Acknowledgements

- Google Stitch for open-sourcing the DESIGN.md specification
- The open source tools that came before: Dembrandt, design-extract, design-md-chrome
