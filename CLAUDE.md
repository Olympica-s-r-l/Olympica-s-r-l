# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static single-page marketing website for **Olympica S.r.l.** promoting the WeSports Center & Village corporate wellbeing format. Deployed to [olympica.it](https://olympica.it) via GitHub Pages (see `CNAME`).

No build system, no package manager, no bundler — just `index.html` + `assets/`.

## Running locally

Open `index.html` directly in a browser, or serve with any static file server to avoid CORS issues with fonts/scripts:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## Architecture

Everything lives in two files:

- **`index.html`** — the full page, written in Italian, structured as sequential `<section>` blocks with Bootstrap 5 grid. Sections are identified by `id` attributes (`#hero`, `#format`, `#neuro-vr`, `#technical-structure`, `#contact-cta`, etc.).
- **`assets/css/olympica-theme.css`** — all custom styles layered on top of Bootstrap.

### CSS design system

The neon/cyberpunk dark theme is driven by CSS custom properties in `:root`:

| Variable | Value | Usage |
|---|---|---|
| `--neon-primary` | `#0ff` (cyan) | `.neon-text`, `.neon-table` headers |
| `--neon-secondary` | `#f0f` (magenta) | `.neon-border`, `.neon-list` left border |
| `--neon-accent` | `#ff0` (yellow) | `.neon-accent` text |
| `--bg-color` | `#0b0f19` | `.bg-main` sections |
| `--bg-color-alt` | `#212529` | `.bg-main-alt` alternating sections |

Section backgrounds alternate between `.bg-main` and `.bg-main-alt`. Images use `.img-uniform` (`grayscale(60%)`) to maintain visual consistency.

### External dependencies (all CDN, no local install)

- Bootstrap 5.3 (CSS + JS bundle)
- Bootstrap Icons 1.10.5
- Google Fonts: Orbitron (headings), Roboto (body)
- Animate.css 4.1.1 + AOS 2.3.4 (scroll animations — initialized with `AOS.init({once: true, duration: 800})`)

### Third-party integrations

- **Contact form**: submitted via [Formspree](https://formspree.io/f/xkgbwrep) using plain `<form method="POST">`
- **Chatbot**: embedded via JotForm script at page bottom
