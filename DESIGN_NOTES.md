# Handoff: imagine.hn — landing page + manifesto

## Overview
imagine.hn is an anonymous publication: a collection of ideas for Honduras on nature conservation, democracy and quality of life. Two pages:

1. **Landing page** — masthead with an animated logo, one headline, a gallery of posts (published + upcoming), and a footer with an Instagram link.
2. **Manifesto page** — the first post: a long-form bilingual document ("Manifiesto para Honduras", 15 chapters), already written and laid out.

Both pages are bilingual (Spanish first, English second) with a `es / en` toggle. The tone is quiet, printed-paper, public-domain: no branding chrome, no data collection, no calls to action beyond reading and sharing.

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes that show intended look and behavior. They are not production code to copy directly.

The task is to **recreate these designs in the target codebase's environment** (React/Next, Astro, plain static HTML — whatever the project uses) following its established patterns. If no codebase exists yet, pick the simplest appropriate stack; this is a two-page, mostly static site, so a static generator or plain HTML/CSS is entirely adequate and matches the project's ethos (fast, cheap to host, works offline).

Note on the landing file: `Imagine Landing.dc.html` is authored in a prototyping format (a `<x-dc>` template plus a small logic class, with `support.js` as its runtime). **Do not port that runtime.** Read it as markup + behavior spec: the template is ordinary inline-styled HTML, and the logic class holds only the language toggle state and the logo morph loop. `Imagine_manifiesto.html` is plain self-contained HTML and can be treated as near-final markup.

## Fidelity
**High-fidelity.** Colors, typography, spacing, the logo artwork and the morph timing are all final and should be reproduced faithfully. The one caveat: the Instagram glyph in both footers is a geometric approximation — replace it with the official mark from Instagram's brand resources, and set the real profile URL (currently `https://www.instagram.com/`).

---

## Screens / Views

### 1. Landing page

**Purpose:** show what imagine.hn is in one line, and let people open the posts.

**Layout:** single centered column, `max-width: 62rem`, `margin: 0 auto`, padding `clamp(1.5rem,4vw,2.5rem) clamp(1.25rem,5vw,3rem) 6rem`. Page background `#f7f5f0`, text `#0b3d63`.

**a) Masthead** — vertical flex, centered, `gap: clamp(1.6rem,4vw,2.6rem)`, `padding-bottom: clamp(2rem,6vw,4.4rem)`:
- **Language toggle** (first): `es` / `en` separated by a `/` at `opacity:.4`. Font `.72rem`, `letter-spacing:.18em`, lowercase. Active language `#0b3d63` with a 1px bottom border; inactive `#476b88`, no border. Buttons, not links (client-side state).
- **Logo** (below): the animated imagine mark, `width: clamp(7rem,14vw,9.5rem)`, aspect ratio `535.9 / 470`. See **Logo & morph animation**.

**b) Hero** — grid, `gap: clamp(2rem,5vw,3rem)`, `padding-bottom: clamp(2.4rem,5.6vw,4.2rem)`:
- **Headline**, centered, `max-width: 30rem`, `justify-self: center`: `font-size: clamp(1.3rem,3.3vw,2.18rem)`, `line-height:1.2`, `letter-spacing:-.01em`, weight 400, `text-wrap: balance`.
  - ES: “Algunos dirán que somos solo unos soñadores. Pero no somos los únicos.”
  - EN: “Some may say we are dreamers. But we are not the only ones.”
- **Hand-drawn rule** directly below the headline (replaces a border): inline SVG, `viewBox="0 0 1000 10"`, `preserveAspectRatio="none"`, `width:100%; height:10px`, path
  `M2,5.4C90,3.6 150,6.6 260,5.1C370,3.6 430,6.9 545,5.6C660,4.3 720,3.2 820,5.0C900,6.4 950,6.0 998,4.6`,
  `fill:none; stroke:#0b3d63; stroke-width:2.6; stroke-linecap:round; vector-effect:non-scaling-stroke`.
  The wobble is intentional — it matches the hand-drawn feel of the logo. The same rule is reused on the manifesto page.

**c) Post gallery** — `padding: clamp(1.75rem,4.2vw,2.8rem) 0 0`; grid `repeat(auto-fill, minmax(8.8rem, 1fr))`, `gap: clamp(1.8rem,4vw,3rem)`. Four cards, in order:

| # | Mark fill | Title | Second line | Link | Dimmed |
|---|---|---|---|---|---|
| 1 | Honduran flag | Manifesto para Honduras / A Manifesto for Honduras | 15 de septiembre 2026 / September 15, 2026 | manifesto page | no |
| 2 | three raised hands | Democracia transparente / Transparent democracy | soñando... / dreaming... | none | yes |
| 3 | chess pieces | No más guerras / No more wars | soñando... / dreaming... | none | yes |
| 4 | empty circle | *(no text)* | — | none | yes |

Card structure: grid, `gap:.9rem`, `align-content:start`. Mark at `width:80%`, aspect ratio `384 / 331`. Title `1.12rem / line-height 1.25`, margin-bottom `.3rem`. Second line `.72rem`, `letter-spacing:.12em`, color `#476b88`.
- Published card is an `<a>` with hover `opacity:.72`; the rest are plain `<div>`s.
- **Dimming rule (accessibility):** apply `opacity:.45` **only to the mark**, never to the wrapper — labels must stay full-opacity `#476b88` (≈5.1:1 on the paper). Earlier drafts dimmed the whole card and the text fell to 2:1.

**d) Footer** — `padding: clamp(3rem,8vw,5.5rem) 0 0`, column flex, centered, `gap:1rem`, **no separator line**:
- Instagram icon link, 30×30, stroke `#0b3d63`, `stroke-width:1.9`, hover `opacity:.65`.
- Caption `.78rem`, `letter-spacing:.06em`, `#476b88`, centered:
  ES “Esperamos que algún día te unas a nosotros” · EN “We hope some day you will join us”.

### 2. Gallery marks (post icons)

Each mark is the imagine logo **without the wordmark**: the large circle plus its two bubbles, in an SVG cropped to `viewBox="32 -6 384 331"`.

Construction, in order:
1. `<clipPath>` holding the circle's **outer contour only** (first subpath of the circle path).
2. The fill artwork inside `<g clip-path="url(#id)" transform="rotate(2 267.8 156)">` — the +2° rotation matches the circle's own tilt (measured from the artwork: its axis leans 1.98°).
3. The full circle path (donut, outer + inner subpath) painted **on top** in `#0b3d63`, so the ring outline survives.
4. The two bubble paths, also `#0b3d63`.

**Every clipPath id must be unique per instance.** The Spanish and English blocks both exist in the DOM; duplicate ids caused the English mark to render unclipped (a hidden ancestor drops the shared clip). Suffix ids per language/instance.

Fills used:
- **Flag:** three bands across the circle — `#0b3d63` top (`y:-70 h:174`), `#f7f5f0` middle (`y:104 h:104`), `#0b3d63` bottom (`y:208 h:180`), each `x:80 w:376`; five blue stars in a quincunx centered at (267.8, 156), offsets ±52 x / ±34 y, radius 13, drawn with `stroke-width:3.4; stroke-linejoin:round` so the points are rounded rather than needle-sharp.
- **Hands (democracy):** icon scaled `0.2993`, translated `(88.2, -15.7)`. Arms are split at `y=820` in icon space: the hands render at natural proportion (clipped to `y<820`), the arms below are drawn again with `translate(0,820) scale(1,1.554) translate(0,-820)` and clipped to `y>820`, so they stretch past the bottom of the circle as if the hands come from below. The seam is invisible because both copies coincide at the cut.
- **Chess:** icon scaled `0.224`, translated `(133.4, 42)`.

### 3. Logo & morph animation (masthead)

Composition: the static artwork (`imagine-static.svg` = wordmark + two bubbles) as an `<img>`, with an overlaid SVG (`viewBox="0 0 535.9 470"`) containing:
- the **original circle path** (`data-ring-static`) — the exact artwork, shown at rest;
- a **nested SVG** at `x="111.75" y="0" width="312.1" height="312.1"` with `viewBox="0 0 1200 1200"` (the icons' coordinate space) holding the **morph path**, inset by half its stroke so nothing clips:
  `M600,25C886.6,25 1118.8,282.4 1118.8,600C1118.8,917.6 886.6,1175 600,1175C313.4,1175 81.2,917.6 81.2,600C81.2,282.4 313.4,25 600,25Z`

Behavior: the circle morphs through four icons — **love → peace(A) → community → peace(B)** — then back to the circle, and loops. Shapes live in `logo-shapes.js` (`icons: [{name, paths[]}]` in a 1200×1200 space, plus `ringD`).

- Interpolation uses **flubber** (MIT) — `flubber.separate()` for circle→icon and `flubber.interpolateAll(..., {match:true})` for icon→icon. GSAP's MorphSVG plugin is paid; flubber gives the same behavior with no license cost. GSAP itself is not required — a `requestAnimationFrame` loop drives progress.
- Icon subpath counts differ (3 / 2 / 14 / 5). They are **padded to the max count by repeating existing paths** — duplicates overlap exactly, so they are invisible, and pairwise morphing becomes possible.
- Timing per segment: hold **1900ms**, morph **1000ms**; easing `inOutCubic`. Five segments (4 icons + return), so a full cycle is 14.5s.
- Appearance: at rest the mark is a **stroked ring** (`stroke-width:50` in the 1200 space, `fill-opacity:0`); as it morphs, `fill-opacity` goes 0→1 and `stroke-width` 50→0, so icons read as solid silhouettes. Reverse on the return segment.
- At rest, the generated ellipse is hidden (`opacity:0`) and the **original circle artwork** is shown instead; they swap the instant motion starts. Do not ship the ellipse as the resting state — the user's contour is the identity.

**Implementation pitfalls that cost real debugging time:**
- Never bind the loop to a component's mount flags/refs alone. Make it a page-level singleton that re-queries the target node each frame; a remount otherwise kills the chain silently.
- `requestAnimationFrame` timestamps can *precede* a `performance.now()` captured just before, so `(now - t0) % total` can go negative. Normalize: `(((now - t0) % total) + total) % total`.
- Clamp progress to `≤0.999`. At exactly `t=1` flubber returns the raw target path, whose relative `m` subpath commands concatenate into displaced geometry.
- Honor `prefers-reduced-motion: reduce` — leave the static circle.

### 4. Manifesto page

Self-contained bilingual document, `max-width: 44rem` column, padding `clamp(2.5rem,7vw,6rem) clamp(1.25rem,5vw,2rem) 5rem`.

- **Header row** (above the article): 3-column grid `1fr auto 1fr`, `align-items:start`, `margin-bottom: clamp(2.5rem,6vw,4rem)`:
  left = the animated imagine mark at `width:5.4rem` linking back to the landing page; center = `es / en` toggle (nudged `margin-top:1.1rem` onto the marks' optical line); right = the post's flag mark at `width:5.4rem`, `justify-self:end`.
- **Header block** (centered): publication date above the title (`.74rem`, `letter-spacing:.3em`, lowercase, `#476b88`), then the title (`clamp(1.6rem,4.4vw,2.6rem)`, `line-height:1.16`, weight 400), then the hand-drawn rule. No standfirst, no "dominio público" label.
- **Index**: two-column list (`columns: 15rem 2`), label “índice / contents” lowercase `.7rem`, `letter-spacing:.28em`.
- **Chapter numbers are Maya numerals**, not Roman — base-20 dots and bars: `bars = floor(n/5)`, `dots = n % 5`; dots row on top (4px circles, 2.5px gap), bars below (17×2.5px, 1.5px radius), stacked in an inline-flex column, `currentColor`, `aria-hidden="true"`. Used in the index and in the “capítulo …” kickers (label lowercase).
- **Footer**: hand-drawn rule, then four social icons centered (WhatsApp, Facebook, X, Instagram) as 2.6rem circles with a 1px `#0b3d63` border, no “compartir” label; below them a pill link back to the top — `padding:.75rem 1.7rem`, `border-radius:2rem`, `.74rem`, `letter-spacing:.18em`, `white-space:nowrap` — “volver al inicio / back to the start”.
- **Reading progress bar**: fixed, 4px, top of viewport, track `rgba(11,61,99,.10)`, fill `#0b3d63`, `transform: scaleX(progress)`, `transition: transform 100ms linear` (none under reduced motion).

## Interactions & Behavior
- **Language switch, landing page:** client state; both language blocks exist in markup, one rendered at a time. Spanish is the default and paints first.
- **Language switch, manifesto page:** CSS-only, no JavaScript — `body:has([id^="en"]:target) [data-lang="es"] { display:none }` and the inverse for `[data-lang="en"]`. The `#en` anchor sits on the **English header row**, not the `<header>`, so switching lands on the top of that view rather than scrolling past the logo.
- **Post cards:** published card links to the manifesto; upcoming cards are inert (not disabled links).
- **Hover:** cards `opacity:.72`; footer icon `opacity:.65`; links `#0b3d63` → `#0b3d63` with border emphasis.
- **Print:** the manifesto hides `[data-noprint]` elements and the progress bar, drops link colors to black, sets `@page { margin: 18mm 17mm }` and keeps `orphans/widows: 3`.
- **Responsive:** everything is fluid (`clamp()`, `auto-fill` grid). No fixed widths; the gallery reflows from 4 columns down to 1.

## State Management
Minimal:
- `lang: 'es' | 'en'` — landing page only (manifesto uses the URL fragment).
- Morph loop internals: start timestamp, segment index, progress `t` — derived from the clock each frame, not stored.
- No data fetching. No forms. No analytics, no cookies, nothing collected.

## Design Tokens
Colors:
- Paper `#f7f5f0`
- Ink / primary `#0b3d63`
- Secondary text `#476b88`
- Rules / hairlines `#c3cfd9`
- Selection `#dce6ee`
- Card hover wash `rgba(11,61,99,.05)`

Typography: **Open Sans** (Google Fonts, weights 300–700 + italic), fallback `Helvetica, Arial, sans-serif`.
- Headline `clamp(1.3rem,3.3vw,2.18rem)` / 1.2 / weight 400
- Document title `clamp(1.6rem,4.4vw,2.6rem)` / 1.16
- Chapter heading `clamp(1.5rem,4vw,1.95rem)` / 1.15
- Body `clamp(1.06rem,2.4vw,1.16rem)` / 1.72, `text-wrap: pretty`
- Card title `1.12rem` / 1.25 · card meta `.72rem` / `letter-spacing:.12em`
- Small labels `.7–.74rem`, `letter-spacing:.18–.3em`, **lowercase** (no uppercase transforms anywhere)

Spacing: fluid `clamp()` throughout; section rhythm `3.4rem` between chapters, `1.15em` between paragraphs.
Radius: `2rem` pill button, `50%` icon circles, `1.5px` on Maya bars.
Shadows: none anywhere — the design is flat ink on paper.
Line weight: hand-drawn rule `2.6px`; hairlines `1px`; ring stroke `50` units in the 1200-space (≈12px at logo scale).

## Assets
In this bundle:
- `imagine.svg` — full logo, user-supplied artwork (wordmark, two bubbles, large circle). Fill forced via a root `fill="#0b3d63"` attribute; a `<style>` inside `<defs>` was stripped by tooling, so keep the attribute.
- `imagine-static.svg` — the same artwork with the large circle removed (used under the morphing circle).
- `logo-shapes.js` — `icons[]` (love, peace ×2, community) and `ringD`, all in a 1200×1200 space.
- `Imagine Landing.dc.html`, `Imagine_manifiesto.html` — the two design references.
- `support.js` — prototyping runtime only. **Not for production**; included so the landing file opens in a browser as-is.

External: **flubber 0.4.2** (MIT, `cdn.jsdelivr.net/npm/flubber@0.4.2`) and Google Fonts (Open Sans).

Third-party icon sources (from The Noun Project, licensed by the client — verify attribution requirements before shipping): love, peace ×2, community, democracy (raised hands), chess. The Instagram glyph is a placeholder approximation.

One tradeoff worth flagging: the manifesto page was originally built to make **zero network requests** — fully offline, nothing collected. Matching the landing page's typeface introduced a Google Fonts request, and the header morph adds the flubber CDN. If offline-proof matters, self-host both.

## Files
- `Imagine Landing.dc.html` — landing page design reference
- `Imagine_manifiesto.html` — manifesto page design reference (near-final markup)
- `imagine.svg`, `imagine-static.svg`, `logo-shapes.js` — logo artwork and morph shapes
- `support.js` — prototype runtime, do not port
