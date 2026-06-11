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
- **Key deadlines:** Submissions open June 15; deadline Aug 10 (11:59 PM Pacific); decisions Sep 18; early reg deadline Oct 15, regular Nov 1, late Nov 30
- **Source of truth for the CFP:** the official Google Doc (export as txt/PDF to get clean content — the body export can leak co-author *comments* as footnotes, so always strip trailing `[a]`/`[b]` comment text and reaction lines)

## Editing Guidelines
- All content changes are direct HTML edits in `index.html`
- Keep images optimized (800px wide for strip, 1200px for panorama)
- Sponsor logos go in `images/logo_*.png` — use dark logos on the gray sponsor section background
- When adding committee members or sponsors, maintain alphabetical ordering
- Push directly to `main` for deployment (GitHub Pages rebuilds in ~1 min)
- **CFP PDF** (`WISE-2026-Call-for-Papers.pdf`, linked from the Call for Papers section) is generated from a standalone branded HTML rendered with headless Chrome: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --no-pdf-header-footer --virtual-time-budget=8000 --print-to-pdf=OUT.pdf file://SOURCE.html`. Keep the PDF's content in sync with the on-page CFP and the timeline dates.

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

## Project Email (`wiseconf2026@gmail.com`)
- Operated via `tools/gmail.py` (gitignored — local-only, never served on the public site). One-time consent: `python3 tools/gmail_auth.py`.
- Auth is **OAuth2** (Desktop client). Credentials live under `oauth/` (gitignored): `oauth/client_secret_*.json` + `oauth/token.json` (refresh token, chmod 600). GCP project `virtual-voyage-499109-b0`. Never print or commit these.
- The OAuth app stays in **Testing** mode (verification avoided), so the refresh token **expires after 7 days** — re-run `tools/gmail_auth.py` to renew. `gmail.py check` warns when it's near expiry.
- Least-privilege scopes: `gmail.readonly` + `gmail.send` (no delete/modify). Account is **hardcoded** in the script — it can only ever act on `wiseconf2026@gmail.com`, never a personal account.
- Capabilities: `check`, `read` (Gmail API metadata — never marks mail as read), `send` (**dry-run unless `--yes`**). No delete.
- Treat sending as an outward action: always preview and get explicit confirmation before `send --yes`. For BULK mail (e.g. acceptances), use the future custom domain + a real email service, not consumer Gmail.
- Examples: `python3 tools/gmail.py check` · `python3 tools/gmail.py read --limit 5 --query "is:unread"` · `python3 tools/gmail.py send --to x@y.com --subject "..." --body "..."` (preview), then add `--yes` to send.
