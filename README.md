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

**A different colour every load.** The page hydrates with one of eight seeds rather
than always opening on Rosso Corsa — five are the only chromatic tokens in the
Ferrari library (`../DESIGN.md` is otherwise greys), three are pigments in the same
register. It never repeats the colour you saw last time.

| | |
|---|---|
| `#da291c` Rosso Corsa | `colors.primary` |
| `#f13a2c` bright red-orange | `colors.semantic-warning` |
| `#fff200` Hypersail yellow | `colors.accent-yellow-hypersail` |
| `#4c98b9` dusty blue | `colors.semantic-info` |
| `#03904a` racing green | `colors.semantic-success` |
| `#002fa7` Klein Blue | added |
| `#004225` British Racing Green | added |
| `#ff4f00` International Orange | added |

**Two export styles**

- **Chip** (the default) — a Pantone/Polaroid-style card: white frame, square colour
  block, hex and RGB set beneath it. Exports at your chosen width × 1.3.
- **Flat** — the colour, edge to edge, square. The one you want most days.

**Three formats** — PNG, JPG (quality 0.95), SVG at 512 / 1024 / 2048 px wide. The
preview is a true scale model of the file: both are drawn from the same 1200-wide
geometry, the preview via container query units and the export via a canvas scale.

**Input** — type any of `da291c`, `#DA291C`, `abc`, `#abcd`, `#rrggbbaa`; the field
normalises as you type and turns Rosso Corsa when it can't parse. There's also the
native colour picker and a dice button for a genuinely random colour.

**Values dropdown** — HEX, RGB, HSL and the nearest named colour, each a click to
copy. It's a dropdown that overlays rather than pushes, which is what keeps the page
scroll-free; the trigger shows the colour's name at a glance. Nearest-name is a
weighted RGB distance against ~110 names — a label, not a colour science claim.

**Niceties** — `Enter` downloads. `localhost:4171/#0f4c81` opens straight onto that
colour, so links still work; without a hash every refresh rotates the seed. The last
seven colours you exported sit at the bottom in `localStorage`.

## Layout

Nothing scrolls. The whole composition is sized off one custom property —
`--stage: clamp(240px, 62dvh, 620px)` — with the swatch on the left and a compact
control panel on the right, collapsing to one column under 760px. A window shorter
than 420px gets a scrollbar rather than a crop.

## Design

Follows the shared Ferrari design system in [`../DESIGN.md`](../DESIGN.md), symlinked
here as `DESIGN.md`: `#181818` canvas, Rosso Corsa reserved for the single download
CTA, sharp 0px corners, uppercase button type at 1.4px tracking, the 8px spacing
ladder, and Inter standing in for FerrariSans.

## Files

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
