<p align="center">
  <img src="public/openscreen.png" alt="OpenScreen Smart Demo" width="72" />
</p>

<h1 align="center">OpenScreen Smart Demo</h1>

<p align="center">
  <strong>AI-powered smart demo generation built on top of OpenScreen.</strong><br/>
  Automatically converts screen recordings into polished product demos.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-green" />
  <img src="https://img.shields.io/badge/built%20on-OpenScreen-blue" />
  <img src="https://img.shields.io/badge/status-hackathon--MVP-purple" />
</p>

---

## How It Works

```
  ┌─────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌───────────────┐
  │  Click      │     │  Record screen   │     │  Smart Demo      │     │  Export       │
  │  ✦ Smart   │ ──▶ │  normally        │ ──▶ │  panel analyses  │ ──▶ │  polished     │
  │  button     │     │  (cursor tracked)│     │  + applies fx    │     │  MP4 / GIF    │
  └─────────────┘     └──────────────────┘     └──────────────────┘     └───────────────┘
```

After recording, the app analyses 10 Hz cursor telemetry to detect:

| Signal | Detection method |
|---|---|
| **Click** | Cursor moves → sudden stop → 150–800 ms dwell → resumes |
| **Typing** | Cursor velocity below threshold for > 1 second |
| **Window change** | Instantaneous position jump > 60% of screen width |
| **Navigation** | Fast sweep covering > 30% of screen distance |

From those signals it automatically generates:

- **Zoom regions** — centred on each click, 1.5× scale, 1.5 s duration
- **Click highlights** — animated pulse circle, `#4F8CFF`, 600 ms
- **Tutorial steps** — numbered list with timestamps
- **Trim suggestions** — silence periods > 3 s flagged for removal

---

## Quick Start

```bash
npm install
npm run dev          # development (Electron + Vite)
npm run build:mac    # production macOS build
```

---

## Smart Demo Usage

1. Select a screen/window source in the HUD overlay
2. Click the **✦ Smart** purple button → recording starts
3. Record your workflow naturally (open browser, click, type, navigate)
4. Click **✦ Smart** again to stop → editor opens automatically
5. In the editor right panel, open the **Smart Demo** accordion
6. Click **Generate Smart Demo** → review detected interactions and steps
7. Click **Apply Zoom & Highlights** → effects added to the timeline
8. Optionally click **Trim Silences** to cut inactive stretches
9. Play the preview, then **Export** as MP4 or GIF

---

## Demo Scenario (Hackathon)

The ideal 60-second demo recording:

```
1. Open Chrome
2. Navigate to a login page
3. Click the email field  ← zoom + highlight
4. Type an email address  ← zoom + typing step
5. Click the password field ← zoom + highlight
6. Type a password         ← zoom + typing step
7. Click Login button      ← zoom + highlight
8. Wait on dashboard       ← silence detected → trim suggestion
```

**Result:** ~4 zoom regions, ~3 click highlights, 3–4 tutorial steps, 1 trim suggestion.

---

## New Files Added

```
src/
├── smart-demo/
│   ├── interactionRecorder.ts   # Cursor telemetry → click/type/nav events
│   ├── timelineAnalyzer.ts      # Events → demo segments with zoom targets
│   ├── inactivityDetector.ts    # Silence detection for trim suggestions
│   ├── stepGenerator.ts         # Human-readable tutorial step generation
│   └── effects/
│       ├── autoZoom.ts          # ZoomRegion[] from click segments
│       └── clickHighlight.ts    # AnnotationRegion[] pulse circles
└── ui/
    └── SmartDemoPanel.tsx       # React panel in the editor sidebar
```

---

## Core Features (from OpenScreen)

- Screen / window recording at up to 4K 60 fps
- Timeline editor: zoom, trim, speed, annotation regions
- Background wallpapers, gradients, solid colours
- Annotations: text, arrows, images
- Export: MP4 and GIF at configurable quality

---

## Built With

Electron · React · TypeScript · Vite · PixiJS · Tailwind CSS

---

## Attribution

Built on top of **OpenScreen** by [@siddharthvaddem](https://github.com/siddharthvaddem)
Original: https://github.com/siddharthvaddem/openscreen · MIT License

---

## Pitch

> OpenScreen Smart Demo is an AI-assisted demo creation tool that automatically detects user interactions in screen recordings and converts them into polished product demos with smart zooms, click highlights, and generated step-by-step guidance — all with one click.
