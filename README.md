# Tinkering as Critical Knowing

Slide deck for the **CUNY BA Student Roundtable**, March 11, 2026.
Presented by **Zach Muhlbauer** — PhD Candidate in English, Technical Lead (CALI), Co-Founder (CUNY AI Lab).

The talk introduces [CALI (Critical AI Literacy Institute)](https://cuny.is/cali) and the [CUNY AI Lab](https://ailab.gc.cuny.edu) — two initiatives at the CUNY Graduate Center advancing critical AI literacy in public higher education. The central argument: engaging AI through building (*t(h)inkering*) is itself a form of critical knowing.

---

## Running the Deck

No build step, no dependencies. Open `index.html` directly in a browser, or serve from any static server:

```sh
npx serve .
# or
python3 -m http.server
```

---

## Presentation Structure

Eleven slides organized into four movements:

| Slides | Focus |
|--------|-------|
| 1–3 | CALI — background, Google.org funding, Year One work |
| 4–5 | T(h)inkering framework and the transition from CALI to the Lab |
| 6–9 | CUNY AI Lab — mission, Sandbox platform, AmigAI, Tools |
| 10–11 | Discussion questions and resource links |

See [SLIDES.md](SLIDES.md) for the full slide map with `data-slide` identifiers and all linked URLs.

---

## Design System

### Layout

Each slide is a `<section class="slide">` with a **two-panel layout** on screens ≥ 720px:

- **`.content`** — left panel: `.label` (uppercase category), `h1` (title), `h2` (subtitle or link)
- **`.stage`** — right panel: visual payload

On mobile the panels stack vertically (content above, stage below).

### Stage Content Types

| Class | Use |
|-------|-----|
| `.step-grid` | Numbered `.step-row` items, fragment-revealed one at a time |
| `.stageCompare` | Two-column side-by-side layout with `.col-tag`, `.col-title`, `.col-sub` |
| `.stageCenter` + `.stageInner` | Centered text or content block |
| `.res-wrap` / `.res-group` / `.res-list` | Grouped resource links (used on the last slide) |
| `.stage-fill` | Full-bleed iframe, canvas, or video |

### Color Palette

All colors are CSS custom properties in `src/styles.css`:

| Variable | Value | Role |
|----------|-------|------|
| `--bg` | `#0f1319` | Page background |
| `--fg` | `rgba(218,225,232,0.92)` | Primary text |
| `--muted` | `rgba(190,200,215,0.55)` | Subtitles, secondary text |
| `--accent` | `#8aa8c7` | Links, active elements |
| `--part` | `#8b9bb5` | Labels, step numbers, section markers |
| `--card` | `rgba(180,200,220,0.055)` | Panel backgrounds |
| `--stroke` | `rgba(180,200,220,0.13)` | Borders |

### Fragment Reveals

Elements with `.frag` start hidden (`opacity: 0`). Each advance reveals the next hidden fragment. Retreating un-reveals the last. Jumping via the scrubber reveals all fragments on the target slide at once.

---

## Navigation

| Input | Action |
|-------|--------|
| `→` / `Space` / `PageDown` | Advance (fragment then slide) |
| `←` / `PageUp` | Retreat |
| `Home` / `End` | First / last slide |
| `Escape` | Toggle overview grid |
| Swipe left / right | Advance / retreat |
| Tap (mobile) | Advance |
| Two-finger trackpad swipe | Advance / retreat |
| Footer scrubber | Jump to any slide |

---

## File Structure

```
index.html          Main presentation (11 slides)
src/
  styles.css        All styles — dark theme, soft grey-blue palette
  slides.js         Navigation engine — fragments, keyboard, touch, scrubber
SLIDES.md           Slide map, structure summary, and all key links
README.md           This file
```

---

## Replicating This Deck

To build a new presentation from this design, follow these steps in order.

### 1. Copy the shell

Start with these four files:

```
index.html
src/styles.css
src/slides.js
SLIDES.md
```

`slides.js` and `styles.css` are self-contained and require no changes to work. All presentation-specific content lives in `index.html`.

### 2. Edit the `<head>` in `index.html`

Update the page title:

```html
<title>Your Talk Title — Event Name</title>
```

### 3. Replace the title slide

The first `<section class="slide" data-slide="title">` contains the talk title, subtitle, date, and speaker credit. Update those fields. The `.stage` on the title slide is full-bleed — swap the `<iframe>` for any visual you want, or remove the stage entirely and let the content panel fill the screen.

### 4. Build your slides

Each content slide follows this structure:

```html
<section class="slide" data-slide="your-id" aria-label="Screen reader label">
  <div class="content">
    <div class="label">Section label</div>
    <h1>Slide title</h1>
    <h2>Subtitle or supporting link</h2>
  </div>
  <div class="stage" aria-hidden="true">
    <!-- stage content here -->
  </div>
</section>
```

Pick a stage layout from the options below and drop it inside `.stage`.

**Step list** — numbered rows revealed one at a time:

```html
<div class="step-grid">
  <div class="step-row frag"><div class="step-num">1</div><div class="step-text">First point</div></div>
  <div class="step-row frag"><div class="step-num">2</div><div class="step-text">Second point</div></div>
</div>
```

**Side-by-side comparison:**

```html
<div class="stageCompare">
  <div class="col">
    <span class="col-tag">Left label</span>
    <div class="col-title">Left heading</div>
    <div class="col-sub">Left body text</div>
  </div>
  <div class="col">
    <span class="col-tag">Right label</span>
    <div class="col-title">Right heading</div>
    <div class="col-sub">Right body text</div>
  </div>
</div>
```

**Resource link list** (for a references / links slide):

```html
<div class="res-wrap">
  <div class="res-group">
    <div class="res-group-title">Group heading</div>
    <ul class="res-list">
      <li>
        <a href="https://example.com" target="_blank" rel="noopener">example.com</a>
        <div class="res-desc">Short description</div>
      </li>
    </ul>
  </div>
</div>
```

**Full-bleed embed** (iframe, canvas, video):

```html
<div class="stage-fill">
  <iframe src="https://..." title="Description" tabindex="-1"></iframe>
</div>
```

Remove `.frag` from any element you want visible immediately on slide entry. Add `.frag` to any element you want revealed by pressing advance.

### 5. Update the footer counter

In the `<div class="sticky-footer">` at the bottom of `index.html`, set `max` and the counter text to match your slide count:

```html
<input type="range" id="slide-scrubber" min="1" max="12" value="1" ...>
...
<span id="slider-counter">1 / 12</span>
```

### 6. Update SLIDES.md

Replace the slide map table and structure summary with your own slides. This file is the single source of truth for slide identifiers and external links — keep it current as you build.

### 7. Customize the palette (optional)

To change the color scheme, edit the CSS custom properties at the top of `src/styles.css`. All colors in the deck derive from these seven variables — you do not need to touch anything else to re-theme:

```css
:root {
  --bg:     #0f1319;              /* page background */
  --fg:     rgba(218,225,232,0.92); /* primary text */
  --muted:  rgba(190,200,215,0.55); /* subtitles */
  --accent: #8aa8c7;              /* links, active elements */
  --part:   #8b9bb5;              /* labels, step numbers */
  --card:   rgba(180,200,220,0.055);
  --stroke: rgba(180,200,220,0.13);
}
```

### Conventions to keep

- All CSS in `src/styles.css` — never inline styles
- All JS in `src/slides.js` — no script tags in slides
- Forward slashes used as visual separators always have a space after: `word / word`
- Slides are identified by `data-slide` attribute, not by position in the DOM
