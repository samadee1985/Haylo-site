# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for **Haylo**, a local marketing agency serving the Sunshine Coast, QLD, Australia (withhaylo.com). No build system, no framework, no package manager — pure HTML, CSS, and JavaScript.

## Architecture

Every page is a folder containing an `index.html` file (pretty URLs). All CSS and JavaScript live inline inside each HTML file — there are no external stylesheets or JS modules.

### Page Categories

| Category | URL pattern | Example |
|---|---|---|
| Service pages | `/service-name/` | `/google-business-profile/`, `/review-generation/` |
| Industry pages | `/google-marketing-for-[industry]/` | `/google-marketing-for-cleaners/` |
| Trade pages | `/marketing-for-[trade]/` | `/marketing-for-plumbers/` |
| Location pages | `/marketing-consultant-[suburb]/` | `/marketing-consultant-noosa/` |
| Blog posts | `/blog-[slug]/` | `/blog-google-reviews/` |

### Creating New Trade Pages

Use `_TEMPLATE-new-trade-page.html` as the starting point:

1. Find & replace `[TRADE]` → trade name (e.g. `Landscapers`)
2. Find & replace `[trade]` → lowercase (e.g. `landscapers`)
3. Find & replace `[SLUG]` → URL slug (e.g. `marketing-for-landscapers`)
4. Update the 6 service tiles, 4 intro paragraphs, and "Other Trades" links
5. Save as `/marketing-for-[trade]/index.html`

### Images

Stored in `/images/` with subdirectories by content type:
- `general/` — OG share image, misc branding
- `hero/` — hero section images
- `services/` — service-specific photos
- `trades/` — trade-specific hero images (named `marketing-for-[trade]-hero.jpg`)
- `suburbs/` — suburb/location photos
- `blog/` — blog post images

## Design System

All pages share the same design tokens (defined via CSS custom properties in each file's `<style>` block):

```css
--navy: #1F2D3D      /* Primary dark */
--sky: #38BDF8       /* Accent blue */
--sky-pale: #F0F8FF
--off: #F4F8FB       /* Page background */
--muted: #6E8A9A     /* Body text */
--border: #D8E8F0
--nav-h: 62px
--pad: 5%            /* Horizontal page padding */
```

**Fonts:** Josefin Sans (headings, nav, labels — all-caps) + Manrope (body text) — loaded from Google Fonts.

**Breakpoints:** 860px (nav collapses to hamburger), 820px (2-col layouts), 480px (single column).

## Common HTML Patterns

**Nav:** Fixed top nav with hamburger drawer on mobile. Scroll adds `.scrolled` shadow class via JS.

**Reveal animations:** Elements with class `.reveal` fade up on scroll using `IntersectionObserver`. The `js-loaded` class is added to `<body>` before the observer runs (prevents flash on non-JS).

**Buttons:**
- `.btn.btn-sky` — sky blue fill (primary CTA)
- `.btn.btn-ghost-w` — ghost style on dark backgrounds

**Section layouts:**
- `.loc-split` — 2-col grid (text + stats/image)
- `.svc-tiles` — 3-col service tile grid
- `.areas-grid` — 4-col pill grid (related links)
- `.loc-stats` — 4-col dark stat bar

## SEO Conventions

Each page includes:
- `<link rel="canonical" href="https://withhaylo.com/[slug]/">`
- Open Graph tags with `/images/general/haylo-og-share.jpg` as the shared OG image
- `application/ld+json` structured data (Service + LocalBusiness schema)
- Trailing slash on all canonical/OG URLs

Business details embedded in schema: phone `0490422192`, address QLD AU.

## Deployment

Hosted on withhaylo.com, served via Cloudflare (email obfuscation script present). No deployment commands needed — changes go live when pushed/uploaded.
