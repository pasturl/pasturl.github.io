# lucas-pastur-romay.com

Personal website of **Lucas Pastur Romay** — CPO & Co-Founder at [Artiso AI](https://www.artiso.ai), building the operating system for fashion with agentic AI.

**Live**: [lucas-pastur-romay.com](https://lucas-pastur-romay.com)

## Quick Start

This repo contains the **build output** deployed to GitHub Pages. The source code lives in [pasturl/masterPortfolio](https://github.com/pasturl/masterPortfolio).

```bash
# Clone source repo
git clone git@github.com:pasturl/masterPortfolio.git
cd masterPortfolio

# Install and run locally
npm install
npm start

# Build and deploy
npm run build
cp -r build/* ../pasturl.github.io/
cd ../pasturl.github.io && git add . && git commit -m "Update site" && git push
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React (Create React App) |
| Hosting | GitHub Pages |
| Domain | `lucas-pastur-romay.com` |
| Styling | CSS + Font Awesome + Iconify |
| Analytics | Google Tag Manager |

## Content

All content is configured in a single file: `masterPortfolio/src/portfolio.js`

- **Bio** — CPO & Co-Founder at Artiso AI
- **Experience** — Artiso AI, Grifols, Mango, Grupo AIA, KDP, UDC
- **Skills** — Agentic AI, Generative AI, Product Development, Cloud/MLOps
- **Projects** — Artiso AI, Lisa, Inspire, Groovify, Fashion Runway Trends
- **Publications** — Peer-reviewed papers in Cancer Research, AIMM, IJMS
- **Education** — PhD in AI (Cum Laude), Neuroscience MSc, Biology degree

## Documentation

See [`/docs`](./docs/) for detailed documentation:

- [`docs/architecture/overview.md`](./docs/architecture/overview.md) — System architecture and repo structure
- [`docs/guides/content-improvement-plan.md`](./docs/guides/content-improvement-plan.md) — Content audit and improvement roadmap
- [`docs/development/contributing.md`](./docs/development/contributing.md) — Development setup and deployment guide

## License

MIT — Based on [ashutosh1919/masterPortfolio](https://github.com/ashutosh1919/masterPortfolio)
