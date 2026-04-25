# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal consultancy website for Aardvark Product Management AB - a product management consultancy showcasing 15 years of experience at companies like Spotify, Electrolux, Kry, Truecaller, and Fyndiq.

**Live site:** https://aardvark.pm (also accessible at https://anders-aardvark.github.io/aardvark-web/)

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
cd /Users/anders/projects/aardvark-web
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

## Project Structure

```
aardvark-web/
├── index.html               # Main landing page
├── styles.css               # All styling
├── CLAUDE.md                # Project documentation for Claude Code
├── DESIGN-PRINCIPLES.md     # Comprehensive design guidelines
├── images/                  # Logos and images
│   ├── logo-nav.svg         # Navigation logo (icon only)
│   ├── logo-hero.svg        # Hero logo (full with text)
│   ├── spotify.png          # Company logos
│   ├── electrolux.png
│   ├── kry.svg
│   ├── truecaller.png
│   ├── fyndiq.png
│   └── rebtel.png
├── CNAME                    # Custom domain configuration (aardvark.pm)
└── README.md                # Project documentation
```

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

All copy is backed by real achievements and metrics:
- Spotify: Scaled wearables from 100K to 10M+ users
- Electrolux: Multi-year digital strategy, global platform launches
- Fyndiq: ML solutions increasing sales by 80%
- Specific product launches: Apple Watch, WearOS, Garmin, etc.

**USP:** "From 100K to 10M+ Users" - highlighting scale achievement

**Avoid:** Generic consulting speak. Always use concrete examples and measurable outcomes.

## Custom Domain Setup

**Domain:** aardvark.pm (managed at Gandi)

**DNS Configuration:**
- 4 A records pointing to GitHub Pages:
  - 185.199.108.153
  - 185.199.109.153
  - 185.199.110.153
  - 185.199.111.153
- CNAME: www → anders-aardvark.github.io

**GitHub Pages Settings:**
- Source: Deploy from branch `main` / (root)
- Custom domain: aardvark.pm
- Enforce HTTPS: ✓ (enabled)

## Common Tasks

**Update content:**
Edit `index.html` directly. Main sections:
- Hero: Headline and tagline
- About: Career summary
- Services: 4 service cards
- Experience: 5 company highlights + metrics
- Contact: Email and CTA

**Update styling:**
Edit `styles.css`. All styles are in one file, organized by section.

**Add a new company logo:**
1. Add image to `images/` directory
2. Update HTML in About section's `.companies` div
3. Follow exact naming convention

**Check if site is live:**
```bash
dig aardvark.pm +short  # Should show GitHub Pages IPs
```

## Git Workflow

**Current setup:**
- Remote: https://github.com/anders-aardvark/aardvark-web.git
- Branch: main
- Authentication: GitHub CLI (gh)

**Standard workflow:**
```bash
# Make changes
git add .
git commit -m "Descriptive commit message"
git push

# Check deployment
gh run list --limit 5
```

**Note:** Git config shows committer as "Anders <anders@mac.lan>". This is fine for personal projects.

## Responsive Breakpoints

- Desktop: Default (1280px max-width)
- Tablet: 1024px and below
- Mobile: 768px and below
- Small mobile: 480px and below

All sections are fully responsive with appropriate font size adjustments.

## Browser Compatibility

Works in all modern browsers:
- Chrome/Edge
- Safari
- Firefox
- Mobile browsers (iOS Safari, Chrome Mobile)

No JavaScript means excellent compatibility and performance.
