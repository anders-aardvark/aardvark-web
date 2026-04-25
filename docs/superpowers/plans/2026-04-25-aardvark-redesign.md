# Aardvark Web Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the current Jomhuria/Oxygen + warm-gray/orange landing page with the Wero-inspired bold-and-playful redesign approved in `docs/superpowers/specs/2026-04-25-aardvark-redesign-design.md`.

**Architecture:** Static HTML/CSS, no build step, deployed via GitHub Pages. Two files fully rewritten (`index.html`, `styles.css`); one file lightly updated (`CLAUDE.md`). Visual verification via local HTTP server + playwright MCP screenshots.

**Tech Stack:** HTML5, CSS3, Google Fonts (Geist + Geist Mono). No JavaScript. No frameworks.

**Verification approach:** Each section task ends with a playwright screenshot and a visual comparison against the locked v5 mockup at `.superpowers/brainstorm/15245-1777126495/content/wero-style-v5-cards-final.html` (gitignored, local-only). The spec at `docs/superpowers/specs/2026-04-25-aardvark-redesign-design.md` is the source of truth for all values.

**Out of scope:** Logo redesign, niche-finder, GitHub Pages config, removal of unused PNGs in `images/`.

**Worktree note:** This plan is intended to run on `main` directly (single-owner repo, no collaborators, low blast radius). No worktree required.

---

## File structure

| File | Action | Responsibility |
| --- | --- | --- |
| `index.html` | Full rewrite | Page structure, content, font links, meta tags |
| `styles.css` | Full rewrite | All visual styling, built up section by section |
| `CLAUDE.md` | Update | Refresh Design System section to reflect new palette/typography |
| `.gitignore` | Already updated | Keeps `.superpowers/`, `.playwright-mcp/`, `.claude/`, `.DS_Store` out of git |

Tasks build `styles.css` incrementally so that each commit is a self-contained verifiable visual milestone. `index.html` is rewritten as a complete file in Task 1, then untouched by later tasks (the page comes to life section by section as CSS is added).

---

## Task 0: Start dev server and capture baseline

**Files:** none (no commit)

- [ ] **Step 1: Start a local HTTP server in the background**

```bash
python3 -m http.server 8765
```

Use `run_in_background: true` on the Bash tool. The server stays alive across tasks and is killed at the end of Task 12.

- [ ] **Step 2: Navigate to the site and take a baseline screenshot**

Use the playwright MCP tools:
1. `mcp__playwright__browser_resize` to `width: 1440, height: 900`
2. `mcp__playwright__browser_navigate` to `http://localhost:8765/index.html`
3. `mcp__playwright__browser_take_screenshot` with `filename: "baseline-before.png"`, `fullPage: true`

Expected: Old landing page renders with warm-gray/orange palette, Jomhuria headlines. Confirms server + playwright work.

---

## Task 1: HTML rewrite + CSS reset

**Files:**
- Modify: `index.html` (full rewrite)
- Modify: `styles.css` (full rewrite to base reset + body)

- [ ] **Step 1: Rewrite `index.html`**

Replace the entire contents of `/Users/anders/Projects/aardvark-web/index.html` with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Senior product leadership, AI-native by practice. Fractional CPO and Principal PM consulting through Aardvark Product Management. 15 years leading at Spotify, Electrolux, Kry, Truecaller, Fyndiq, and Rebtel.">
    <title>Aardvark Product Management — Fractional CPO and AI-native product leadership</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Geist:wght@300..800&family=Geist+Mono:wght@400..500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="nav-bar">
        <a href="/" class="nav-mark">aardvark</a>
        <nav class="nav-links">
            <a href="#about">About</a>
            <a href="#ai">AI</a>
            <a href="#experience">Track Record</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main class="container">

        <section class="box hero">
            <span class="star" style="top:14%;left:5%;"><svg width="44" height="44" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.4"/></svg></span>
            <span class="star" style="top:64%;left:48%;"><svg width="32" height="32" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.6"/></svg></span>
            <span class="star" style="top:18%;right:8%;"><svg width="36" height="36" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.6"/></svg></span>
            <span class="star" style="bottom:18%;right:6%;"><svg width="40" height="40" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.4"/></svg></span>

            <span class="eyebrow">Fractional CPO &middot; Aardvark Product Management</span>
            <h1>Senior product<br>leadership.<br><em>AI-native</em> by practice.</h1>
            <p class="sub">Fractional CPO and Principal PM. 15 years leading product at Spotify, Electrolux, Kry, Truecaller, Fyndiq, and Rebtel.</p>
            <div class="cta-row">
                <a class="pill" href="#contact">Get in touch <span class="arrow">&rarr;</span></a>
                <a class="secondary" href="mailto:anders@aardvark.pm">anders@aardvark.pm</a>
            </div>
        </section>

        <section id="about" class="white-area about-area">
            <div class="heading-col">
                <span class="eyebrow">About</span>
                <h2>Builder<br>at heart.<br>Operator<br>by trade.</h2>
            </div>
            <div class="body-col">
                <p>15 years building products that reach millions. I've led product strategy and execution at Spotify (wearables &amp; in-car), Electrolux (Care vertical, 300K+ connected users globally), Kry (regulated digital health), Truecaller (iOS, 5M+ MAU), Fyndiq (ML categorisation), and now Rebtel (payments).</p>
                <p>Today I run Aardvark Product Management — an independent practice doing Fractional CPO, Principal PM, and AI-native operating-model work for ambitious teams.</p>
                <ul class="logos">
                    <li class="chip">Spotify</li>
                    <li class="chip">Electrolux</li>
                    <li class="chip">Kry</li>
                    <li class="chip">Truecaller</li>
                    <li class="chip">Fyndiq</li>
                    <li class="chip">Rebtel</li>
                </ul>
            </div>
        </section>

        <section id="ai" class="box ai-box">
            <span class="star" style="top:18%;right:6%;"><svg width="42" height="42" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.4"/></svg></span>
            <span class="star" style="bottom:14%;left:8%;"><svg width="32" height="32" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#FFFCF0" stroke="#0A0A0A" stroke-width="1.6"/></svg></span>

            <span class="eyebrow">Why AI-native</span>
            <h2>AI-native.<br>Not in slideware.</h2>
            <p>The hard part of AI in established companies isn't the demo. It's making it ship without colliding with governance, security, and existing engineering culture. As AI Lead PM at Electrolux, I established agentic coding workflows that produced production-grade code aligned to enterprise governance — and enabled engineers without prior mobile experience to contribute to the mobile codebase.</p>
            <p class="tools">Daily tools — Claude Code, Anthropic &amp; OpenAI APIs, Figma, MCP integrations.</p>
        </section>

        <section id="experience" class="white-area track-area">
            <div class="head">
                <div>
                    <span class="eyebrow">Track Record</span>
                    <h2>15 years.<br>Six companies.<br>One throughline.</h2>
                </div>
                <p class="intro">Builder at heart. Every role has been about turning ideas into products that real users can pick up, hold, use, and pay for.</p>
            </div>
            <div class="cards">
                <article class="card brand-aardvark">
                    <div class="meta">2025 — Present</div>
                    <h3 class="title">Aardvark</h3>
                    <p class="role">Founder &middot; Fractional CPO</p>
                    <p class="body">Director / CPO advisory and interim leadership, product strategy, operating-model audits, AI transformation, coaching for senior product leaders.</p>
                </article>
                <article class="card brand-rebtel">
                    <div class="meta">2025 — Present</div>
                    <h3 class="title">Rebtel</h3>
                    <p class="role">Lead PM, Payments</p>
                    <p class="body">Driving auth rates, conversion, and payment cost reduction across PSP, ledger, wallet, and checkout. Earlier engagement as Fractional CPO.</p>
                </article>
                <article class="card brand-electrolux">
                    <div class="meta">2022 — 2025</div>
                    <h3 class="title">Electrolux</h3>
                    <p class="role">Group PM &middot; AI Lead PM</p>
                    <p class="body">Care vertical (washing, drying, dishwashing). 300K+ users on a single global platform. Red Dot 2025. App Store rating 2.0 &rarr; 4.3.</p>
                </article>
                <article class="card brand-spotify">
                    <div class="meta">2017 — 2021</div>
                    <h3 class="title">Spotify</h3>
                    <p class="role">PM, Wearables &amp; In-Car</p>
                    <p class="body">Scaled from 100K to 10M+ users globally. Apple Watch, WearOS, Garmin, Fitbit, Spotify OneTouch, Magic Leap AR.</p>
                </article>
                <article class="card brand-kry">
                    <div class="meta">2021 — 2022</div>
                    <h3 class="title">Kry</h3>
                    <p class="role">Senior PM, Growth</p>
                    <p class="body">Growth team lead for the Swedish market in regulated digital health. Vaccination flows and patient acquisition.</p>
                </article>
                <article class="card brand-fyndiq">
                    <div class="meta">2016 — 2017</div>
                    <h3 class="title">Fyndiq</h3>
                    <p class="role">Product Manager</p>
                    <p class="body">ML-driven categorisation across 1M+ SKUs. 95% accuracy. Lifted product sales 80%.</p>
                </article>
            </div>
        </section>

        <section id="contact" class="box contact-box">
            <span class="star" style="top:14%;left:8%;"><svg width="38" height="38" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#F4D43B" stroke="#0A0A0A" stroke-width="1.6"/></svg></span>
            <span class="star" style="top:24%;right:10%;"><svg width="32" height="32" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 1.5 L14.7 8.7 L22.5 9.2 L16.4 14.1 L18.4 21.5 L12 17.3 L5.6 21.5 L7.6 14.1 L1.5 9.2 L9.3 8.7 Z" fill="#F4D43B" stroke="#0A0A0A" stroke-width="1.6"/></svg></span>

            <h2>Let's talk.</h2>
            <p>Whether you're between CPOs, scaling a product org, or trying to make AI ship inside real governance — I'd be glad to hear from you.</p>
            <a class="pill" href="mailto:anders@aardvark.pm">anders@aardvark.pm <span class="arrow">&rarr;</span></a>
        </section>

    </main>

    <footer>
        <p>&copy; 2026 Aardvark Product Management AB</p>
        <p class="footer-tagline">Senior product leader, junior AI builder.</p>
    </footer>
</body>
</html>
```

- [ ] **Step 2: Replace `styles.css` with reset + base**

Replace the entire contents of `/Users/anders/Projects/aardvark-web/styles.css` with:

```css
/*
 * Aardvark Product Management — landing page styles
 * Visual system: Wero-inspired bold-playful, Geist + Geist Mono,
 * cream chrome with brand-colored boxes.
 * See docs/superpowers/specs/2026-04-25-aardvark-redesign-design.md
 */

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html, body {
    background: #FAF7F0;
    color: #0A0A0A;
}

body {
    font-family: 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    line-height: 1.55;
    font-size: 16px;
    padding-bottom: 4rem;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

img { max-width: 100%; height: auto; display: block; }
ul { list-style: none; }
a { color: inherit; text-decoration: none; }

.container {
    max-width: 1240px;
    margin: 0 auto;
    padding: 0 1.5rem;
}

/* Generic colored "box" sections — yellow hero, cyan AI, magenta contact */
.box {
    border-radius: 18px;
    margin-top: 1.25rem;
    padding: 4rem 4rem 4.5rem;
    position: relative;
    overflow: hidden;
}

/* Generic white-spacer sections — about, track record */
.white-area {
    margin-top: 1.25rem;
    padding: 4rem 4rem;
}

/* Star decoration helper */
.star {
    position: absolute;
    pointer-events: none;
    z-index: 1;
}
.star svg { display: block; }

/* All section content sits above stars via z-index */
.box > *:not(.star) {
    position: relative;
    z-index: 2;
}
```

- [ ] **Step 3: Verify in browser**

Refresh `http://localhost:8765/index.html` and screenshot via playwright. Expected: cream background, content visible (unstyled headings/paragraphs/lists), Geist font loaded, no errors in console (except the harmless favicon 404).

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Redesign: HTML scaffold and CSS base"
```

---

## Task 2: Sticky nav

**Files:**
- Modify: `styles.css` (append nav styles)

- [ ] **Step 1: Append nav styles to `styles.css`**

Append to the end of `/Users/anders/Projects/aardvark-web/styles.css`:

```css
/* === STICKY NAV === */
.nav-bar {
    position: sticky;
    top: 0;
    z-index: 10;
    background: rgba(250, 247, 240, 0.92);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    padding: 1.1rem 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}

.nav-mark {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 1.125rem;
    letter-spacing: -0.04em;
    color: #0A0A0A;
}

.nav-links {
    display: flex;
    gap: 2rem;
    font-family: 'Geist', sans-serif;
    font-size: 0.875rem;
}

.nav-links a {
    color: #2A2A2A;
    text-decoration: none;
    transition: text-decoration 0.15s ease;
}

.nav-links a:hover,
.nav-links a:focus-visible {
    text-decoration: underline;
    text-underline-offset: 4px;
}

/* Universal focus state for keyboard accessibility */
:focus-visible {
    outline: 2px solid #0A0A0A;
    outline-offset: 3px;
    border-radius: 2px;
}
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: sticky nav at top, "aardvark" word-mark left, four links right, faint border below. Hover any link → underline appears (no color change). Tab through → focus rings appear.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: sticky nav with cream chrome"
```

---

## Task 3: Hero section

**Files:**
- Modify: `styles.css` (append hero, eyebrow, pill, secondary styles)

- [ ] **Step 1: Append hero + reusable component styles**

Append to `/Users/anders/Projects/aardvark-web/styles.css`:

```css
/* === SHARED COMPONENTS === */

/* Eyebrow — small mono label */
.eyebrow {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.8125rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.18em;
    color: #0A0A0A;
    margin-bottom: 1.5rem;
    display: block;
}

/* Pill CTA — primary button with arrow icon */
.pill {
    display: inline-flex;
    align-items: center;
    gap: 0.6rem;
    padding: 0.7rem 0.7rem 0.7rem 1.25rem;
    border-radius: 999px;
    border: 2px solid #0A0A0A;
    background: #FFFCF0;
    color: #0A0A0A;
    font-family: 'Geist', sans-serif;
    font-size: 0.9375rem;
    font-weight: 500;
    text-decoration: none;
    transition: transform 0.12s ease, box-shadow 0.12s ease;
    box-shadow: 0 0 0 0 #0A0A0A;
}
.pill:hover {
    transform: translateY(-1px);
    box-shadow: 3px 3px 0 #0A0A0A;
}
.pill .arrow {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background: #F4D43B;
    border: 2px solid #0A0A0A;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 0.875rem;
    line-height: 1;
}

/* Secondary text-link beside the pill */
.secondary {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.875rem;
    color: #0A0A0A;
    text-decoration: none;
    border-bottom: 2px solid #0A0A0A;
    padding-bottom: 1px;
    transition: border-bottom-color 0.15s ease;
}
.secondary:hover {
    border-bottom-color: transparent;
}

/* === HERO === */
.hero {
    background: #F4D43B;
    color: #0A0A0A;
}

.hero h1 {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 5.5rem;
    line-height: 0.94;
    letter-spacing: -0.05em;
    text-transform: uppercase;
    max-width: 1100px;
    margin-bottom: 1.75rem;
}

/* The signature tilted "AI-native" callout block */
.hero h1 em {
    font-style: normal;
    background: #8BD0EC;
    border: 4px solid #0A0A0A;
    border-radius: 8px;
    padding: 0 0.18em;
    display: inline-block;
    transform: rotate(-2deg);
    box-shadow: 5px 5px 0 #0A0A0A;
}

.hero p.sub {
    font-family: 'Geist', sans-serif;
    font-size: 1.1875rem;
    line-height: 1.5;
    color: #0A0A0A;
    max-width: 620px;
    margin-bottom: 2.5rem;
}

.hero .cta-row {
    display: flex;
    align-items: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: yellow hero box appears below nav, with eyebrow + giant uppercase headline + tilted cyan "AI-native" callout block + sub paragraph + pill CTA + secondary email link. Stars scattered. Hover the pill → it lifts and gains an offset shadow.

Cross-check against `.superpowers/brainstorm/15245-1777126495/content/wero-style-v5-cards-final.html` for visual fidelity.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: hero box (yellow ground, tilted callout, pill CTA)"
```

---

## Task 4: About section

**Files:**
- Modify: `styles.css` (append about-area styles)

- [ ] **Step 1: Append about-area styles**

```css
/* === ABOUT === */
.about-area {
    display: grid;
    grid-template-columns: 1fr 1.4fr;
    gap: 3.5rem;
    padding: 5rem 4rem;
}

.about-area h2 {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 3.5rem;
    line-height: 0.94;
    letter-spacing: -0.045em;
    text-transform: uppercase;
    color: #0A0A0A;
}

.about-area .body-col p {
    font-family: 'Geist', sans-serif;
    font-size: 1.125rem;
    line-height: 1.6;
    color: #2A2A2A;
    margin-bottom: 1.25rem;
}

.about-area .logos {
    display: flex;
    gap: 0.6rem;
    flex-wrap: wrap;
    margin-top: 1.5rem;
}

.about-area .chip {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.75rem;
    padding: 0.4rem 0.8rem;
    border: 2px solid #0A0A0A;
    border-radius: 999px;
    background: #FFFCF0;
    color: #0A0A0A;
}
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: two-column About area below hero. Left col: small "ABOUT" eyebrow + bold uppercase H2 stacked vertically. Right col: two paragraphs of body copy + a row of mono-styled chip pills with company names.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: About section (two-column with company chips)"
```

---

## Task 5: AI section

**Files:**
- Modify: `styles.css` (append ai-box styles)

- [ ] **Step 1: Append AI-box styles**

```css
/* === AI BOX === */
.ai-box {
    background: #8BD0EC;
    color: #0A0A0A;
}

.ai-box h2 {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 4rem;
    line-height: 0.94;
    letter-spacing: -0.045em;
    text-transform: uppercase;
    max-width: 900px;
    margin-bottom: 2rem;
}

.ai-box p {
    font-family: 'Geist', sans-serif;
    font-size: 1.125rem;
    line-height: 1.55;
    color: #0A0A0A;
    max-width: 720px;
}

.ai-box p.tools {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.875rem;
    margin-top: 2rem;
    opacity: 0.8;
}
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: cyan box below About. "WHY AI-NATIVE" eyebrow + uppercase "AI-NATIVE. NOT IN SLIDEWARE." + body paragraph + small italic-feeling mono "Daily tools — ..." line. Two stars scattered.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: AI section (cyan box with tools mono line)"
```

---

## Task 6: Track Record + brand-coded cards

**Files:**
- Modify: `styles.css` (append track-area + card styles)

- [ ] **Step 1: Append track-area + card styles**

```css
/* === TRACK RECORD === */
.track-area {
    padding: 5rem 4rem 2rem;
}

.track-area .head {
    margin-bottom: 3rem;
    display: flex;
    align-items: end;
    justify-content: space-between;
    gap: 2rem;
}

.track-area h2 {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 3.5rem;
    line-height: 0.94;
    letter-spacing: -0.045em;
    text-transform: uppercase;
    color: #0A0A0A;
    max-width: 700px;
}

.track-area p.intro {
    font-family: 'Geist', sans-serif;
    font-size: 1.0625rem;
    line-height: 1.55;
    color: #2A2A2A;
    max-width: 360px;
}

.track-area .cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.25rem;
}

/* Track card base */
.track-area .card {
    border: 3px solid #0A0A0A;
    border-radius: 12px;
    padding: 1.5rem 1.5rem 1.75rem;
    box-shadow: 4px 4px 0 #0A0A0A;
    color: #0A0A0A;
    transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.track-area .card:hover {
    transform: translate(-2px, -2px);
    box-shadow: 6px 6px 0 #0A0A0A;
}

.track-area .card .meta {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    color: #0A0A0A;
    margin-bottom: 0.5rem;
}

.track-area .card .title {
    font-family: 'Geist', sans-serif;
    font-weight: 700;
    font-size: 1.5rem;
    text-transform: uppercase;
    letter-spacing: -0.025em;
    line-height: 1;
    margin-bottom: 0.4rem;
    color: #0A0A0A;
}

.track-area .card .role {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.75rem;
    margin-bottom: 0.85rem;
    color: #2A2A2A;
}

.track-area .card .body {
    font-family: 'Geist', sans-serif;
    font-size: 0.9375rem;
    line-height: 1.5;
    color: #2A2A2A;
}

/* Brand-coded card backgrounds (all light, all readable in black text) */
.card.brand-aardvark   { background: #F4D43B; }
.card.brand-rebtel     { background: #F0857A; }
.card.brand-electrolux { background: #8BD0EC; }
.card.brand-spotify    { background: #9CD653; }
.card.brand-kry        { background: #80D9B5; }
.card.brand-fyndiq     { background: #F4A04A; }
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: white-area Track Record section. Header row at top (eyebrow + uppercase 3-line H2 + intro paragraph on the right). Below: 3-column grid of 6 cards, each in its brand color. All text black except role/body in dark gray. Hover any card → it lifts up-left with bigger shadow.

Confirm the 6 brand colors visually match the spec hex values.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: Track Record with brand-color-coded cards"
```

---

## Task 7: Contact section + footer

**Files:**
- Modify: `styles.css` (append contact-box + footer styles)

- [ ] **Step 1: Append contact + footer styles**

```css
/* === CONTACT === */
.contact-box {
    background: #DD5DB8;
    color: #0A0A0A;
    text-align: center;
    padding: 5rem 4rem 5.5rem;
}

.contact-box h2 {
    font-family: 'Geist', sans-serif;
    font-weight: 800;
    font-size: 5rem;
    line-height: 0.94;
    letter-spacing: -0.05em;
    text-transform: uppercase;
    margin-bottom: 1.25rem;
    color: #0A0A0A;
}

.contact-box p {
    font-family: 'Geist', sans-serif;
    font-size: 1.125rem;
    max-width: 580px;
    margin: 0 auto 2rem;
    line-height: 1.5;
    color: #0A0A0A;
}

.contact-box .pill {
    background: #FFFCF0;
}
.contact-box .pill .arrow {
    background: #DD5DB8;
}

/* === FOOTER === */
footer {
    text-align: center;
    padding: 2.5rem 2rem 1rem;
    margin-top: 1.25rem;
}

footer p {
    font-family: 'Geist Mono', ui-monospace, monospace;
    font-size: 0.75rem;
    color: #555;
}

footer .footer-tagline {
    margin-top: 0.5rem;
    font-style: italic;
}
```

- [ ] **Step 2: Verify**

Refresh + screenshot. Expected: magenta box below Track Record with centered black "LET'S TALK." + body + cream pill (with magenta arrow circle). Yellow stars in background. Below: small mono footer copyright + tagline on cream.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: contact box and footer"
```

---

## Task 8: Responsive + reduced-motion

**Files:**
- Modify: `styles.css` (append @media queries)

- [ ] **Step 1: Append responsive + reduced-motion**

```css
/* === RESPONSIVE === */
@media (max-width: 900px) {
    .container { padding: 0 0.75rem; }
    .box { padding: 2.5rem 1.5rem 3rem; }
    .white-area { padding: 2.5rem 1.5rem; }

    .nav-bar { padding: 0.85rem 1rem; }
    .nav-links { gap: 1.25rem; font-size: 0.8125rem; }

    .hero h1 { font-size: 2.75rem; }
    .hero h1 em { box-shadow: 3px 3px 0 #0A0A0A; }
    .hero p.sub { font-size: 1rem; }

    .about-area { grid-template-columns: 1fr; gap: 1.5rem; padding: 2.5rem 1.5rem; }
    .about-area h2 { font-size: 2.25rem; }

    .ai-box h2 { font-size: 2.25rem; }
    .ai-box p { font-size: 1rem; }

    .track-area { padding: 2.5rem 1.5rem; }
    .track-area .head { flex-direction: column; align-items: flex-start; }
    .track-area h2 { font-size: 2.25rem; }
    .track-area .cards { grid-template-columns: 1fr; }

    .contact-box h2 { font-size: 2.75rem; }
    .contact-box p { font-size: 1rem; }
}

@media (max-width: 480px) {
    /* Hide stars on smallest screens — they overlap text */
    .star { display: none; }

    .hero h1 { font-size: 2.25rem; }
    .contact-box h2 { font-size: 2.25rem; }
}

/* === REDUCED MOTION === */
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        transition-duration: 0.01ms !important;
        animation-duration: 0.01ms !important;
    }
    .pill:hover,
    .track-area .card:hover {
        transform: none;
    }
}
```

- [ ] **Step 2: Verify desktop unchanged + mobile breakpoints work**

Run two playwright resizes and screenshots:
1. `mcp__playwright__browser_resize` to `width: 768, height: 1024` then refresh + screenshot. Expected: single-column grid, smaller headlines, stars still visible.
2. `mcp__playwright__browser_resize` to `width: 400, height: 800` then refresh + screenshot. Expected: even smaller headlines, **stars hidden**, all content readable, no horizontal scroll.

Then resize back to desktop: `width: 1440, height: 900`. Verify desktop unchanged.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Redesign: responsive breakpoints and reduced-motion"
```

---

## Task 9: Update CLAUDE.md design system section

**Files:**
- Modify: `CLAUDE.md` (replace Design System section)

- [ ] **Step 1: Read current CLAUDE.md to find the Design System section**

Use the Read tool on `/Users/anders/Projects/aardvark-web/CLAUDE.md`. Locate the section starting `## Design System` (likely around lines 70–110, but verify) and the "Company Logos" / "Content Strategy" sections that follow it.

- [ ] **Step 2: Replace the Design System section**

Use the Edit tool. Replace the existing `## Design System` block (and its subsections covering Color Palette, Typography, Layout Rule, Key Design Principles) with:

```markdown
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
```

Then locate the "Company Logos" subsection. Update it to reflect the new approach: company names appear as text chips in About, not as logo PNGs. The PNGs in `images/` are no longer referenced and can be cleaned up later.

Replace the Company Logos section content with:

```markdown
## Company logos

Company names are rendered as **mono-styled text chips** in the About section (not as PNGs). The PNG files in `images/` are no longer referenced from `index.html` and can be cleaned up in a separate housekeeping pass. The hero/nav SVG logos (`logo-hero.svg`, `logo-nav.svg`) are also unused; a real logo design is a separate later project.
```

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md
git commit -m "Update CLAUDE.md design system to reflect new visual system"
```

---

## Task 10: Final visual + accessibility verification

**Files:** none (verification + possible final commit)

- [ ] **Step 1: Capture final desktop screenshot**

Resize playwright to `width: 1440, height: 900`, refresh, take a `fullPage: true` screenshot named `final-desktop.png`.

- [ ] **Step 2: Compare against the v5 mockup**

Open the mockup in playwright at `file://...` won't work (file:// blocked). Instead, while the dev server is running, navigate to `http://localhost:8765/.superpowers/brainstorm/15245-1777126495/content/wero-style-v5-cards-final.html` (path may vary; check `.superpowers/brainstorm/` directory).

Take a screenshot. Compare side by side. Differences expected:
- Eyebrow color is **black** in the implementation, **magenta** in the v5 mockup (intentional accessibility deviation per spec)
- Contact section text is **black** in the implementation, **cream** in the v5 (intentional accessibility deviation per spec)
- Nav links don't change color on hover (only underline) — different from v5 magenta hover

If any other differences appear, investigate and fix. Otherwise proceed.

- [ ] **Step 3: Keyboard navigation + focus check**

In playwright, use `mcp__playwright__browser_press_key` to press Tab repeatedly. Verify a visible 2px black focus ring appears around each interactive element (`.nav-mark`, `.nav-links a`, `.pill`, `.secondary`).

- [ ] **Step 4: Spot-check contrast**

Visually verify:
- Card meta text ("2025 — Present") is clearly readable on every brand color
- Body copy in About is readable on cream
- Contact body is readable on magenta

If any contrast looks weaker than expected, refer to the spec's contrast table and verify the implementation hex values match exactly.

- [ ] **Step 5: Cleanup — kill the dev server**

```bash
lsof -ti:8765 | xargs -r kill
```

- [ ] **Step 6: Commit any final tweaks (skip if none)**

If steps 2–4 surfaced any small fixes, commit them as a final polish commit. Otherwise skip.

```bash
# Only if there were tweaks:
git add styles.css
git commit -m "Redesign: final polish and accessibility tweaks"
```

---

## Task 11: Push and close out

**Files:** none

- [ ] **Step 1: Review the commit log**

```bash
git log --oneline main..HEAD
```

Expected: ~9 commits, one per task that produced changes (Tasks 1–9, Task 10 if tweaks were made).

- [ ] **Step 2: Push to GitHub Pages**

```bash
git push
```

GitHub Pages will auto-rebuild within 1–3 minutes.

- [ ] **Step 3: Verify deployment**

```bash
gh run list --limit 3
```

Expected: latest deploy is in_progress or completed.

After ~2 minutes, fetch `https://aardvark.pm` in playwright and screenshot. Compare to the local desktop screenshot. They should match.

- [ ] **Step 4: Tell the user the work is done**

Report: commit count, deploy status, link to live site, list of any items still to address (e.g., logo design, PNG cleanup) referenced from the spec's Open Questions section.

---

## Self-review

After completing the plan above, the implementer should verify each spec section is covered:

| Spec section | Covered by |
| --- | --- |
| Goals (senior-credible, legibility, content-as-artifact) | Visual verification at end of each section task |
| Non-goals (logo, niche-finder, deploy config) | Out of scope, untouched |
| Visual system → Typography (Geist + Geist Mono) | Task 1 step 1 (font link), Task 2+ (font-family rules) |
| Visual system → Palette | Tasks 3–7 (each section uses its assigned hex value) |
| Visual system → Layout (cream chrome, boxes, white-area) | Task 1 step 2 (base box / white-area helpers) |
| Signature motifs (stars, callout, cards, pills, chips) | Tasks 3 (callout, pill, stars), 4 (chips), 6 (cards) |
| Page structure (nav → hero → about → AI → track → contact → footer) | Task 1 step 1 (HTML), Tasks 2–7 (styling) |
| Section content (locked copy) | Task 1 step 1 (literal copy in HTML) |
| Component inventory (.nav-bar, .box, .white-area, .eyebrow, .pill, .star, .card, .chip) | Tasks 1–7 (each component defined once) |
| Accessibility → contrast | Task 1 step 1 (color choices already verified in spec); Task 10 step 4 (spot-check) |
| Accessibility → focus states | Task 2 step 1 (`:focus-visible` rule) |
| Accessibility → reduced motion | Task 8 step 1 (`prefers-reduced-motion` rule) |
| Accessibility → semantic markup | Task 1 step 1 (`<section>`, `<article>`, `<nav>`, `<header>`, `<footer>` used) |
| Files affected | All three files modified across plan |
| Files NOT affected | niche-finder, images/, CNAME left untouched throughout |
| Dependencies (Geist Google Fonts) | Task 1 step 1 |
| Deviations from v5 mockup (eyebrow color, contact text, nav hover) | Task 2 (nav hover), Task 3 (eyebrow color in `.eyebrow` base), Task 7 (contact text); also called out in Task 10 step 2 |

All spec requirements are mapped to tasks. No "TBD" or "implement later" placeholders. Type/property names are consistent across tasks.
