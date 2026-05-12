# NOTES.md — Homepage Hi-Fi Build

Deviations from the wireframe, decisions made, and things still to do.

---

## What was built

`index.html` + `styles.css` + `script.js` — opens directly in any browser, no build step.  
Screenshots at three breakpoints are in `/screenshots/`.

---

## Deviations from the wireframe

### 1. Hero primary CTA — off-white button (approved)
Wireframe specified `btn-black` (black fill) for the hero primary CTA, which would be invisible on the dark hero background. Changed to an off-white fill with brand-black text per your decision in PLAN.md review.

### 2. Header "Get a quote" hidden on mobile
On narrow viewports the header CTA and hamburger compete for space. The button is hidden below 768px — it reappears in the mobile nav slide-down panel. The conversion path is still one tap away on mobile.

### 3. No photography — all photo slots are CSS placeholders
The `/assets/` folder contains only logo files. All photo positions use warm grey gradient blocks marked `<!-- TODO: real photo -->`. To swap in an image, either:
- **Hero:** add `background-image: url('assets/photography/hero.jpg')` to `.hero-photo` in `styles.css`
- **Portfolio grid:** replace each `.portfolio-img-placeholder` div with an `<img>` tag

### 4. Testimonial — Cormorant Garamond Italic loaded for blockquote
One additional Google Font was loaded (Cormorant Garamond Italic) to give the testimonial an editorial, serif quality distinct from the UI type. Adds ~40KB on first load. If bandwidth is a priority, this can be removed and the blockquote falls back to Plus Jakarta Sans Italic — still readable, less characterful.

### 5. Opening quote mark in burnt orange
A single typographic `"` character before the blockquote is set in `--burnt-orange`. This is not a UI element (not a CTA, not a highlight) — it's a micro-typographic warmth signal. It does not conflict with the single-orange-signal-per-viewport rule. Remove it in `index.html` (`.quote-open` span) if preferred.

### 6. Section heading "Curated" (was "Curated Experiences")
All nav labels and page references already updated to "Curated" from the prior wireframe session. The homepage §5 eyebrow also reads "Curated" to match.

---

## Orange discipline — confirmed

| Location | Element | Role |
|---|---|---|
| §5 Curated band | Eyebrow label "Curated" | Brand signal — ORANGE #1 |
| §7 Social proof | Opening `"` quote mark | Micro-typographic warmth |
| §8 Footer CTA band | "Get a quote" button | Primary conversion CTA — ORANGE #2 |

These are always in separate viewports. No orange is used as a large background fill. ✓

---

## Scroll reveals

- All sections below the hero have `.reveal` (fade-up) on key elements.
- Cards within grids have staggered delays (`.reveal-d1` through `.reveal-d4`) — 80ms apart.
- The hero itself has no reveal — it's the first thing seen.
- `prefers-reduced-motion` is respected: all reveals are disabled for users who have that accessibility preference set.
- `IntersectionObserver` fires each reveal once and then stops observing — no unnecessary loop.

---

## Screenshots

Captured with Chrome headless at time of build. Scroll reveals are opacity: 0 in static screenshots — the page is fully visible when opened in a real browser.

| File | Viewport |
|---|---|
| `screenshots/mobile-375.png` | 375 × 812px |
| `screenshots/tablet-768.png` | 768 × 1024px |
| `screenshots/desktop-1440.png` | 1440 × 900px |

---

## Immediate next steps (before WordPress build)

1. **Photography.** Drop event photos into `/assets/photography/` and swap the `<!-- TODO: real photo -->` placeholders. The hero has the highest visual impact — one strong full-bleed image transforms the above-fold entirely.
2. **Logo asset.** Current build uses `logo v1.png` / `logo v1 light.png`. Once the final logo is signed off, update the two `<img>` tags in `index.html` (header and footer).
3. **Client logo strip.** Replace the 5 grey placeholder blocks in §7 with real SVG/PNG client logos.
4. **Testimonial copy.** Swap in the real client quote and attribution in the blockquote.
5. **Nav links.** The `href` values in the nav point to the local wireframe directory structure. These will need updating to WordPress permalink slugs.
6. **Icons.** The persona routing cards use simple inline SVGs (rings, building, speaker, sparkle). These can stay as-is or be replaced with a proper icon set.
