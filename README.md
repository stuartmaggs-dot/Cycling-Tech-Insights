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

## Development notes

- **Styling:** All pages share `/css/article.css`. The homepage has its styles inline (in `<style>`) for a single-file initial load.
- **No JavaScript dependencies.** The only JS is a one-liner to write the current year into the footer.
- **Deployment:** Push to `main` → Vercel auto-deploys.
