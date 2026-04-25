# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal consultancy website for Aardvark Product Management AB - a product management consultancy showcasing 15 years of experience at companies like Spotify, Electrolux, Kry, Truecaller, and Fyndiq.

**Live site:** https://aardvark.pm (also accessible at https://anders-aardvark.github.io/aardvark-web/)

## Scope

"The webpage" / "this project" refers to the landing page (`index.html`, `styles.css`, `images/`, `CNAME`) and any other pages that may be added at the repo root. The `niche-finder/` subdirectory is a separate tool managed in another project — do not modify it as part of landing-page work, and exclude it when reasoning about the site (architecture, design system, deployment behavior, etc.).

## Tech Stack

- Pure HTML/CSS - no build tools, frameworks, or JavaScript
- Hosted on GitHub Pages
- Custom domain: aardvark.pm (managed via Gandi DNS)

## Local Development

**View the site locally:**
```bash
# Simply open the file in a browser
open index.html

# Or navigate to the directory
cd /Users/anders/Projects/aardvark-web
open index.html
```

**Make changes:**
1. Edit `index.html` or `styles.css` directly
2. Refresh browser to see changes (no build step needed)

## Deployment

**Push to GitHub Pages:**
```bash
git add .
git commit -m "Your commit message"
git push
```

GitHub Pages automatically rebuilds and deploys within 1-3 minutes. Check deployment status:
```bash
gh run list --limit 5
```

**Force browser cache refresh after deployment:**
- Mac: `Cmd + Shift + R`
- Or open in incognito/private window

## Companion docs

- `DESIGN-PRINCIPLES.md` — full design system reference (read before non-trivial visual changes).
- `DESIGN-UPDATE-PLAN.md` — in-flight redesign plan; consult if asked about pending visual direction.
- `QA-AUDIT-2025.md` — accessibility/QA audit findings; check before claiming a fix is complete in audited areas.

## Design System

**📖 See [DESIGN-PRINCIPLES.md](DESIGN-PRINCIPLES.md) for general principles. The visual system below is the active implementation; principles in that doc are the broader policy.**

**Locked design spec:** `docs/superpowers/specs/2026-04-25-aardvark-redesign-design.md`

**Color Palette:**
- Page chrome: `#FAF7F0` (cream)
- Cream card / pill: `#FFFCF0`
- Ink (primary text): `#0A0A0A`
- Secondary ink (body, role): `#2A2A2A`
- Hero / brand yellow: `#F4D43B`
- AI box / Electrolux cyan: `#8BD0EC`
- Contact / magenta accent: `#DD5DB8` (ground only, never as text on light surfaces)
- Brand cards: Rebtel `#F0857A`, Spotify `#9CD653`, Kry `#80D9B5`, Fyndiq `#F4A04A`

**Typography:**
- Display & body: `Geist` (Google Fonts) — weights 300–800
- Mono accents: `Geist Mono` — weights 400–500
- Headlines: Geist 800, uppercase, line-height 0.94, letter-spacing -0.045em to -0.05em
- Hero H1: 5.5rem; section H2s: 3.5–5rem
- Body: 1.125rem; sub/lead: 1.1875rem
- Eyebrow / meta: 0.7–0.8125rem mono uppercase

**Layout:**
- Cream chrome with sticky translucent nav
- Sections sit as **rounded boxes** (`border-radius: 18px`) when colored; white-area sections use the cream chrome directly
- 1.25rem vertical gap between sections
- Max content width 1240px

**Key gestures:**
- Tilted black-outlined inline callout (the cyan "AI-native" block in the H1) — used once
- Cartoon stars scattered in colored boxes — never in white-area sections
- Pill CTA: cream background, 2px black border, yellow arrow icon
- Black-outlined cards with offset shadow (3px border, 4px 4px 0 shadow)
- Hover: cards and pill lift up-left + bigger shadow (disabled under prefers-reduced-motion)

## Company logos

Company names are rendered as **mono-styled text chips** in the About section (not as PNGs). The PNG files in `images/` are no longer referenced from `index.html` and can be cleaned up in a separate housekeeping pass. The hero/nav SVG logos (`logo-hero.svg`, `logo-nav.svg`) are also unused; a real logo design is a separate later project.

## Content Strategy

Headline positioning: *"Senior product leadership. AI-native by practice."* Anders operates as Fractional CPO and Principal PM through Aardvark Product Management.

Track record proof points used on the page:
- Aardvark (2025–): Fractional CPO advisory, AI transformation, operating-model audits
- Rebtel (2025–): Lead PM, payments
- Electrolux (2022–2025): Group PM + AI Lead PM, Care vertical 300K+ users, Red Dot 2025, App Store rating 2.0 → 4.3
- Spotify (2017–2021): Wearables vertical scaled 100K → 10M+
- Kry (2021–2022): Senior PM, growth, regulated digital health
- Fyndiq (2016–2017): ML categorisation 95% accuracy, 80% sales lift

**Avoid:** Generic consulting speak. Always use concrete examples and measurable outcomes.

## Custom Domain

`aardvark.pm` is registered at Gandi. DNS A records and the `www` CNAME point at GitHub Pages; HTTPS is enforced in the Pages settings. The `CNAME` file in the repo root must continue to contain `aardvark.pm` — removing it will break the custom domain on next deploy.

Sanity-check the domain is still live:
```bash
dig aardvark.pm +short  # Should return GitHub Pages IPs (185.199.108–111.153)
```

## Responsive breakpoints

Defined in `styles.css`: `@media (max-width: 900px)` for tablet/mobile (single-column grids, smaller headlines), `@media (max-width: 480px)` for small mobile (hides decorative stars, further headline reduction). Max content width is 1240px. A `prefers-reduced-motion: reduce` block disables card and pill hover transforms.
