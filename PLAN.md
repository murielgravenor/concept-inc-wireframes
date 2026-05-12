# PLAN.md — Concept Inc. Homepage Hi-Fi Build

**For Muriel's review before any code is written.**

---

## What I read

- **Wireframe**: `homepage/index.html` — 9 sections, structure and content confirmed.
- **Brand guide**: `Brand Identity & Website Guide - Concept Inc..pdf` — full colour system, type scale, and discipline rules confirmed.
- **Assets**: `/assets/` has 4 logo files only (`logo v1.png`, `logo v1 light.png`, `C black.png`, `C reversed.png`). No `/assets/photography/` directory exists — all photo slots will be CSS placeholders with `<!-- TODO: real photo -->`.

---

## Conflicts — please decide before I build

### Conflict 1 — Hero CTA button is invisible on its own background
**What the wireframe says:** Primary CTA uses `btn-black` (black fill, off-white text) on a dark-overlaid hero photo.  
**The problem:** Black button on a dark/near-black overlay disappears. It won't read at all.  
**My proposed resolution:** Replace with an off-white fill + brand-black text button for the primary CTA. Off-white on dark reads cleanly, doesn't use orange, and saves the single orange signal for the footer conversion moment. Secondary CTA stays as the white outline.  
**Alternative if you prefer orange here:** Use burnt orange for the primary hero CTA, making it the one orange signal for that viewport. The Curated eyebrow and footer button each appear in separate viewports as you scroll, so per-viewport discipline is maintained.

> **Decision needed: off-white button (my default) or orange?**

### Conflict 2 — Two orange uses across the page
**What the wireframe says:** Orange appears twice — as an eyebrow label in the Curated band (§5) and as the "Get a quote" button in the Footer CTA band (§8). The wireframe even labels these `ORANGE #1` and `ORANGE #2`.  
**The brand rule:** "One clear signal per viewport."  
**Verdict (no decision needed, flagging for transparency):** These two orange moments are always in *separate viewports* — a user never sees both simultaneously. The per-viewport rule is satisfied. I'll keep both as the wireframe specifies.

### Conflict 3 — No event photography available
**What the brief expects:** `/assets/photography/` with event photos.  
**Reality:** Directory doesn't exist. Only logo files are present.  
**Resolution:** All photo slots get styled CSS placeholder blocks in the brand's `--light-grey` / `--placeholder` tone with `<!-- TODO: real photo -->` comments. The hero will have a warm dark gradient block that evokes the photo's role without looking like a broken image. Once Duane provides photography, each placeholder can be swapped with a single `background-image` or `<img>` swap.

### Conflict 4 — Font: build spec vs. brand guide heading recommendation
**Build spec says:** Plus Jakarta Sans for all text.  
**Brand guide says:** DM Sans / Manrope / Inter for headings; Plus Jakarta Sans listed as one option for body.  
**Resolution:** Following the build spec — Plus Jakarta Sans at 400/600/700 for everything. It's in the brand guide's approved body list, handles display sizes well, and using one font family reduces HTTP requests (important for slow SA mobile connections). No conflict in practice.

---

## Section-by-section breakdown

### §1 — Header / Nav

**What it is:** Sticky header. Logo left, nav + CTA right. Mobile: logo + hamburger.

**Visual treatment:**
- Background: `--off-white` (#FAFAF7), 1px `--light-grey` bottom border, subtle box-shadow on scroll.
- Logo: use `assets/logo v1.png` (dark version) on the light header background. Mark with `<!-- TODO: replace with final logo asset -->`.
- Nav links: Plus Jakarta Sans 14px, weight 500, `--soft-black`. Active page in weight 700. Hover: smooth colour transition to `--brand-black`.
- Dropdowns (Production, Events): absolute panel, 1px `--light-grey` border, shadow, 160px min-width. CSS `:hover` + `:focus-within`.
- "Get a quote" button: `--brand-black` fill, off-white text, 14px. **Not orange** — saving orange for the footer's primary conversion moment.
- Mobile (≤768px): nav collapses to a hamburger icon (3-line SVG). Tap opens a full-width slide-down panel over the page content. Handled in `script.js` alongside scroll reveals.

**No conflicts.**

---

### §2 — Hero

**What it is:** Full-bleed photo background, gradient overlay, headline, subhead, two CTAs.

**Visual treatment:**
- Height: 85vh mobile, 90vh desktop.
- Background: dark placeholder `#2A2522` (warm dark neutral matching brand black) with `<!-- TODO: real photo -->`. Real implementation: `background-image: url(...)` as `background-size: cover`.
- Overlay: `linear-gradient(to top, rgba(26,22,18,0.88) 0%, rgba(26,22,18,0.45) 55%, transparent 100%)` — bottom-heavy so text sits on solid dark while top of photo reads.
- H1: "Bring your concept to life." — Plus Jakarta Sans 700, 52px desktop / 36px mobile, off-white, line-height 1.1, letter-spacing -0.02em.
- Subhead: 17px, `rgba(250,250,247,0.72)`, max-width 520px.
- Primary CTA "See packages": **off-white fill + brand-black text** (see Conflict 1 above — my default). 2px border off-white for hover state.
- Secondary CTA "Talk to us": transparent fill, 2px off-white border, off-white text.
- Scroll reveal: hero content fades up on load (CSS animation, not IntersectionObserver — it's the first thing visible).

**Conflict 1 applies here — awaiting your decision.**

---

### §3 — Persona Routing ("What are you planning?")

**What it is:** 4-card routing grid. 1-col mobile → 2-col tablet → 4-col desktop.

**Visual treatment:**
- Section background: `--off-white`, 1px `--light-grey` bottom border.
- Section heading "What are you planning?": H2 scale, `--brand-black`.
- Card grid: 1px `--light-grey` gap lines between cards (the `gap: 1px / background: var(--light-grey)` trick from the wireframe — keeps it sharp and minimal).
- Cards: `--off-white` fill, 28px padding. On hover: 2–4px `translateY(-3px)` lift + `box-shadow: 0 8px 24px rgba(26,22,18,0.08)`. Smooth 200ms transition.
- Card icon placeholder: 32×32px `--light-grey` block. `<!-- TODO: replace with SVG icons -->`.
- H3 (card title): 22px semibold, `--brand-black`.
- Price note: 13px, `--mid-grey`, weight 600, slight letter-spacing.
- Body copy: 15px, `--mid-grey`, line-height 1.55.
- "→" card links: 13px, weight 700, `--brand-black`, underline on hover.
- No orange in this section — stays neutral, lets the routing be the focus.

**Scroll reveal:** cards fade up staggered (100ms delay between each).

---

### §4 — Credibility Strip ("More than gear and crew")

**What it is:** 3-column service overview. 1-col mobile → 3-col desktop.

**Visual treatment:**
- Background: `--off-white`, 1px `--light-grey` bottom border.
- Eyebrow label "What we do": 12px, weight 700, letter-spacing +0.08em, all-caps, `--mid-grey`.
- H2 "More than gear and crew.": H2 scale, `--brand-black`, max-width 560px.
- Column separator: `2px solid --brand-black` top border on each `<h3>` (bold editorial move from the wireframe). Tight, confident.
- H3 (column heading): 18px semibold, `--brand-black`.
- Body paragraph: 15px, `--mid-grey`, line-height 1.6.
- List items: `—` prefix, 14px, `--mid-grey`.
- No orange.

**Scroll reveal:** columns fade up on entry.

---

### §5 — Curated Band

**What it is:** Full-width `--brand-black` background block. Announces the Curated product line.

**Visual treatment:**
- Background: `--brand-black` (#1A1612), padding 5.5rem vertical.
- **ORANGE #1:** Eyebrow "Curated" label — burnt orange (#E85D04), 12px, weight 700, letter-spacing +0.1em, all-caps. Single small accent on a black field — very visible, completely brand-correct.
- H2 "When the brief is 'make it unforgettable.'": clamp(28px, 4vw, 44px), off-white, tight letter-spacing. Max-width 580px.
- Body copy: 16px, `rgba(250,250,247,0.62)`, line-height 1.65, max-width 480px.
- CTA "Explore": transparent fill, 2px off-white border, off-white text. **Not orange** — orange is already used on the eyebrow, keeping one per viewport.
- Layout: left-aligned text. On desktop, copy left, optional decorative element right (or just generous whitespace).

**Orange discipline:** Eyebrow is the one orange element in this viewport. CTA stays off-white outline. ✓

---

### §6 — Portfolio Preview ("Recent work")

**What it is:** 4-up image grid with caption labels. 2-col mobile → 4-col desktop.

**Visual treatment:**
- Background: `--off-white`, 4rem top/bottom padding.
- Section header row: "Recent work" H2 left, "View all →" link right (14px, weight 700, `--brand-black`).
- Grid: `repeat(4, 1fr)`, `gap: 12px` desktop / `repeat(2, 1fr)` mobile.
- Photo placeholders: `aspect-ratio: 4/3`, `--light-grey` background, `<!-- TODO: real photo -->`. Slight scale transform on hover (`scale(1.02)`) inside `overflow: hidden` container.
- Caption labels: 13px, `--mid-grey`, weight 500.
- No orange.

**Scroll reveal:** grid fades up on section entry.

---

### §7 — Social Proof

**What it is:** Italic blockquote + client logo strip. Black background.

**Visual treatment:**
- Background: `--brand-black`, padding 5rem.
- Blockquote: Cormorant Garamond Italic (loaded for the logo wordmark anyway) at 22–26px, off-white, line-height 1.55, centred, max-width 660px. Opening `"` in burnt orange (a single character — barely an accent, but adds warmth).
- Cite: 13px, weight 600, `rgba(250,250,247,0.45)`, letter-spacing +0.08em, all-caps.
- Logo strip: 5 placeholder `80×28px` blocks, `rgba(250,250,247,0.12)` fill, centred with flex-wrap. `1px solid rgba(250,250,247,0.08)` top border separator.
- `<!-- TODO: real client logos (SVG recommended for retina) -->`.

**Note on opening quote character as micro-orange:** This is a single typographic character, not a UI element. It adds warmth without functioning as a CTA or signal. I consider it within the spirit of the rules — but flagging in case you disagree and prefer to remove it.

---

### §8 — Footer CTA Band ("Ready to transform your event?")

**What it is:** Full-width conversion section. Single CTA.

**Visual treatment:**
- Background: `--off-white`, `1px solid --light-grey` top border, generous vertical padding (5rem).
- H2 "Ready to transform your event?": H2 scale, `--brand-black`, centred, max-width 480px.
- **ORANGE #2:** "Get a quote" button — burnt orange fill, off-white text, 2px orange border. This is the page's primary conversion CTA — the one place burnt orange appears as a filled button.
- Links to `mailto:hello@conceptinc.co.za` (from the wireframe).
- Hover: orange darkens slightly (`filter: brightness(0.9)`), slight scale-up.

**Orange discipline:** This viewport contains only one orange element — the button. ✓

---

### §9 — Site Footer

**What it is:** Minimal footer. Logo, location, social links, copyright.

**Visual treatment:**
- Background: `--brand-black`, padding 2rem.
- Logo: `assets/logo v1 light.png` (light version on dark bg). Height 40px. `<!-- TODO: final logo asset -->`.
- Footer meta: "Cape Town, South Africa / hello@conceptinc.co.za" — 13px, `rgba(250,250,247,0.45)`.
- Links (Instagram, Facebook, Privacy policy): 13px, `rgba(250,250,247,0.4)`. Hover to 0.7.
- Copyright: "© 2026 Concept Inc." — 12px, `rgba(250,250,247,0.25)`.
- Layout: logo + meta stacked on mobile; row layout with logo/meta left, links right on desktop.

---

## Technical plan

**Files:** `index.html`, `styles.css`, `script.js` (scroll reveals + mobile nav toggle).

**Google Fonts to load:**
```
Cormorant+Garamond:ital@1   (logo "Concept" cursive placeholder + blockquote)
Plus+Jakarta+Sans:wght@400;600;700   (all UI text)
```

**Scroll reveals:** `IntersectionObserver` — on entry, add `.is-visible` class that triggers a CSS `opacity 0→1 + translateY 20px→0` transition. 400ms ease-out. No reveals on the hero (it's the first thing visible) or header.

**Mobile nav:** JS toggle on hamburger click — adds `.nav-open` to `<body>`, which triggers a full-width slide-down panel via CSS. Accessible: `aria-expanded` toggled, focus trapped in panel.

**Responsive breakpoints:** `480px` (small mobile), `768px` (tablet), `1200px` (desktop).

**CSS architecture:** single `styles.css` with clear section comments. Custom properties on `:root`. No utility classes — just semantic component classes.

---

## Open questions for you

1. **Conflict 1 decision:** Off-white button or orange on the hero primary CTA?
2. **Mobile nav:** Slide-down panel (my default) or full-screen overlay?
3. **Cormorant Garamond for the blockquote quote:** Happy with this, or keep it all Plus Jakarta Sans?
4. **Logo placeholder:** The existing `logo v1.png` / `logo v1 light.png` assets are in place from the wireframe work. Should I use those directly, or build the inline SVG wordmark as spec'd? (My default: use the existing PNGs since they're already in use across the wireframe pages, and add the TODO comment.)

**Awaiting sign-off before I write any HTML/CSS.**
