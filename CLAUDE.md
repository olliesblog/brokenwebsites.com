# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

BrokenWebsites.com is the **US/Global version** of the marketing website for a web design service that finds broken websites and offers to redesign them for $500 USD. The business model is unique: the designer creates a spec design first, shows it to the client, and only charges if they want it built.

**This is the international version.** The Australian version is at brokenwebsites.com.au.

**Business Details:**
- Business Name: Underdog Digital
- Stripe Payment Link: `STRIPE_USD_LINK_TODO` (needs to be created)
- Pricing: $500 USD
- Hosting: $29/month (2-year commitment gets free redesign)

## Architecture

This is a **static HTML website** with no build process, no package.json, and no framework dependencies. It uses:

- **HTML**: Vanilla HTML with inline critical CSS and deferred external resources
- **CSS Framework**: Tailwind CSS loaded via CDN
- **Fonts**: Bebas Neue (headings) and Inter (body text) loaded from Google Fonts
- **JavaScript**: Alpine.js for interactive components (mobile menu, FAQ accordions, lightbox)
- **Hosting**: Cloudflare Pages (configured via `_redirects` and `_headers`)

### File Structure

```
/
├── index.html                 # Main landing page (highly optimized for Core Web Vitals)
├── 404.html                   # Custom 404 error page
├── _redirects                 # Cloudflare Pages URL rewriting
├── _headers                   # Cloudflare Pages security headers
├── site/
│   ├── example.html          # Template for client design previews
│   └── [client].html         # Client-specific preview pages
├── example/                   # Design preview screenshots (PNG files)
└── images/                    # Site images
```

## Regional Differences from .com.au

This site is adapted for international audiences:
- Currency: USD instead of AUD
- Language: Neutral English (no Australian slang like "cooked", "mate", etc.)
- No ABN or Melbourne references
- Structured data targets worldwide audience
- hreflang tags link to Australian version

**Note on hreflang:** The hreflang tags are for SEO only — they tell search engines which version to show in results for different regions. They do NOT redirect users. To redirect Australian visitors to .com.au, configure geo-redirect rules in Cloudflare dashboard.

## Design System

### Color Palette
- **Charcoal**: `#171717` - Background
- **Glitch Green**: `#A7F3D0` - Primary accent (links, CTAs)
- **Caution Yellow**: `#FFD470` - Secondary accent (highlights)
- **White**: Various opacity levels for text hierarchy

### Typography
- **Headings**: Bebas Neue (uppercase, tracking-wider)
- **Body**: Inter (regular 400, bold 700)

## Key Tasks

### Updating Stripe Payment Link

Search and replace all instances of:
```
STRIPE_USD_LINK_TODO
```

Found in multiple locations throughout `index.html`.

### Creating a New Client Preview

1. Save the design mockup as PNG in `/example/` directory
2. Copy `/site/example.html` to `/site/[clientname].html`
3. Update the image path
4. Update the alt text to reflect the client's business
5. Send the client the URL: `https://brokenwebsites.com/site/[clientname]`

## Deployment

This site is deployed via **Cloudflare Pages** connected to GitHub.

**Workflow:**
1. Edit files locally
2. `git add -A && git commit -m "message" && git push`
3. Cloudflare Pages auto-deploys within ~30 seconds

**No build step required** - all files are production-ready as-is.

## Brand Voice & Tone

The copy is direct and no-nonsense but **toned down** from the Australian version:
- Less slang, more universally accessible language
- Still confident and anti-corporate
- Profanity used sparingly for emphasis
- Direct CTAs ("$500 - I WANT IT")

**When editing copy**: Keep it punchy and confident, but avoid regional slang that won't resonate globally.

## Outstanding Tasks

- [ ] Create USD Stripe payment link and replace `STRIPE_USD_LINK_TODO` in index.html
- [ ] Set up Cloudflare Pages deployment
- [ ] Add custom domain brokenwebsites.com in Cloudflare

## Changelog

### 2026-01-16: Accessibility Improvements (WCAG 2.1)
- Added `aria-hidden="true"` to decorative SVGs (mobile menu icons, play icon, scroll indicator, browser window dots)
- Made play button keyboard accessible: `role="button"`, `tabindex="0"`, `aria-label="Play video"`, focus ring
- Made gallery items (4) keyboard accessible: `role="button"`, `tabindex="0"`, `aria-label`, `@keydown.enter` handler, focus ring
- Added `role="dialog"`, `aria-modal="true"`, `aria-label="Website preview"` to lightbox modal
- Added `aria-label="Close lightbox"` to close button
- Added `:aria-expanded` binding to all 10 FAQ accordion buttons
- **Score improved from 72/100 to 92/100**
