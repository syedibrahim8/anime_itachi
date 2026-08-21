# anime_itachi

A scroll-driven, cinematic tribute to **Uchiha Itachi** from *Naruto*. The page is a single static site — no build step, no framework — built from pre-rendered image sequences, Canvas 2D, and a raw WebGL ghost-cursor effect.

## Overview

The experience unfolds in four acts as you move through the page:

| Act | Section | Interaction |
|-----|---------|-------------|
| **I — 静寂 / Silence** | Scroll-scrubbed animation | Scroll to scrub through 71 frames as Itachi opens his eyes and the Sharingan activates |
| **II — 見つめ返せ** | Mouse-tracked eyes | Move your cursor — gaze is mapped across 51 eye frames with smooth crossfading |
| **III — 其の眼に宿る術** | Jutsu grid | Parallax copy, a reveal mask, and a WebGL ghost-cursor trail in Amaterasu red |
| **IV** | Quote & footer | Currently commented out in `index.html` |

Ambient layers run throughout: film grain, vignette, scanlines, animated **Amaterasu** black-flame hem, and procedurally generated **lightning** with optional thunder audio.

## Features

- **Frame preloader** — loads 122 JPEG frames (71 main + 51 eyes) with a progress bar before the experience starts
- **Scroll-scrubbed sequence** — scroll position drives frame index with lerp smoothing; phase captions fade in/out at tuned scroll windows
- **Crow feather particles** — canvas-drawn feathers drift during the final act of the scroll sequence
- **Live gaze tracking** — pointer X maps to a monotonic lookup table of nine gaze positions; frames crossfade for continuity
- **Ghost cursor (WebGL)** — port of [reactbits.dev ghost-cursor](https://reactbits.dev/animations/ghost-cursor) to raw WebGL (fbm smoke shader, trail ring-buffer, no Three.js)
- **Amaterasu hem** — procedural black-flame tongues along the bottom edge, drawn as crimson halo + black core
- **Storm system** — SVG lightning bolts, screen flash, and synthesized thunder via Web Audio API
- **Custom cursor** — smooth-follow red ring cursor
- **Reduced motion** — respects `prefers-reduced-motion: reduce` (static Amaterasu, no storm loop)
- **Responsive layout** — cover-fit canvas drawing with capped upscale so faces stay framed on tall/narrow screens

## Tech stack

- HTML5, CSS3, vanilla JavaScript
- Canvas 2D for frame playback, feathers, and Amaterasu flames
- WebGL for the jutsu-section ghost cursor
- Web Audio API for procedural thunder
- Google Fonts: Shippori Mincho, Zen Kaku Gothic New, Cinzel, Space Grotesk

## Project structure

```
anime_itachi/
├── index.html          # Page markup and sections
├── main.js             # All animation, audio, and interaction logic
├── style.css           # Layout, typography, ambient effects
├── frames/
│   ├── main/           # 001.jpg – 071.jpg  (scroll sequence)
│   ├── eyes/           # 001.jpg – 051.jpg  (gaze sequence)
│   └── storm.jpg       # Background plate for jutsu reveal
└── README.md
```

## Getting started

You need a local HTTP server so frame images load correctly. Opening `index.html` directly (`file://`) often breaks image loading.

**1. Open a terminal and go to the project folder:**

```bash
cd ~/anime_itachi
```

**2. Start a server (Python 3):**

```bash
python3 -m http.server 8080
```

**3. Open in your browser:**

```
http://localhost:8080
```

**Stop the server:** press `Ctrl+C` in the terminal.

### Other server options

```bash
# Node (npx)
npx serve .

# PHP
php -S localhost:8080
```

## Controls

| Action | Effect |
|--------|--------|
| **Scroll** | Scrub the main animation; progress shown in the right rail |
| **Move cursor** (Eyes section) | Itachi's gaze follows your pointer left ↔ right |
| **Move cursor** (Jutsu section) | Ghost-cursor trail and circular reveal mask |
| **音 / Sound button** (header) | Toggle thunder audio (requires a click to unlock browser audio) |
| **EYES / JUTSU / END** (nav) | Jump to section anchors |

## Frame breakdown (Act I)

The main sequence is choreographed to scroll progress:

- **Frames 1–13** — eyes closed, silence
- **Frames 14–24** — awakening
- **Frames 25–52** — Sharingan active
- **Frames 53–71** — crow / genjutsu phase

Phase captions and the title lockup are timed to these ranges in `main.js` (`PHASE_WINDOWS`).

## Browser support

Works best in modern browsers with Canvas 2D and WebGL support (Chrome, Firefox, Safari, Edge). Thunder audio requires a user gesture before playback (handled by the sound toggle).

## License & attribution

Fan project — *Naruto* and Uchiha Itachi are property of their respective rights holders.

Ghost-cursor shader adapted from [reactbits.dev](https://reactbits.dev/animations/ghost-cursor).
