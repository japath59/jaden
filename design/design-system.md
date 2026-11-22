# vol. 01 — design system

The site's concept: a personal portfolio presented as **Volume 01**, a record and a manga volume. The hero is the cover, the about section is the liner notes, the discography is the tour poster, and the footer is the back sleeve.
All tokens live at the top of `style.css`.

## Palette (blue family only, no warm accents)

| token | hex | use |
|---|---|---|
| `--prussian` | `#1E3A6E` | cyanotype sections (about), scrims, hero base |
| `--cobalt` | `#2F5FB3` | display titles and markers on paper, hero field |
| `--cornflower` | `#6E9BEA` | display titles on dark, selection, focus ring |
| `--haze` | `#A9C3DA` | secondary text on dark, soft blur fields |
| `--slate` | `#8A97B5` | decorative only |
| `--paper` | `#ECEBE6` | light sections |
| `--ink` | `#0B0D18` | text on paper, footer base |
| `--indigo` / `--steel` / `--mist` | `#2D336B` / `#6096B4` / `#93BFCF` | legacy gradient accents (footer glow, blur blocks) |
| `--muted-foreground` | `#3E4A66` | metadata on paper |

### Approved text pairs (WCAG)
| text on background | ratio |
|---|---|
| ink on paper | 16.2 |
| paper on prussian | 9.3 |
| muted on paper | 7.4 |
| haze on prussian | 6.1 |
| white on cobalt | 6.2 |
| cobalt on paper | 5.2 |
| white on hero top (`#3F6FB8`) | 5.0 |
| cornflower on prussian | 4.0 (display sizes only, 40px or larger) |

Never use slate or cornflower for body text on paper.

## Type

| role | family | settings |
|---|---|---|
| Display, wide (section titles) | **Archivo** | wght 800, `font-stretch: 125%`, uppercase, line-height .86, tracking −.02em |
| Hero name / sign-off | **Inter** | wght 200, lowercase |
| Body | **Inter** | wght 300, lowercase, line-height 1.7 to 1.95, measure 58ch |
| Labels, metadata, nav | **JetBrains Mono** | wght 400, 11 to 13px, tracking .04 to .08em, `[ bracket ]` style |
| Vertical kanji (剣道) | **Noto Serif JP** | wght 700, subset to the two glyphs |

All fonts are free on Google Fonts. The voice is lowercase everywhere except the wide display titles.

### Scale
`--step--2` 11px · `--step--1` 13px · `--step-0` 15 to 17px · `--step-1` 18 to 24px · `--step-3` 38 to 68px (thin name) · `--step-4` 44 to 120px (wide titles)

## Layout
- Gutter `clamp(16px, 3.4vw, 56px)`. Section padding `clamp(88px, 12vw, 180px)`.
- Every section opens with a **label row**: a mono `[ name // ]` on the left, context on the right, and a 1px hairline under it.
- **Tour list** (discography): columns `date | type | title | tools`. Dates use the format `YYYY.MM`. Each row has a hairline under it, and the list opens with a 1px ink rule.
- **Markers**: `[ ◊ ]` competition / industry, `[ ♦ ]` build / study, `[ ▢ ]` research. Small outlined squares (`.sq`) mark mono list items.
- **Editorial details**: at most one rotated-180° "mirror" line (discography only, decorative, `aria-hidden`), and one vertical text element (剣道 in the gallery).
- **Restraint**: the hero has one focal point (you and the lily behind you). There's no giant numeral and no repeated labels. Don't number things that aren't a sequence.

## Images
- **Hero figure**: `photos/ibm-cutout.webp` (cut out of `ibm.jpg`) with the SVG filter `#duo-hero`. The filter maps luminance through ink → prussian → cobalt → haze → paper. Keep it sharp, never hazed.
- **Gallery**: grayscale plus a prussian gradient blended in `screen` mode gives a cyanotype look. On hover the photo returns to full color.
- **Spider lilies**: white line art (`lily-outline.png`, `lily-dots.png`). Place them only on dark blue grounds: the outline lily behind the hero figure at 55% opacity, the dot-matrix lily beside the liner notes at 90% opacity.

## Texture
- **Film grain**: fixed `body::after` fractal noise at 6% opacity, drifting in 9 steps.
- **Paper**: fine fiber noise (`--paper-tex`) on light sections only.
- **Blur blocks** (instead of gradients): 2 to 3 rounded rects blurred by 48 to 60px, in cobalt, haze or steel, at 15 to 60% opacity.
- **Sparkles**: footer only. Each one is a 2px star with crossed flare lines, twinkling over 6s.
- **Scrims**: put a prussian gradient (82 to 94%) under any small text that sits over an image. Never lower the text's contrast instead.

## Motion
Grain drift, line-through on hover, a 0.6s fade from cyanotype to color on gallery photos, and a 0.7s rise when the gallery opens.
`prefers-reduced-motion: reduce` turns off all of it, including smooth scrolling.
