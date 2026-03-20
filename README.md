# Cycling Tech Insights

**[cyclingtechinsights.com](https://www.cyclingtechinsights.com)** — Independent analysis of cycling technology, AI training tools, and UK-available gear for performance-focused riders.

---

## Content Structure Plan

This site is intentionally kept as a **plain static HTML site** — no build tools, no frameworks, no Node. Every page is a standalone `.html` file. Vercel serves them as-is.

### Folder layout

```
/
├── index.html              ← Homepage (listing + intro)
├── articles/               ← One HTML file per article
│   ├── ai-cycling-training-platforms.html
│   ├── garmin-edge-840-review.html
│   └── smart-trainers-uk-comparison.html
└── css/
    └── article.css         ← Shared stylesheet for article pages
```

### Why this structure?

- **No build step needed.** Vercel picks up every `.html` file and serves it at its natural path (e.g. `/articles/garmin-edge-840-review`).
- **Easy to extend.** Add a new article by dropping a new `.html` file in `/articles/` and adding a card to `index.html`.
- **Affiliate-ready.** Each article page has a designated affiliate-link area in the body. UK-specific affiliate programmes (Wiggle, Sigma Sport, Amazon UK, Wahoo UK) can be dropped in per-article.
- **SEO-friendly.** Each page has its own `<title>`, `<meta description>`, and canonical URL.

### Content strategy (UK-first)

1. AI and tech-enabled training platforms (Zwift, Wahoo SYSTM, TrainerRoad, Xert, OnForm) with UK pricing.
2. Hardware reviews: head units, power meters, smart trainers — all with UK RRP and where to buy in the UK.
3. Weekly tech roundups and buyer guides targeted at UK riders.

### Monetisation approach

- Affiliate links embedded naturally within article content (Amazon Associates UK, Wiggle, Sigma Sport).
- Future: display ads (Carbon Ads / Mediavine once traffic grows), sponsored content, and email newsletter.

---

## Visual Design (v2 — March 2026)

A full visual redesign was applied to `index.html` and `css/article.css` with no structural changes to content, URLs, or file locations.

### What changed

**Fonts**
- Added [Satoshi](https://www.fontshare.com/fonts/satoshi) (700, 500) via Fontshare CDN for all headings — replaces generic system-ui. Satoshi gives a contemporary, editorial feel without being overexposed.
- Added [Inter](https://fonts.bunny.net) (400, 500) via Bunny Fonts for body text — neutral, highly legible at small sizes.
- Both fonts load via CDN with `display=swap`; no self-hosting required.

**Colour palette**
- Replaced blue (#2563eb) accent with **Hydra Teal** (`#01696F` / `#0C4E54`) throughout — a warmer, more distinctive accent that distinguishes the site from generic tech blogs.
- Homepage background: `#F7F6F2` (warm off-white) instead of cool grey.
- All surfaces: `#FDFCFA` (very slightly warm white) with `#D4D1CA` borders — creates clear layering without heavy drop shadows.
- Tag pills: teal-tinted (`#D6EFEF` bg, `#0C4E54` text) — consistent with accent.
- Buy boxes: green (`#F0FAF5` bg, `#A8DABC` border) — signals positive/action without overusing green elsewhere.

**Homepage (`index.html`)**
- Hero header: deeper padding, teal gradient overlay stripe, pill-shaped "UK Cycling Tech" kicker badge above the title, `clamp()`-sized responsive headline.
- Intro section: two-column layout on ≥640 px (prose left, bullet list right) with arrow-prefixed list items instead of plain bullets.
- Section label: uppercase micro-label with a `::after` rule extending a divider line to the right edge — cleaner than a plain border-bottom paragraph.
- Article cards: teal top accent bar on hover, `translateY(-2px)` lift, border highlights to `--accent` on hover — cards now feel interactive and premium.
- "Read article" CTAs: border-bottom underline style with animated arrow (`translateX(3px)`) on hover.
- "Coming soon" card: dashed border, transparent background — visually distinct from live content.
- `prefers-reduced-motion` respected throughout.

**Article pages (`css/article.css`)**
- Header: slim horizontal nav bar (dark background) with site name left-aligned and "← All articles" back link right-aligned — replacing the centred wordmark.
- `h1`: `clamp()` fluid sizing, Satoshi 700, negative letter-spacing.
- `h2` section headings: lighter bottom border (`1px var(--border)`) instead of `2px solid #e5e7eb`.
- Article `<article>` element: `border: 1px solid var(--border)` replaces box-shadow for a flatter, more editorial feel.
- Comparison tables: wrapped in `<div class="table-wrap">` for horizontal scroll on mobile; dark header row uses `--header-bg` with muted uppercase column labels.
- Buy boxes: `.buy-links` wrapper gives button row proper flex layout with wrapping; button background changed to `#16803C` (green).
- Article meta row: separator dots auto-inserted between non-tag items via `::before` pseudo-element — no manual `·` characters needed.
- Full `@media (max-width: 640px)` block for article padding and font size.

---

## Logo Header (v3 — March 2026)

A logo was added to the repository root and a consistent header bar introduced across all pages.

### Logo files

| File | Use |
|------|-----|
| `Blue Black Minimal Initial Letter Company Technology Logo.svg` | Primary logo (vector, served first) |
| `Blue Black Minimal Initial Letter Company Technology Logo.png` | Fallback if SVG fails to load |

Both files live in the repo root and are served at `/` by Vercel. The `<img>` tag references the SVG via URL-encoded path and falls back to the PNG via the `onerror` attribute — no JavaScript library or build step required.

### What changed

**New shared `.site-header` component**

All pages (homepage and all `/articles/` pages) now open with an identical logo nav bar rendered as `<div class="site-header">`. The bar contains:
- Left: `.site-logo` — logo image (40 × 40 px, `border-radius: 6px`) + `.header-text` block with `.logo-name` (site title) and `.logo-tagline` ("UK Cycling Tech & AI Tools")
- Right: navigation links (`Articles`, `About` on the homepage) or a `← All articles` back link on article pages

The bar sits above the existing hero section on the homepage and replaces the old slim text-only nav bar on article pages.

**CSS additions**

- `index.html` inline `<style>`: added `.site-header`, `.site-header .header-inner`, `.site-header .site-logo`, `.site-header .site-logo img`, `.site-header .header-text`, `.site-header .header-text .logo-name`, `.site-header .header-text .logo-tagline`, `.site-header .header-nav`, `.site-header .back-nav` rules, plus a `@media (max-width: 420px)` rule to hide the tagline on very small screens.
- `css/article.css`: same set of rules replacing the old `header`, `.header-inner`, `header a.site-name`, `.back-nav` rules.

**No structural changes** to article content, URLs, folder layout, or any other CSS.

---

## Development notes

- **Styling:** All pages share `/css/article.css` (with `@import` for fonts). The homepage has its styles inline (in `<style>`) for a single-file initial load.
- **No JavaScript dependencies.** The only JS is a one-liner to write the current year into the footer.
- **Deployment:** Push to `main` → Vercel auto-deploys.
