---
version: 1
name: jisooahn.com-design
description: >
  A portfolio for enterprise and fintech product design, built as a single
  static HTML file. The system is adapted from Vercel's DESIGN.md: a stark
  ink-and-neutral duet where typography and case-study imagery carry the
  page, depth comes from a four-step surface ladder plus hairline borders
  and stacked shadows, and metadata is set in a mono caption voice rather
  than in tinted chips. Two deliberate departures from the reference:
  dark is the default theme, and the lime brand colour is retained for the
  wordmark and focus ring only.
---

# DESIGN.md

Source reference: `awesome-design-md-main/design-md/vercel/DESIGN.md`.
Implementation: the single `<style>` block at the top of `index.html`.

## 1. Atmosphere

Quiet, dense, engineered. The page is a near-black canvas with off-white
type, hairline-bordered panels, and no decorative chrome. There is no
glassmorphism, no backdrop blur outside the floating nav, and no
atmospheric gradient. The screenshots of shipped product work are the
loudest thing on the page, and that is intentional.

Section depth comes from cycling surfaces, not from blur or shadow: the
page sits on `--canvas-soft`, panels lift to `--canvas`, and a highlighted
panel flips polarity to `--ink`.

## 2. Colour

Four-step surface ladder and four-step text ramp, defined per theme.

Surfaces keep the site's original palette (near-black `#06060A` in dark,
lavender-white `#F2F0FF` in light, translucent lifted cards). Text uses the
type system's ramp, with `--mute` raised in both themes for legibility.

| Role | Dark (default) | Light |
|---|---|---|
| `--canvas` (card / lifted) | `rgba(255,255,255,.05)` | `rgba(255,255,255,.72)` |
| `--canvas-soft` (page) | `#06060A` | `#F2F0FF` |
| `--canvas-soft-2` (inset) | `rgba(255,255,255,.09)` | `rgba(255,255,255,.5)` |
| `--ink` (headings, CTA fill) | `#F5F4F0` | `#0A0A0A` |
| `--body` (paragraphs) | `#C9C9C3` | `#4A4A45` |
| `--mute` (captions, eyebrows) | `#9A9A95` | `#656560` |
| `--hairline` | `rgba(255,255,255,.08)` | `rgba(0,0,0,.08)` |
| `--hairline-strong` | `rgba(255,255,255,.18)` | `rgba(0,0,0,.18)` |
| `--link` / `--brand` | `#C8FF00` | `#4F7000` |
| `--danger` | `#FF7A56` | `#CC3000` |

Every pair above clears WCAG AA (4.5:1) on both the page and a lifted card.
Re-check with the ratio script if you change any of them.

**Ink is the CTA colour.** `--brand` is per-theme, because lime is illegible
on the light canvas. It appears on the hero wordmark (`.hi`), the
`:focus-visible` ring, and — **in dark mode only** — three accent
treatments, each applied to the same trait in every case study rather than
as a one-off:

| Trait | Element | Dark | Light |
|---|---|---|---|
| Accent word in a case-study title | `.cs-hero h1 em` | `--brand` | `--body` |
| Context metrics (the cost of the old system) | `.stat-n` | `--danger`, matching the critical-card left bar | `--ink` |
| Paired comparison headings | `.dec-col h3`, `h3.accent` | `--brand` | `--ink` |
| Impact card titles (16, all four projects) | `.impact-card h3` | `--brand` | `--ink` |
| Inline key figures in a card | `.after-n` | `--brand` | `--ink` |

Light mode stays neutral on all three: the olive equivalent sits too close
to body copy and muddies the hierarchy. Add new accents to the
`DARK-MODE ACCENTS` block, never inline.

`--danger` is the only semantic colour, and it earns its place in three
spots: the left border on a critical problem card, the `Cons` label and
bullet in an interaction-model card, and the manual-flow diagram.

## 3. Typography

**Geist** for everything, **Geist Mono** for the technical caption voice.
Weights 400 / 500 / 600 only. 600 is the display ceiling.

| Token | Size | Weight | Tracking | Use |
|---|---|---|---|---|
| `--fs-dlg` | 32px | 600 | `-.04em` | Section `h2` |
| `--fs-dmd` | 24px | 600 | `-.04em` | Project card titles, big numerals |
| `--fs-dsm` | 20px | 600 | `-.03em` | Card `h3`, pull quotes |
| `--fs-lg` | 18px | 400 | `0` | Lead paragraphs |
| `--fs-md` | 16px | 400 | `0` | Body |
| `--fs-sm` | 14px | 400/500 | `-.02em` | Card body, labels, buttons |
| `--fs-xs` | 12px | 400 | `0` | Captions, eyebrows (mono) |

Hero `h1`s are the only `clamp()` in the system, one per page type.

### Principles

- **Sentence case everywhere. No all-caps.** This is the rule that removed
  169 uppercase micro-labels from the page.
- **Negative tracking on display sizes** is part of the voice.
- **Mono is for the technical layer only:** eyebrows, section numbering,
  metric captions, figure captions, `<cite>`. Never body copy.
- **Em-dashes are rationed.** Appositives take a colon, parentheticals take
  commas or parentheses, and two independent clauses take two sentences.
  Four em-dashes remain in the whole document, each because it beats the
  alternative.

## 4. Layout

- Base unit 4px. Space tokens `--sp-1` (4px) through `--sp-10` (96px).
- `--maxw` 1200px content, `--measure` 720px prose. Prose is capped at
  `--measure` so long paragraphs stay readable; `.wide` opts out.
- `--gutter` 48px desktop, 24px at ≤1024px, 20px at ≤860px.
- `--sec-y` 96px desktop, 72px tablet, 64px mobile.
- **Large gaps between bands, tight interiors.** 8px from a headline to its
  paragraph, 64–96px between sections.
- Two breakpoints only: 1024px (tablet) and 860px (mobile), each a single
  media block.

## 5. Elevation

Stacked hairline shadows, never a single heavy blur.

| Token | Treatment | Use |
|---|---|---|
| `--e1` | inset 1px hairline ring | Default panel chrome |
| `--e2` | `--e1` + two small offsets | Project cards, nav |
| `--e3` | `--e1` + three offsets | Hover state, modal |

## 6. Shape

`--r-xs` 4px (the one surviving chip) · `--r-sm` 6px (nav-scale controls,
inputs) · `--r-md` 8px (all panels) · `--r-lg` 12px (image frames, project
cards, modal) · `--r-pill` 100px (**marketing-scale CTAs only**, meaning
the hero button and the theme switch track).

The two pill scales must not mix on one screen: nav-scale controls are 6px,
marketing CTAs are 100px.

## 7. Components

One primitive, then modifiers. `.card` carries background + radius +
`--e1`; every lifted surface shares that rule and adds only its padding:
`.out-card`, `.whatido-card`, `.stat`, `.prob-card`, `.step`, `.insight`,
`.ux-card`, `.decision`, `.state-table-wrap`, `.impact-card`, `.ref-card`,
`.im-card`, `.pcard`, `.pwd-modal-card`.

**Two label tiers.** A section label is a navigational landmark and a
caption is not, so they are not the same size or colour:

- **Section tier** (`.eyebrow`, `.cs-label`, `.cs-eye`): mono 14px/500,
  `--body`, sentence case. `.eyebrow` takes `--ink` because it is a
  standalone heading with no adjacent `h2` to carry the weight.
- **Caption tier** (`.fig-cap`, `.pcard-meta`, `.imp-l`, `.prob-n`,
  `.step-n`, `.krf-n`, `.ref-tag`, `.im-num`, `.cs-meta-item label`,
  `.state-table th`): mono 12px/400, `--body`.

`--mute` is for decorative marks only — bullet dots and flow arrows. Never
for text. A 12px mono caption in `--mute` disappears.

| Component | Notes |
|---|---|
| `.label` | Sans 14px/500 `--body`, for label text read as content (`Pros`/`Cons`, table row names) |
| `.manual-flow` | Runs top to bottom at every width. Sequences read as sequences vertically; side by side they read as a table and force two-word line breaks |
| Layout modifiers | `.g1/.g2/.g4/.flush-top/.gap-5` are declared **last** in the sheet. They are single-class selectors, so placed before `.ux-grid` / `.ref-grid` / `.decision` they are silently dead |
| `.frame` | Image frame: full width, `--r-lg`, `--e1`, `--sp-5` top margin. `.flush` removes the margin |
| `.prob-card.crit` | 2px `--danger` left border. **This is the severity signal** — do not add a "Critical" tag beside it |
| `.im-badge` | The only chip in the system. 4px radius, mono, `--canvas-soft-2`. It survives because it carries information available nowhere else |
| `.bullets`, `.dec-col ul`, `.im-list`, `.ims-list`, `.after-list` | All use a `·` marker. No em-dash glyphs |
| `.pcard` | A `<button>`, not a clickable `<div>`, so it is keyboard-reachable |

## 8. Motion

Two durations (`--dur-1` .15s, `--dur-2` .25s) and one easing
(`--ease`). No keyframes. `prefers-reduced-motion` shortens transitions
and drops the decorative hero video, but keeps case-study demo videos,
which are content.

## 9. Do's and Don'ts

### Do
- Reserve `--ink` for CTAs and emphasis. Black ink is the conversion target.
- Set every headline sentence case at weight 600 with negative tracking.
- Put metadata in `.eyebrow` (mono, `--mute`), not in a box.
- Use the surface ladder for hierarchy: `canvas-soft` → `canvas` → `ink`.
- Layer stacked hairline shadows rather than one heavy drop.
- Let case-study imagery run full content width in a `.frame`.
- Cap prose at `--measure`.

### Don't
- **Don't add a chip, badge, tag, or pill.** If a label is worth showing,
  it is worth showing as an `.eyebrow` or as prose. The one exception,
  `.im-badge`, is already spent.
- Don't introduce a second accent colour, and don't use `--brand` for
  anything but the wordmark and the focus ring.
- Don't set a headline in all-caps, or add letter-spacing to a label.
- Don't reach for an em-dash. Use a colon, a comma, or a full stop.
- Don't add `backdrop-filter` outside the nav, or bring back an
  atmospheric gradient.
- Don't promote display type to weight 700+.
- Don't write layout into a `style` attribute; add a class.
- Don't hardcode a colour, space, radius, or duration. Every value in the
  system has a token.
