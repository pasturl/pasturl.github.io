# Site Audit and Improvement Plan

> Last updated: March 2025

## Completed Fixes

| # | Issue | Status |
|---|-------|--------|
| 1 | Identity updated to CPO & Co-Founder at Artiso AI | Done |
| 2 | Artiso AI added as first experience entry with real logo | Done |
| 3 | Grifols experience added (Jul 2024 - Jul 2025) with real logo | Done |
| 4 | Mango dates corrected (ended Jun 2024) | Done |
| 5 | X-Twitter link removed | Done |
| 6 | Artiso AI link added to social media (rocket icon) | Done |
| 7 | Google AdSense removed from source template | Done |
| 8 | `manifest.json` personalized | Done |
| 9 | SEO meta tags updated in source `public/index.html` | Done |
| 10 | `robots.txt` updated with sitemap | Done |
| 11 | Projects section rebuilt (Artiso, Groovify, Fashion Runway, etc.) | Done |
| 12 | Publications expanded (Cancer Research 2023, Medicinal Chemistry 2017) | Done |
| 13 | All text rewritten to remove AI-generated patterns | Done |
| 14 | SocialMedia.js fixed to support both `fab` and `fas` icon prefixes | Done |
| 15 | Resume link changed from stale Google Drive to LinkedIn | Done |

## Code Quality Review

### Architecture

The site uses a **fork of ashutosh1919/masterPortfolio** (React 16 + CRA 3). This is a working but dated stack. The architecture is simple and fits the GitHub Pages deploy model well:

- `src/portfolio.js` is the single source of truth for all content
- Components are split into `components/` (reusable cards) and `containers/` (page sections)
- Pages live in `src/pages/` and are routed via `react-router-dom`
- Theming via `styled-components` + a manual theme object in `theme.js`

**What works well:**
- Single-file content config makes edits fast and non-breaking
- Component structure is consistent (each has its own `.js` + `.css`)
- Mobile hamburger menu is functional
- Theme switcher architecture exists (disabled but available)

**Issues found:**

| Issue | Severity | Location | Details |
|-------|----------|----------|---------|
| Class components mixed with functional | Low | `ExperienceCard.js`, `Header.js`, `Main.js` | Some use `class extends Component`, others use hooks-style functions. Not blocking, but inconsistent. |
| `SocialMedia.js` hardcoded `fab` prefix | Medium | `SocialMedia.js:29` | Fixed: now reads optional `fontAwesomePrefix` from config. |
| Typo in folder name `assests/` | Low | `src/assests/` | Should be `assets/`. Renaming would break all imports. Leave as-is. |
| Commented-out code blocks | Low | Multiple files | `ProjectCard.js`, `Greeting.js`, `ExperienceCard.css` have large commented sections. Harmless but cluttered. |
| Unused components | Low | `Blogs.js`, `Podcast.js`, `Issues.js`, `PullRequests.js` | Template features not used. They don't ship in the build unless imported. |
| `ExperienceCard.css` has `float: center` | Low | Lines 306, 313 | `float: center` is not valid CSS. Browsers ignore it, no visible bug since `margin: auto` handles centering. |
| Duplicate `<link rel="manifest">` | Low | `public/index.html` lines 21, 48 | Two manifest links. Browsers use the first one. |
| `experience-card` min-width: 350px | Medium | `ExperienceCard.css:91` | On very small screens (< 350px), this forces horizontal scroll. Most phones are 360px+ so marginal risk. |
| `greeting-nickname` line-height: 0px | Medium | `Greeting.css:42` | Forces the nickname text to have zero line height, relying on overflow. Works visually but fragile. |
| No `alt` text on experience logos | Low | `ExperienceCard.js:18` | `alt=""` for all logos. Should be company name for accessibility. |

### Mobile Responsiveness

The site has responsive breakpoints at:
- **1380px** - reduces font sizes
- **768px** - switches to mobile layout (stacked, centered)
- **960px-768px** - reduces header font size

**What works:**
- Header collapses to hamburger menu on mobile
- Experience cards stack vertically, stepper hides
- Project cards go full-width
- Greeting text centers on mobile
- Skills section stacks

**Potential issues:**
- `experience-card` `min-width: 350px` may overflow on very narrow screens
- No breakpoint between 768px and 1380px for tablets; some elements may look sparse
- Project card descriptions are clamped to 2 lines (`-webkit-line-clamp: 2`), truncating longer descriptions

### UI/Style Notes

- The `blueTheme` is active (clean, professional, appropriate for VC audience)
- Font Awesome 6.4.2 loaded via CDN (correct, supports both `fab` and `fas`)
- Iconify 1.0.4 loaded for skill icons
- Google Sans font family used throughout (professional look)
- Scroll animations via `react-reveal` work smoothly
- Footer shows just the name, no social links or copyright (minimal but fine)

## Remaining Improvements (Not Blocking)

These are optional enhancements that can be done in future iterations:

### High Value
1. **Add Press & Media section** - The template doesn't have one natively. Would require creating a new container component. Could reuse the project card layout.
2. **Add canonical URL** - `<link rel="canonical" href="https://lucas-pastur-romay.com/" />` in `public/index.html` for SEO.
3. **Replace `homepage` in package.json** - Currently points to `https://pasturl.github.io`, should be `https://lucas-pastur-romay.com` for correct asset paths if the custom domain ever changes.

### Medium Value
4. **Remove duplicate manifest link** in `public/index.html` (line 21 and 48).
5. **Add `alt` text to experience logos** in `ExperienceCard.js` for accessibility.
6. **Fix `greeting-nickname` line-height** from `0px` to a normal value like `1.2`.
7. **Remove unused commented code** in `ProjectCard.js`, `Greeting.js`.

### Low Value / Future
8. **Upgrade React** from 16 to 18 (would require updating many dependencies, significant effort).
9. **Migrate from CRA to Vite or Next.js** for faster builds and better SSR/SEO.
10. **Add a blog section** using the existing `Blogs.js` container.
11. **Add OG image** meta tag pointing to a real screenshot/portrait instead of `/icons/desc.png`.

## Build & Deploy Reference

```bash
cd ~/masterPortfolio
NODE_OPTIONS=--openssl-legacy-provider npm run build
rsync -av --delete --exclude='.git' --exclude='docs' --exclude='README.md' --exclude='CNAME' build/ ../pasturl.github.io/
cd ../pasturl.github.io
git add . && git commit -m "Update site" && git push origin master
```
