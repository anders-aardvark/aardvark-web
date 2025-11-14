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

**📖 See [DESIGN-PRINCIPLES.md](DESIGN-PRINCIPLES.md) for comprehensive design guidelines.**

**Color Palette:**
- Background: `#F8FAF9` (warm light gray)
- Main text: `#1D1E18` (almost black)
- Accent: `#FDA10D` (vibrant orange/gold)
- Secondary text: `#6b7280` (gray)

**Typography:**
- Headings: `Jomhuria` (Google Fonts) - distinctive display font
- Body: `Oxygen` (Google Fonts) - clean, readable
- Hero headline: 5rem (80px), weight 400 (Jomhuria is naturally bold)
- Section headings: 3rem (48px), weight 400
- Body text: 1.25rem (20px)
- Tight letter-spacing (-0.02em to -0.03em) for headlines

**Layout Rule: 60-30-10**
- 60% Whitespace (breathing room, margins, padding)
- 30% Text Content (body copy, descriptions)
- 10% Accent Elements (CTAs, highlights)

**Key Design Principles:**
- Generous white space (6rem padding between sections)
- White content areas on warm gray background
- Orange/gold accents for CTAs and interactive elements
- Subtle borders: `1px solid rgba(0, 0, 0, 0.06)`
- Smooth transitions: 0.2s for interactive elements
- Mobile-first responsive design

## Company Logos

Located in `images/` directory. Logos display at:
- Desktop: 40px height
- Mobile: 32px height
- Default: Grayscale with 60% opacity
- Hover: Full color with 100% opacity

**Adding/updating logos:**
1. Place PNG or SVG in `images/` directory
2. Name exactly as referenced in HTML (e.g., `spotify.png`)
3. Prefer transparent backgrounds
4. High resolution (200px+ height recommended)

**Note:** Rebtel logo is intentionally upside down (their brand design choice)

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
