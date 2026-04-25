# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

APEX (AI Portfolio & Exchange System) is a static documentation site — a detailed R&D blueprint for an AI-driven investment portfolio management system targeting US stocks, funds, and commodities with a ฿500,000 capital base.

## Commands

```bash
npm run dev       # Start Vite dev server with HMR
npm run build     # Build optimized static output to dist/
npm run preview   # Preview production build locally
```

No test suite or linter is configured.

## Architecture

This is a **pure HTML/CSS static site** with no JavaScript logic. Vite is used solely for the dev server and production optimization.

```
apex_blueprint/
├── index.html              # Main site: 17 content sections (~4,000 lines)
├── styles_showcase.html    # CSS component demo page
├── src/
│   ├── apex_styles.css     # Centralized design system (1,321 lines)
│   └── assets/             # Images (hero.png, icons)
└── public/                 # favicon.svg, icons.svg
```

All content lives in `index.html`. All styling lives in `src/apex_styles.css`. There is no routing, no state management, and no JavaScript beyond what Vite injects.

## CSS Design System

The entire visual language is defined via CSS custom properties in `:root` inside `src/apex_styles.css`:

- **Colors:** Primary accent purple (`#b263ff`) + cyan (`#54d9ff`); semantic highlights for red, gold, green, orange
- **Glassmorphism:** `backdrop-filter: blur()` on `.card` elements over a dark navy gradient
- **Animated blobs:** Four `@keyframes blobFloat` background elements at z-index 0
- **Typography:** Google Fonts — Bebas Neue (headings), DM Sans (body), DM Mono (code/mono)

### Key component classes

| Class | Purpose |
|-------|---------|
| `.card` | Glassmorphic content container; use `data-num` attribute for label badge |
| `.card-grid` | CSS Grid wrapper for multi-column card layouts |
| `.rule-box` | Structured decision/rule block with heading + list |
| `.bench-card` | Benchmark target display with large percentage number |
| `.ptag` | Pill/badge for technology or category tags |
| `.text-bright`, `.text-dim`, `.text-highlight`, `.price-highlight` | Semantic text utilities |
| `.blur-tbody` | Glassmorphic table row styling |

### Z-index layering

Background blobs → grid overlay → page content (sticky nav on top)

## Content Structure

`index.html` contains 17 anchor-linked sections (e.g., `#objectives`, `#allocation`, `#datasources`, `#models`). The sticky nav header links to each. When adding or reordering sections, update both the section `id` and the nav link.

## Development Notes

- **STRICT RULE:** `index.html` contains structure only — no inline `style` attributes, no `<style>` tags. All CSS must go in `src/apex_styles.css`.
- Edit CSS variables in `:root` to restyle site-wide; avoid hardcoding colors inline
- `data-num` on `.card` elements controls the decorative label that appears via `::after` pseudo-element
- The site targets desktop/tablet layouts; the max content width is `1100px`
- No ARIA labels are currently used — add them if improving accessibility
