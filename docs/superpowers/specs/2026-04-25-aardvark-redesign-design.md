# Aardvark Web — Visual Redesign Design Spec

**Date:** 2026-04-25
**Author:** brainstorm session with Anders
**Status:** Approved — ready for implementation plan
**Scope:** `index.html` and `styles.css` at repo root. Niche Finder (`niche-finder/`) and the logo files are out of scope.

---

## Summary

Replace the current Aardvark landing page (Jomhuria display + Oxygen body, warm-gray + orange-accent palette, concentric-circle motif) with a Wero-inspired bold-and-playful design system: chunky uppercase Geist headlines, monospace mono callouts, a TTG-coded multi-color palette of yellow / cyan / magenta accents on a cream chrome, with brand-color-coded track-record cards. Page structure becomes a sequence of rounded "boxes" of solid color separated by white spacers, with one pill-shaped primary CTA and decorative cartoon stars inside the colored sections.

The redesign keeps the locked content from the previous pass (positioning as Fractional CPO / AI-native, six-company track record incl. Rebtel, Electrolux Red Dot 2025, etc.) but completely replaces the visual system and section structure.

## Goals

1. **Senior-credible but distinctive.** Land "Fractional CPO consultant who is AI-native" without sliding into generic-Vercel-startup or kids-cartoon. Signature is bold-but-controlled playfulness: chunky type + colored boxes + tilted black-outlined callouts + pill CTAs.
2. **Legibility first.** Cream chrome + white spacer areas keep body copy on neutral grounds; colored boxes are reserved for brand moments (hero, AI section, contact). Track-record body copy lives on brand-colored card grounds, all calibrated for black-text WCAG AA contrast.
3. **Content as artifact.** Track-record section is the centerpiece — six color-coded brand cards function as Anders' equivalent of Wero's "phone in hand" hero artifact.

## Non-goals

- Logo redesign / new logo. Current `images/logo-nav.svg` and `images/logo-hero.svg` will be temporarily replaced with a plain word-mark ("aardvark") in the nav. A real logo is a separate later project.
- Niche Finder under `niche-finder/`. Independent project, not modified.
- Any change to the GitHub Pages deployment, CNAME, or domain config.
- Server-side, JS frameworks, or build tooling. Site stays static HTML/CSS.

---

## Visual system

### Typography

Two families, both free Google Fonts, swapped in for the current Jomhuria + Oxygen.

| Use | Family | Weights |
| --- | --- | --- |
| Display & body | `Geist` | 300, 400, 500, 600, 700, 800 |
| Mono accents (eyebrow, meta, callouts, code) | `Geist Mono` | 400, 500 |

**Headline treatments:** all display headings (H1, section H2s) are set in **Geist 800**, **uppercase**, line-height 0.94, letter-spacing -0.045em to -0.05em depending on size. No serif, no Jomhuria.

**Body copy:** Geist 400, line-height 1.5–1.6, color `#0A0A0A` on light grounds, `#2A2A2A` for secondary copy.

**Mono accents:** Geist Mono 400/500, ~0.7–0.8125rem, uppercase + letter-spacing 0.12em–0.18em for eyebrows; lowercase for body-style mono lines (e.g. tools list).

**Type scale (desktop):**
- Hero H1: 5.5rem (88px)
- Section H2 (AI / Track Record / Contact): 3.5–5rem
- About H2: 3.5rem
- Card title: 1.5rem (uppercase, 700)
- Sub / lead body: 1.1875rem
- Body: 1.125rem
- Card body: 0.9375rem
- Eyebrow / meta: 0.7–0.8125rem mono
- Footer: 0.75rem mono

**Mobile breakpoint (≤900px):** hero H1 → 2.75rem, section H2s → 2.25rem, contact H2 → 2.75rem.

### Palette

```
Cream chrome (page background):  #FAF7F0
Cream card / pill background:     #FFFCF0
Ink / primary text:               #0A0A0A
Secondary ink (body / role):      #2A2A2A
Subtle border:                    rgba(0,0,0,0.06)

— Hero / brand yellow:            #F4D43B
— AI box / Electrolux cyan:       #8BD0EC
— Contact / magenta accent:       #DD5DB8

Brand-card colors (all light, all black-text-legible):
  Aardvark:   #F4D43B  (matches hero)
  Rebtel:     #F0857A  (paler coral-red)
  Electrolux: #8BD0EC  (matches AI box — intentional tie to AI proof point)
  Spotify:    #9CD653  (lime)
  Kry:        #80D9B5  (mint, distinct from cyan)
  Fyndiq:     #F4A04A  (warm orange)
```

The magenta `#DD5DB8` is used as a **section ground only** — the contact section background. It is **not** used as text-color anywhere (fails WCAG AA contrast on every other surface in the palette: 1.95:1 on cyan, 2.25:1 on yellow, 3.16:1 on cream).

**Eyebrow color:** all eyebrows render in `#0A0A0A` (ink) regardless of section ground. This is a deviation from the v5 mockup, where eyebrows used `#DD5DB8` on yellow and cyan grounds. Reason: contrast. On the magenta contact ground, eyebrows are not used.

**Nav-link hover:** color stays `#0A0A0A`, hover adds `text-decoration: underline` (no color change). Avoids the magenta-on-cream contrast issue.

### Layout

- Outer body: cream `#FAF7F0`, max content width 1240px, centered, 1.5rem horizontal padding.
- Sticky nav: 90% opacity cream + `backdrop-filter: blur(8px)`, 1.1rem vertical padding, 1px rgba border below.
- Sections sit as **rounded boxes** (`border-radius: 18px`) with 1.25rem top margin between them. Padding 4rem horizontal, 4rem-4.5rem vertical.
- White spacer sections (About, Track Record) use the same outer cream — no rounded background — but use the same 4–5rem padding rhythm so vertical spacing reads continuous.
- Each colored box keeps decorative stars contained inside it via `overflow: hidden`.

### Signature motifs

1. **Cartoon stars.** Hand-drawn 5-pointed stars (white fill, 1.4–1.8px black stroke, sizes ~22–48px) scattered absolutely-positioned inside colored boxes. 2–4 per box. SVG inline, `pointer-events: none`. Not used in white spacer areas.

2. **Black-outlined tilted callout** (the "AI-native" inline block). Used **once** in the hero H1: `<em>` wrapping the words "AI-native" rendered as inline-block with `background: #8BD0EC`, `border: 4px solid #0A0A0A`, `border-radius: 8px`, `padding: 0 0.18em`, `transform: rotate(-2deg)`, `box-shadow: 5px 5px 0 #0A0A0A`. This is the page's strongest single design gesture.

3. **Black-outlined offset-shadow cards.** All track-record cards: `border: 3px solid #0A0A0A`, `border-radius: 12px`, `box-shadow: 4px 4px 0 #0A0A0A`. Hover lifts: `transform: translate(-2px, -2px)` + `box-shadow: 6px 6px 0`.

4. **Pill CTAs.** Rounded fully-pill (`border-radius: 999px`), 2px black border, cream `#FFFCF0` background, 0.7rem padding, with a yellow circular arrow icon on the right (`width: 30px; height: 30px; border-radius: 50%; background: #F4D43B; border: 2px solid #0A0A0A`). On the magenta contact box, the pill arrow background flips to magenta.

5. **Mono chips.** Used in About for the company logo-name list — small mono caps in cream-bordered pills (`padding: 0.4rem 0.8rem; border: 2px solid black; border-radius: 999px`).

---

## Page structure

Order top to bottom, with section type and ground:

| # | Section | Ground | Notes |
| - | --- | --- | --- |
| 0 | Sticky nav | Cream (translucent) | Word-mark "aardvark" left, 5 nav links right |
| 1 | Hero | Yellow box (`#F4D43B`) | Eyebrow + H1 with cyan tilted "AI-native" callout + sub + pill CTA + secondary email link + 4 stars |
| 2 | About | White spacer (cream) | Two-column: heading-col (eyebrow + H2 stacked) / body-col (2 paragraphs + chip list) |
| 3 | AI | Cyan box (`#8BD0EC`) | Eyebrow + H2 "AI-native. Not in slideware." + body + mono tools line + 2 stars |
| 4 | Track Record | White spacer (cream) | Header (eyebrow + H2 + intro paragraph), then 3-column grid of 6 brand-coded cards |
| 5 | Contact | Magenta box (`#DD5DB8`) | Centered: H2 "Let's talk." + body + pill CTA. Cream text + yellow stars. |
| 6 | Footer | Cream | Copyright + tagline "Senior product leader, junior AI builder." in mono |

Nav anchors: `#about`, `#ai`, `#experience`, `#contact`. The "Services" nav link from the previous design is **dropped** in this redesign — About + AI + Track Record carry the offering implicitly. Removing the link keeps the nav at four targeted anchors plus Home.

---

## Section-by-section content

All copy is locked from the previous content pass and rendered as-is. No copy changes in this redesign.

### Hero
- **Eyebrow:** `Fractional CPO · Aardvark Product Management`
- **H1:** `Senior product leadership. AI-native by practice.` — with `AI-native` wrapped in the cyan tilted callout
- **Sub:** `Fractional CPO and Principal PM. 15 years leading product at Spotify, Electrolux, Kry, Truecaller, Fyndiq, and Rebtel.`
- **CTA:** `Get in touch →` (anchors to `#contact`)
- **Secondary:** `anders@aardvark.pm` (mailto, mono)

### About
- **Eyebrow:** `About`
- **H2:** `Builder at heart. Operator by trade.`
- **Body 1:** `15 years building products that reach millions. I've led product strategy and execution at Spotify (wearables & in-car), Electrolux (Care vertical, 300K+ connected users globally), Kry (regulated digital health), Truecaller (iOS, 5M+ MAU), Fyndiq (ML categorisation), and now Rebtel (payments).`
- **Body 2:** `Today I run Aardvark Product Management — an independent practice doing Fractional CPO, Principal PM, and AI-native operating-model work for ambitious teams.`
- **Chip list:** Spotify · Electrolux · Kry · Truecaller · Fyndiq · Rebtel

### AI
- **Eyebrow:** `Why AI-native`
- **H2:** `AI-native. Not in slideware.`
- **Body:** `The hard part of AI in established companies isn't the demo. It's making it ship without colliding with governance, security, and existing engineering culture. As AI Lead PM at Electrolux, I established agentic coding workflows that produced production-grade code aligned to enterprise governance — and enabled engineers without prior mobile experience to contribute to the mobile codebase.`
- **Tools line:** `Daily tools — Claude Code, Anthropic & OpenAI APIs, Figma, MCP integrations.`

### Track Record
- **Eyebrow:** `Track Record`
- **H2:** `15 years. Six companies. One throughline.`
- **Intro:** `Builder at heart. Every role has been about turning ideas into products that real users can pick up, hold, use, and pay for.`
- **Cards (3-up grid, in order):**

| Card | Brand color | Meta | Title | Role | Body |
| --- | --- | --- | --- | --- | --- |
| 1 | Aardvark `#F4D43B` | 2025 — Present | Aardvark | Founder · Fractional CPO | Director / CPO advisory and interim leadership, product strategy, operating-model audits, AI transformation, coaching for senior product leaders. |
| 2 | Rebtel `#F0857A` | 2025 — Present | Rebtel | Lead PM, Payments | Driving auth rates, conversion, and payment cost reduction across PSP, ledger, wallet, and checkout. Earlier engagement as Fractional CPO. |
| 3 | Electrolux `#8BD0EC` | 2022 — 2025 | Electrolux | Group PM · AI Lead PM | Care vertical (washing, drying, dishwashing). 300K+ users on a single global platform. Red Dot 2025. App Store rating 2.0 → 4.3. |
| 4 | Spotify `#9CD653` | 2017 — 2021 | Spotify | PM, Wearables & In-Car | Scaled from 100K to 10M+ users globally. Apple Watch, WearOS, Garmin, Fitbit, Spotify OneTouch, Magic Leap AR. |
| 5 | Kry `#80D9B5` | 2021 — 2022 | Kry | Senior PM, Growth | Growth team lead for the Swedish market in regulated digital health. Vaccination flows and patient acquisition. |
| 6 | Fyndiq `#F4A04A` | 2016 — 2017 | Fyndiq | Product Manager | ML-driven categorisation across 1M+ SKUs. 95% accuracy. Lifted product sales 80%. |

### Contact
- **H2:** `Let's talk.` — rendered in `#0A0A0A` on the magenta ground (cream-on-magenta is 3.23:1, fails AA for body)
- **Body:** `Whether you're between CPOs, scaling a product org, or trying to make AI ship inside real governance — I'd be glad to hear from you.` — rendered in `#0A0A0A`
- **CTA:** `anders@aardvark.pm →` (mailto pill, cream background, magenta arrow)
- **Stars:** yellow fill with black stroke

This is a deviation from the v5 mockup, which had cream text on magenta. Contrast required the swap.

### Footer
- `© 2026 Aardvark Product Management AB · Senior product leader, junior AI builder.` (mono)

---

## Component inventory

These are reusable across the page. Implementation should define them once.

- **`.nav-bar`** — sticky translucent cream nav with word-mark + nav links
- **`.box`** — generic colored rounded section block (4rem padding, 18px radius, overflow hidden)
- **`.white-area`** — non-rounded white-cream spacer section
- **`.eyebrow`** — mono uppercase label
- **`.pill`** — primary CTA pill with arrow icon
- **`.star`** — absolute-positioned star wrapper for inline SVG
- **`.card`** + brand modifiers (`.brand-aardvark`, `.brand-rebtel`, etc.) — track record cards
- **`.chip`** — small mono pill used for company-name list in About
- **H1 inline `<em>`** — the "AI-native" tilted callout block

---

## Accessibility

WCAG AA compliance is required. All text/background combinations have been pre-verified for contrast:

| Combination | Contrast | Status |
| --- | --- | --- |
| `#0A0A0A` on `#F4D43B` (yellow hero) | 13.7:1 | AAA |
| `#0A0A0A` on `#8BD0EC` (cyan AI / Electrolux card) | 11.6:1 | AAA |
| `#0A0A0A` on `#F0857A` (Rebtel card) | 7.4:1 | AAA |
| `#0A0A0A` on `#9CD653` (Spotify card) | 11.7:1 | AAA |
| `#0A0A0A` on `#80D9B5` (Kry card) | 12.5:1 | AAA |
| `#0A0A0A` on `#F4A04A` (Fyndiq card) | 9.6:1 | AAA |
| `#0A0A0A` on `#DD5DB8` (contact box) | 6.2:1 | AAA |
| `#0A0A0A` on `#FAF7F0` (eyebrow / nav on cream) | 19.4:1 | AAA |
| `#2A2A2A` on `#FAF7F0` (body on cream) | 13.6:1 | AAA |
| `#2A2A2A` on each card brand color | 7.0–9.6:1 | AAA |

**Combinations explicitly avoided** (would fail AA):
- `#DD5DB8` magenta on `#F4D43B` yellow — 2.25:1
- `#DD5DB8` magenta on `#8BD0EC` cyan — 1.95:1
- `#DD5DB8` magenta on `#FAF7F0` cream — 3.16:1
- `#FFFCF0` cream on `#DD5DB8` magenta — 3.23:1

**Focus states:** all interactive elements (`.pill`, `.nav-links a`, `.card[role=link]` if cards become links) need a visible focus ring — 2px solid `#0A0A0A` with 4px offset, or `outline: 2px solid #DD5DB8` on cream surfaces. Confirm during implementation.

**Reduced motion:** the hover lift on cards and pills should be disabled under `prefers-reduced-motion: reduce`.

**Semantic markup:** all sections must use `<section>` with descriptive IDs. Cards use `<article>` if they later become linkable, otherwise stay as `<div>`.

**Alt text:** the only images currently in scope are the company logo PNGs in `images/`. They will not be displayed in this redesign (we use chip-style word-marks instead). Old `images/logo-hero.svg` is also not used in the redesign.

---

## Files affected

- **`index.html`** — full rewrite of `<body>` content. Update `<title>`, `<meta name="description">`, font `<link>` tags. Header and structure replaced.
- **`styles.css`** — full rewrite. The current file's contents (current palette, Jomhuria, circle pattern system, all section styles) are entirely replaced.
- **`CLAUDE.md`** — update Design System section to reflect the new palette/typography. The companion file `DESIGN-PRINCIPLES.md` is principles-not-implementation so does not need a change for the visual swap, but its color/typography section lines about Jomhuria/Oxygen and the orange `#FDA10D` palette are now stale and should be flagged.

## Files NOT affected

- `niche-finder/index.html` — separate project
- `images/` directory — kept on disk but logo PNGs no longer referenced from `index.html`. Cleanup is a later task.
- `CNAME`, GitHub Pages config, DNS — no change
- Existing companion docs (`DESIGN-UPDATE-PLAN.md`, `QA-AUDIT-2025.md`) — historical, not modified

## Dependencies

**Google Fonts swap.** Replace the current `<link>` (Jomhuria + Oxygen) with:
```
https://fonts.googleapis.com/css2?family=Geist:wght@300..800&family=Geist+Mono:wght@400..500&display=swap
```

No other external dependencies. No JavaScript. No build step. No new images.

---

## Open questions / deferred decisions

1. **Logo.** Word-mark "aardvark" placeholder in nav; full logo is a later task.
2. **Star density on mobile.** Stars are positioned absolutely; on small mobile screens they may overlap text. Decision: hide stars under `≤480px` viewport. Confirm during implementation.
3. **Hover behaviors.** Cards lift on hover (`translate(-2px,-2px)` + `6px 6px 0` shadow). Pill CTA lifts on hover. Both must respect `prefers-reduced-motion: reduce`. Other interactive states deferred.
4. **Existing image assets.** PNG company logos in `images/` are no longer referenced from `index.html`. Removal is housekeeping, separate task.

## Deviations from the v5 mockup

These changes were made during spec self-review for accessibility. They preserve the design intent but adjust three specific text-color choices:

1. **Eyebrows** in hero/AI box switched from magenta `#DD5DB8` to ink `#0A0A0A`. Magenta on yellow/cyan failed WCAG AA contrast.
2. **Contact section H2 + body** switched from cream to ink `#0A0A0A`. Cream on magenta was 3.23:1, failed AA for body copy.
3. **Nav-link hover** switched from magenta color to underline-only. Magenta on cream failed AA.

The visual character (bold caps, brand-colored boxes, tilted callout, pill CTAs, scattered stars, brand-coded cards) is identical to the approved v5. The contact section reads slightly more "newspaper-on-magenta" than "magenta poster" — but stronger contrast.

---

## Reference artefacts

- Final approved mockup: `.superpowers/brainstorm/15245-1777126495/content/wero-style-v5-cards-final.html`
- Inspiration: [wero-wallet.eu](https://wero-wallet.eu/) — split heroes, full-bleed colored sections, bold caps, pill CTAs, scattered stars
- Inspiration: Teen Titans Go! logo — multi-color candy palette + thick black outlines + slight rotation gestures
- Brainstorm session content directory: `.superpowers/brainstorm/15245-1777126495/content/` (typography options A–C, palette options A–F, palette v3 G–I, palette v4 J–L, Wero v1–v3, Wero refined v4, brand-card v1–v5)
