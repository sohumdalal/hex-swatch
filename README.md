# hex-swatch

**One HTML file.** No sign-up, no build step, no dependencies, no framework — a hex
code in, a flat image out. It turns `#da291c` into a PNG, JPG or SVG you can drop
straight into a deck, a Figma frame or a CSS comment.

Live at **[swatch.beer](https://swatch.beer)**.

Built because getting a plain PNG of a single colour is absurdly annoying.

## Run it

```bash
python3 -m http.server 4171   # from this directory
open http://localhost:4171
```

Opening `index.html` directly (`file://`) works too — the only thing that needs
`localhost` is the clipboard copy buttons, which browsers gate to secure contexts.

## Design

Follows the shared Ferrari design system in [`../DESIGN.md`](../DESIGN.md), symlinked
here as `DESIGN.md`: `#181818` canvas, sharp 0px corners, uppercase button type at
1.4px tracking, the 8px spacing ladder, and Inter standing in for FerrariSans.

One deliberate departure: the download button and the wordmark square take the live
swatch colour rather than Rosso Corsa, flipping their label between white and
`#181818` at the WCAG luminance crossover so they stay legible on any hue.

## Files

```
hex-swatch/
├── index.html      the whole app — markup, design tokens, logic
├── DESIGN.md       → ../DESIGN.md (shared across every agent in the tree)
├── .vercelignore   keeps that symlink out of deploys
└── README.md
```
