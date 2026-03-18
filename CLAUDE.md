# CLAUDE.md

Guidance for Claude Code when working in this repository.
For human-readable project documentation see [README.md](README.md).

## Project

A vanilla HTML/CSS/JS slide deck for the CUNY BA Student Roundtable on CALI and the CUNY AI Lab.
No build step, no dependencies — open `index.html` directly or serve with any static server.

## File Structure

```
index.html          Main presentation (11 slides)
src/
  styles.css        All styles — dark theme, soft grey-blue palette
  slides.js         Navigation engine — fragments, keyboard, touch, scrubber
SLIDES.md           Slide map and link reference (update when slides change)
README.md           Human-facing documentation
CLAUDE.md           This file
```

The speaker script (`CUNY_BA_Presentation_Script.md`) is gitignored as source material.

## Architecture

Each slide is a `<section class="slide">` with a **two-panel layout** at ≥720px:
- `.content` — left panel: label, h1, h2 (the "what")
- `.stage` — right panel: visual payload (the "how")

Stage content types: `.stageCenter`, `.stageCompare`, `.step-grid`, `.res-wrap`

**Fragment reveals**: Elements with `.frag` start hidden. `advance()` in `slides.js` toggles `.visible` one at a time. `retreat()` reverses. The `show()` function can optionally reveal all fragments at once (`revealAll` param) when jumping via scrubber or hash.

**Input layers** (all in `slides.js`):
- Keyboard: arrows, space, pageup/down, home/end, escape (overview)
- Touch: swipe (≥48px horizontal) and tap (<16px movement) advance; `.stage` and `.sticky-footer` are excluded zones
- Trackpad: horizontal wheel events with 400ms debounce
- Footer: prev/next buttons + range scrubber

## Conventions

- CSS lives in `src/styles.css`, never inline
- JS lives in `src/slides.js`
- Slides use `data-slide` attributes for semantic identification
- Color palette via CSS custom properties: `--bg`, `--fg`, `--muted`, `--accent`, `--part`
- Dark background (`#0f1319`) with soft grey-blue accent (`#8aa8c7`)
- Forward slashes in slide text are separators — always include a space after (`/`)

## Adding or Removing Slides

1. Add/remove `<section class="slide">` in `index.html` inside `<main>`
2. Update the scrubber `max` attribute in the footer `<input type="range">`
3. Update the hardcoded counter text in `<span id="slider-counter">`
4. Update `SLIDES.md` slide map and structure sections
