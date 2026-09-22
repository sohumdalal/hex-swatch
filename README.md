# Swatch

A hex code in, a flat image out. No sign-up, no build step, no dependencies — one
HTML file that turns `#da291c` into a PNG, JPG or SVG you can drop straight into a
deck, a Figma frame or a CSS comment.

Built because getting a plain PNG of a single colour is absurdly annoying.

## Run it

```bash
python3 -m http.server 4171   # from this directory
open http://localhost:4171
```

Opening `index.html` directly (`file://`) works too — the only thing that needs
`localhost` is the clipboard copy buttons, which browsers gate to secure contexts.

## What it does

**Two export styles**

- **Flat** — the colour, edge to edge, at 512 / 1024 / 2048 px square. This is the
  one you actually want most days.
- **Chip** — a Pantone/Polaroid-style card: white frame, square colour block, hex
  and RGB set beneath it. 1200 × 1560.

**Three formats** — PNG, JPG (quality 0.95), SVG. Flat SVG is three lines of markup
and scales forever; chip SVG carries the labels as real text.

**Input** — type any of `da291c`, `#DA291C`, `abc`, `#abcd`, `#rrggbbaa`; the field
normalises as you type and turns Rosso Corsa when it can't parse. There's also the
native colour picker and a dice button for a random colour.

**Readouts** — HEX, RGB, HSL, each with a copy button, plus the nearest named CSS
colour (a weighted RGB distance against ~110 names — a label, not a colour science
claim).

**Niceties** — the hex lives in the URL hash, so `localhost:4171/#0f4c81` opens on
that colour and links are shareable. `Enter` downloads. The last 12 colours you
exported sit at the bottom in `localStorage`.

## Design

Follows the shared Ferrari design system in [`../DESIGN.md`](../DESIGN.md), symlinked
here as `DESIGN.md`: `#181818` canvas, Rosso Corsa reserved for the single download
CTA, sharp 0px corners, uppercase button type at 1.4px tracking, the 8px spacing
ladder, and Inter standing in for FerrariSans.

## Layout

```
hex-swatch/
├── index.html    the whole app — markup, tokens, logic
├── DESIGN.md     → ../DESIGN.md (shared across every agent in the tree)
└── README.md
```

## Notes

- Chip PNG/JPG waits on `document.fonts.ready` so the label renders in Inter rather
  than a fallback. Chip **SVG** references Inter by name — anything opening that file
  without Inter installed falls back to the system sans.
- JPG has no alpha; both styles are fully opaque so nothing is lost.
- No analytics, no network calls beyond the Google Fonts stylesheet.
