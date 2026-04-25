# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for **Fragments #KH50** (fragmentis-vitae.org), a memorial and community engagement project for the Cambodian diaspora. Uses a custom-modified "charlolamode" theme managed as a git submodule.

## Build & Development Commands

```bash
# Local development
hugo server                    # Dev server with live reload
hugo server --buildDraft       # Include draft posts
hugo server --buildFuture      # Include future-dated posts

# Production build
hugo --gc --minify             # Standard build (output in public/)
```

Hugo version: 0.111.2 (pinned in netlify.toml and CI).

## Architecture

- **Hugo static site** — no Node.js, no package.json
- **Theme**: `themes/charlolamode/` (git submodule) — contains all layouts, partials, shortcodes, and CSS
- **Content**: Markdown files in `content/` with YAML front matter; sections include `presentation`, `crowdfunding`, `monument`, `events-actus`, `artistes`, `porteurs-projet`, `soutiens`, `shop`, `espace-presse`, `temoignages`, `contact`, `contributeurs`
- **Structured data**: `data/*.yaml` files (companies, founders, contributors, supports) consumed by shortcodes and partials
- **Static assets**: `static/images/` organized by type (companies, founders, events, etc.)
- **Config**: `config.yml` at root — site title, menu items, params, social links

## Key Patterns

- **Shortcodes** (`themes/charlolamode/layouts/shortcodes/`) render dynamic content from `data/` YAML files: `support-companies`, `founders`, `contributors`, `cta`, `accent-title`
- **Content naming**: dated posts use ISO prefix format `YYYYMMDD-slug.md`
- **Sections** use kebab-case (`events-actus`, `porteurs-projet`, `espace-presse`)
- Markdown allows unsafe HTML (`goldmark.renderer.unsafe: true`) for iframe embeds (YouTube, Google Forms)
- Homepage uses Hugo's profile mode with hero image and CTA buttons

## Deployment

- **GitHub Pages**: CI via `.github/workflows/hugo.yaml` — triggers on push to `main`
- **Netlify**: configured in `netlify.toml` with deploy previews for branches
- Theme is a git submodule — checkout requires `--recurse-submodules`

## Content & Language

All content is in **French**. The theme has i18n support but only French is active.
