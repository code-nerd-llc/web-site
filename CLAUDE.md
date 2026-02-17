# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jekyll static site for **codenerd.llc**, hosted on GitHub Pages. Uses the `github-pages` gem (Jekyll 3.9.x) with a fully custom dark theme — minima is not used.

## Development Commands

```bash
bundle install            # Install dependencies
bundle exec jekyll serve  # Local dev server (http://localhost:4000), auto-reloads except _config.yml
bundle exec jekyll build  # Build static site to _site/
```

Changes to `_config.yml` require restarting `jekyll serve`.

## Architecture

Single-page consulting site. Zero JavaScript. Pure CSS responsive design.

- **`_config.yml`** — Site config, SEO metadata, plugins (`jekyll-seo-tag`, `jekyll-sitemap`), sass config, exclude list
- **`_layouts/default.html`** — The only layout. Full HTML shell with `<head>` (viewport, SEO, CSS, favicon), nav include, `<main>`, and inline footer
- **`_includes/nav.html`** — Sticky nav with CSS-only hamburger menu (checkbox hack, no JS). Hardcoded anchor links
- **`_includes/icon.html`** — Reusable inline SVG icon partial. Called with `{% include icon.html icon="name" %}`. Supports: cloud, code, users, terminal, mail, linkedin, github
- **`_data/services.yml`** — Service card data (title, description, icon) rendered in a loop on the index page
- **`index.html`** — All page sections inlined: hero, about, services, contact. Uses `default` layout
- **`_sass/`** — Three partials: `_variables.scss` (design tokens), `_reset.scss` (CSS reset), `_site.scss` (all styles)
- **`assets/css/main.scss`** — SCSS entry point with Jekyll front matter. Imports all partials. Compiles to `main.css`
- **`assets/images/`** — Logo variants. `Code-Nerd-logos_white.png` (white on transparent) used in hero
- **CNAME** — Custom domain: `codenerd.llc`

## Constraints

- **Jekyll 3.9.x** (not 4.x) — pinned by `github-pages` gem
- **Ruby Sass** via `jekyll-sass-converter 1.5.2` — use `@import`, NOT `@use`/`@forward`
- **GitHub Pages plugin whitelist only** — no custom Ruby plugins
- **No server-side processing** — purely static output
