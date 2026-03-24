# WISE 2026 Conference Website

## Project Overview
Single-page static website for WISE 2026 (Workshop on Information Systems and Economics), held December 16-18, 2026 in Lisbon, Portugal. Hosted via GitHub Pages from the `main` branch.

**Repo:** https://github.com/MiguelGodinhoMatos/conference_wise2026

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
- **Co-Chairs:** Belo (Nova, local), Ferreira (CMU), Godinho de Matos (Católica, local), Reichman (Tel Aviv), Rock (Wharton), Saar-Tsechansky (McCombs), Todri (Emory)
- **Key deadlines:** Submissions open June 1, deadline Aug 24, decisions Sep 30, early reg Sep 30 - Oct 14

## Editing Guidelines
- All content changes are direct HTML edits in `index.html`
- Keep images optimized (800px wide for strip, 1200px for panorama)
- Sponsor logos go in `images/logo_*.png` — use dark logos on the gray sponsor section background
- When adding committee members or sponsors, maintain alphabetical ordering
- Push directly to `main` for deployment
