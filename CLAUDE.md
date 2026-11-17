# Working notes for Claude

Read `README.md` first: it documents the site, hosting, DNS, SSL, email, v2 and history.

## Who you're working with
Whoever is working on the site (the person who set it up, or later the school's owner) describes changes in plain words; you do everything else. **Assume they are not a developer.**
- Use plain language. Avoid jargon (git, commit, push, HTML, CSS, DNS). Say "publish", "the live site", "a preview".
- Never ask them to run commands, edit files, or use GitHub or Namecheap. Do all git work yourself, silently: `git pull --rebase` before starting, then commit with a clear message.
- For every change: make it → show a preview (run the local server and open it in the browser pane, or send a screenshot) → **publish only after they say it looks good** → confirm it's live and give the link.
- If it's unclear whether they mean the main site or `/v2/`, ask which one.
- Photos they share: resize with `sips` (see README) and add them; never commit the originals.
- Domain, DNS and Namecheap are managed by the person who set the site up. If the school's owner is working and something needs those accounts, say so plainly and suggest they ask that person.
- If a GitHub push fails because of login or permissions, explain simply and stop; don't try workarounds with other accounts.

## Current state (as of 2026-10-23)
- Live: https://www.mudranrityalaya.com (original rebuild), served by GitHub Pages from `main` of `rekhatharayil/mudranrityalaya`. HTTPS enforced, domain verified.
- `/v2/` is an unlisted (noindex) single-page redesign. **Decision pending** on whether it replaces the original; don't swap it in without the user asking.
- Old Namecheap hosting plan is being left to expire (no refund). Domain stays on Namecheap BasicDNS with auto-renew.
- Open ideas: higher-res portrait of Rekha; for v2, trial-class offer, performance video, parent quotes, recital dates (only if provided; never invent these).

## How to work in this repo
- Pushing to `main` deploys. Treat every push as publishing to the live site.
- **Always `git pull --rebase` before pushing.** GitHub commits to `CNAME` itself whenever the custom domain is re-saved in Pages settings, so pushes get rejected otherwise.
- Repo-local git identity must use the GitHub noreply email (public repo, no personal emails in history). On a fresh clone or a new computer, check `git config user.email`; if it isn't a `@users.noreply.github.com` address, set it with `git config user.email "<id>+<login>@users.noreply.github.com"` using `gh api user --jq '"\(.id)+\(.login)"'`.
- The site may be edited from more than one computer, which makes `git pull --rebase` before starting essential.
- After pushing, wait for the Pages build of *that* commit before checking the live site:
  `gh api repos/rekhatharayil/mudranrityalaya/pages/builds/latest --jq '"\(.commit) \(.status)"'`
  (`latest` may still be the previous build right after a push).
- Header and footer are duplicated in every page (`index.html`, `Classes/index.html`, `Gallery/index.html`, `v2/index.html`); change them all.
- Keep `/Classes/` and `/Gallery/` capitalized (they match the old site's URLs; Pages is case-sensitive).
- Large pushes (images) need `git config http.postBuffer 157286400`; set it on any new clone.
- Resize images with `sips` (see README) before adding; never commit originals.
- Local preview: `python3 -m http.server 8765`, then open http://localhost:8765/ and stop the server when done.
- Headless Chrome screenshots: Chrome's headless window won't go below 500px wide, so "390px" screenshots get cropped rather than reflowed. Don't mistake that for overflow. Chrome can also hang after writing the screenshot; kill it with a timeout.
- Content rule: only use facts from the original site or the user. No made-up fees, testimonials, offers or dates.
