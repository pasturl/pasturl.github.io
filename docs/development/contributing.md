# Development Guide

## Prerequisites

- Node.js 14+ and npm
- Git

## Setup

```bash
# Clone the source repository
git clone git@github.com:pasturl/masterPortfolio.git
cd masterPortfolio

# Install dependencies
npm install
```

## Local Development

```bash
npm start
```

Opens `http://localhost:3000` with hot reload.

## Content Editing

All website content lives in a single file:

```
src/portfolio.js
```

Edit this file to update any section: bio, experience, projects, publications, skills, contact info, SEO metadata.

## Build & Deploy

```bash
# Build production bundle
npm run build

# Copy build output to the deploy repo
cp -r build/* ../pasturl.github.io/

# Commit and push
cd ../pasturl.github.io
git add .
git commit -m "Update site content"
git push origin master
```

GitHub Pages will serve the updated site within minutes at `lucas-pastur-romay.com`.

## Theme Customization

Color themes are defined in `src/theme.js`. The site supports multiple color schemes toggled via a theme switcher in the header.

## Adding New Sections

1. Create a new config object in `portfolio.js`
2. Export it at the bottom of the file
3. Create a container component in `src/containers/`
4. Import and render it in the appropriate page component under `src/pages/`

## Asset Management

- Company logos → `src/assests/images/`
- Skill icons → Use Iconify class names or Font Awesome
- Profile photo → `src/assests/images/lucas.jpg`
- Favicon/icons → `public/icons/`

## Deployment Checklist

- [ ] All dates are accurate (no stale "Present" on past roles)
- [ ] All external links are working
- [ ] SEO meta tags reflect current role and company
- [ ] `manifest.json` has correct app name
- [ ] No console errors in production build
- [ ] Test on mobile viewport
