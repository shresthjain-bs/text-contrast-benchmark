# Text Contrast Benchmark

A single self-contained page with **80 text-contrast test cases** across 9 sections —
every case a WCAG contrast solution should aim to resolve.

**Live page:** https://shresthjain-bs.github.io/text-contrast-benchmark/

## Sections

| Section | Covers |
|---|---|
| A — Contrast ladder | solid/solid from 21:1 down to 1.43:1, large-text 3:1 threshold pair, tiny/thin AA-regime text |
| B — Text color structure | per-word / per-character colors, multi-color single glyph, gradient text, low-contrast link in paragraph, shadow/stroke rescues |
| C — Background structure | gradients (linear/radial/conic/hard-stop), patterns, photo BG with/without scrim, OCR phantom-texture trap |
| D — Text & images | HTML text over images, images whose pixels contain text, both at once |
| E — Opacity | rgba colors, element opacity, nested ancestor opacity, disabled/placeholder patterns |
| F — Overlays | transparent/opaque × fully/partially covering, backdrop-filter blur, modal dim, mix-blend-mode |
| G — Real-world edge cases | tiny 10px text, single characters, clipped glyphs, pills, empty crops, white-on-white, monospace codes |
| H — Kitchen-sink combos | gradient-on-gradient, multi-color text on photo, opacity + scrim + image |
| I — Multi-line paragraphs | 3–6 line wrapped text: per-line BG variation (vertical gradients, photos, section boundaries), links buried mid-paragraph, inline highlights, band/banner overlays covering only some lines, dense 12px legal text, drop caps |

## Ground truth

Each croppable target (`.target[id]`) carries its expected outcome in `data-*` attributes:

- `data-expect` — `PASS` / `FAIL` / `REVIEW` (REVIEW = a confident verdict would be wrong by design)
- `data-ratio` — worst-pair WCAG ratio where computable
- `data-font-px` — when the case tests the 24px large-text threshold
- `data-note` — why the case exists / what it traps

The full machine-readable manifest (ids, expectations, bounding rects) is exposed at
runtime as `window.TC_MANIFEST` — run `copy(JSON.stringify(window.TC_MANIFEST))` in
DevTools to export it.

## Design notes

- **No external assets** — all "photos" are inline SVG data URIs, so the page renders
  identically in every browser and headless capture stack.
- Labels live **outside** the croppable targets, so per-element screenshots contain
  only the test content.
- Thresholds follow WCAG 2.1 AA: 4.5:1 normal text, 3:1 for ≥24px text.
