# CUNY BA Roundtable Presentation — Tinkering as Critical Knowing

## Project

A lightweight slide deck for the CUNY BA Student Roundtable on CALI and the CUNY AI Lab.
Uses a vanilla HTML/CSS/JS presentation framework adapted from the CAIL Spotlight Workshop series.

## File Structure

```
index.html          Main presentation (16 slides)
src/
  styles.css        All styles — dark theme, soft grey-blue palette
  slides.js         Navigation engine — fragments, keyboard, touch, scrubber
SLIDES.md           Slide outline and link reference
CLAUDE.md           This file
```

## Conventions

- CSS lives in `src/styles.css`, never inline in `index.html`
- JS lives in `src/slides.js`
- Slides are `<section class="slide">` with `data-slide` attributes
- Progressive reveals use `.frag` class; JS toggles `.visible`
- Section breaks use `.slide-break` class
- Stage content types: `.stageCenter`, `.stageCompare`, `.step-grid`, `.res-wrap`
- Color palette defined via CSS custom properties in `:root`
- Design tokens: `--bg`, `--fg`, `--muted`, `--accent`, `--part`

## Theme

Dark background (`#0f1319`) with soft grey-blue accent (`#8aa8c7`).
Labels and tags use `--part` (`#8b9bb5`).

## Adding Slides

1. Add a `<section class="slide">` in `index.html` inside `<main>`
2. Update the scrubber `max` attribute and counter in the footer
3. Update `SLIDES.md` with the new slide entry
