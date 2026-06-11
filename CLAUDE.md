# WISE 2026 Conference Website

## Project Overview
Single-page static website for WISE 2026 (Workshop on Information Systems and Economics), held December 16-18, 2026 in Lisbon, Portugal. Hosted via GitHub Pages from the `main` branch.

**Repo:** https://github.com/wiseconf2026/wiseconf2026.github.io
**Live site:** https://wiseconf2026.github.io/

> ⚠️ **Account ownership:** This project lives under the dedicated **`wiseconf2026`** GitHub account — NOT Miguel's personal `MiguelGodinhoMatos` account. The old personal copy (`MiguelGodinhoMatos/conference_wise2026`) has been retired. Always push to the `wiseconf2026` remote.

## Architecture
- **Single HTML file** (`index.html`) with all CSS and JS inline — no build step, no framework
- **Images** in `images/` — Lisbon photos (Unsplash, free to use), university sponsor logos, WISE owl logo
- **No external dependencies** except Google Fonts (DM Serif Display + DM Sans)

## Key Design Decisions
- Dark navy (#0a1628) + gold (#c8963e) color palette
- Responsive: breakpoints at 768px (tablet) and 480px (mobile)
- Hamburger menu on mobile, fixed nav on desktop
- Scroll-reveal animations via IntersectionObserver
- Photo strip between About and Important Dates sections

## Content Structure (sections in order)
1. Hero (with WISE logo)
2. About
3. Lisbon photo strip
4. Important Dates (timeline)
5. Call for Papers
6. Organizing Committee (alphabetical by last name)
7. Venue (Lisbon)
8. Registration
9. Program & Social Events
10. Sponsors (Católica Lisbon, Nova SBE)
11. Past WISE (1989-2025, with toggle)
12. Footer

## Conference Details
- **Dates:** Dec 16 (reception), Dec 17-18 (conference), 2026
- **Co-Chairs:** Belo (Nova, local), Cheng (LSE), Ferreira (CMU), Godinho de Matos (Católica, local), Reichman (Tel Aviv), Rock (Wharton), Saar-Tsechansky (McCombs), Todri (Emory)
- **Key deadlines:** Submissions open June 15, deadline Aug 24, decisions Sep 30, early reg Sep 30 - Oct 14

## Editing Guidelines
- All content changes are direct HTML edits in `index.html`
- Keep images optimized (800px wide for strip, 1200px for panorama)
- Sponsor logos go in `images/logo_*.png` — use dark logos on the gray sponsor section background
- When adding committee members or sponsors, maintain alphabetical ordering
- Push directly to `main` for deployment (GitHub Pages rebuilds in ~1 min)

## Deployment & Auth
- `origin` points to `https://github.com/wiseconf2026/wiseconf2026.github.io.git` (no token embedded).
- The local machine's default `gh` login is Miguel's **personal** account, which does **not** have write access to the `wiseconf2026` repo. So a plain `git push` will fail.
- Push using the `wiseconf2026` admin token stored in `.env` (var `GITHUB_WISECONF2026`, gitignored):
  ```bash
  set -a && source .env && set +a
  git push "https://wiseconf2026:${GITHUB_WISECONF2026}@github.com/wiseconf2026/wiseconf2026.github.io.git" main:main
  ```
  When printing push output, redact the token: `sed -E "s/wiseconf2026:[^@]+@/[redacted]@/g"`.
- Never write the token into `.git/config` or any committed file — the repo folder is inside Dropbox.
