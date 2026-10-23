# Working notes for Claude

Read `README.md` first: it documents the site, hosting, DNS, SSL, email, v2 and history.

## Current state (as of 2026-10-23)
- Live: https://www.mudranrityalaya.com (original rebuild), served by GitHub Pages from `main` of `rekhatharayil/mudranrityalaya`. HTTPS enforced, domain verified.
- `/v2/` is an unlisted (noindex) single-page redesign. **Decision pending** on whether it replaces the original; don't swap it in without the user asking.
- Old Namecheap hosting plan is being left to expire (no refund). Domain stays on Namecheap BasicDNS with auto-renew.
- Open ideas: higher-res portrait of Rekha; for v2, trial-class offer, performance video, parent quotes, recital dates (only if provided; never invent these).

## How to work in this repo
- Pushing to `main` deploys. Treat every push as publishing to the live site.
- **Always `git pull --rebase` before pushing.** GitHub commits to `CNAME` itself whenever the custom domain is re-saved in Pages settings, so pushes get rejected otherwise.
- Repo-local git identity uses the GitHub noreply email; keep it that way (public repo, no personal emails in history).
- After pushing, wait for the Pages build of *that* commit before checking the live site:
  `gh api repos/rekhatharayil/mudranrityalaya/pages/builds/latest --jq '"\(.commit) \(.status)"'`
  (`latest` may still be the previous build right after a push).
- Header and footer are duplicated in every page (`index.html`, `Classes/index.html`, `Gallery/index.html`, `v2/index.html`); change them all.
- Keep `/Classes/` and `/Gallery/` capitalized (they match the old site's URLs; Pages is case-sensitive).
- Large pushes (images) may need `git config http.postBuffer 157286400` (already set in this repo).
- Resize images with `sips` (see README) before adding; never commit originals.
- Local preview: `python3 -m http.server 8765`, then open http://localhost:8765/ and stop the server when done.
- Headless Chrome screenshots: Chrome's headless window won't go below 500px wide, so "390px" screenshots get cropped rather than reflowed. Don't mistake that for overflow. Chrome can also hang after writing the screenshot; kill it with a timeout.
- Content rule: only use facts from the original site or the user. No made-up fees, testimonials, offers or dates.
