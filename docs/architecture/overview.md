# Architecture Overview

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React (Create React App) |
| Source repo | [pasturl/masterPortfolio](https://github.com/pasturl/masterPortfolio) — fork of [ashutosh1919/masterPortfolio](https://github.com/ashutosh1919/masterPortfolio) |
| Deploy target | GitHub Pages at [pasturl.github.io](https://pasturl.github.io) |
| Custom domain | `lucas-pastur-romay.com` (configured via `CNAME`) |
| Styling | CSS Modules + Font Awesome 5/6 + Iconify |
| Fonts | Agustina, Montserrat, Google Sans family |
| SPA routing | Hash-based with `404.html` redirect (spa-github-pages) |
| PWA | Service Worker + `manifest.json` for offline support |
| Analytics | Google Tag Manager (`AW-825508380`) + UA (`UA-158726526-1`) |
| Ads | Google AdSense (`ca-pub-8856447829714090`) |

## Repository Structure

```
pasturl.github.io/          # Deploy repo (build artifacts only)
├── index.html               # Entry point with SEO meta tags
├── 404.html                 # SPA redirect for GitHub Pages
├── CNAME                    # Custom domain: lucas-pastur-romay.com
├── manifest.json            # PWA manifest
├── robots.txt               # Search engine directives
├── service-worker.js        # Offline caching
├── asset-manifest.json      # Webpack asset map
├── icons/                   # Favicon and app icons
├── skills/                  # Skill logo assets
├── static/
│   ├── css/                 # Compiled CSS bundle
│   ├── js/                  # Compiled JS bundles (React app)
│   └── media/               # Images, fonts, SVGs
└── docs/                    # Documentation (this folder)
```

## Source Repository Structure

```
masterPortfolio/src/
├── portfolio.js             # ALL content configuration (single source of truth)
├── App.js                   # Root component
├── App.css                  # Global styles
├── index.js                 # React entry point
├── theme.js                 # Theme/color configuration
├── global.js                # Global constants
├── components/              # Reusable UI components
├── containers/              # Section containers (Skills, Education, etc.)
├── pages/                   # Page-level components
├── shared/                  # Shared utilities
└── assests/                 # Static assets (images, fonts)
```

## Content Configuration

All website content is defined in `masterPortfolio/src/portfolio.js`. This single file controls:

| Section | Config Object | Description |
|---------|--------------|-------------|
| SEO | `seo` | Page title, description, Open Graph tags |
| Homepage | `greeting` | Name, tagline, subtitle, resume link |
| Social links | `socialMediaLinks` | GitHub, LinkedIn, Gmail, Twitter/X |
| Skills | `skills` | Three skill categories with icons |
| Education | `degrees` | PhD, Masters, Biology degree |
| Certifications | `certifications` | Coursera specializations |
| Experience | `experience` | Work history and teaching positions |
| Projects | `projects` | Featured project cards |
| Publications | `publications` | Academic papers |
| Contact | `contactPageData` | Contact info, address, blog |

## Build & Deploy Workflow

1. Edit content in `masterPortfolio/src/portfolio.js`
2. Run `npm run build` in the `masterPortfolio` directory
3. Copy `build/` output to `pasturl.github.io/` root
4. Commit and push to `pasturl.github.io` repo
5. GitHub Pages serves from `master` branch

## Key Dependencies

- `react` / `react-dom` — UI framework
- `react-router-dom` — Client-side routing
- `react-reveal` — Scroll animations
- `react-headroom` — Sticky header
- `react-lottie` — Animated SVG illustrations
- `emoji-js` — Emoji rendering
- `baseui` — Base Web UI components
