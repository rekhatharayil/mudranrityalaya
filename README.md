# Mudra Nrityalaya – Website

Website for **Mudra Nrityalaya**, a Bharatanatyam dance school in Cambrian Park, San Jose, founded by Rekha Garg (disciple of Kalaimamani Guru Shri Madurai R. Muralidharan).

| | |
|---|---|
| **Live site** | https://www.mudranrityalaya.com |
| **Redesign preview (v2)** | https://www.mudranrityalaya.com/v2/ (unlisted) |
| **Hosting** | GitHub Pages, free, from the `main` branch of this repo |
| **Domain registrar / DNS** | Namecheap (BasicDNS) |
| **SSL** | Free Let's Encrypt certificate, issued and auto-renewed by GitHub Pages |
| **Contact email on site** | contactmudra.n@gmail.com |

The site is plain HTML and CSS with a few lines of vanilla JavaScript. There is no build step, framework or dependency: whatever is in `main` is what is served.

---

## Repository layout

```
.
├── index.html            Home: hero, founder bio, offerings, photo strip
├── Classes/index.html    Curriculum (Beginner / Intermediate), schedule, dance forms
├── Gallery/index.html    All 30 photos with a click-to-enlarge lightbox
├── css/style.css         Styles for the three pages above
├── v2/                   Alternative redesign (single page), see below
│   ├── index.html
│   └── style.css
├── images/
│   ├── logo.png          School logo (green/gold "MN")
│   ├── rekha.jpg         Founder portrait (514×731, the largest that existed)
│   ├── gallery/NN.jpg    Full-size photos, max 1600px, JPEG q80
│   └── thumbs/NN.jpg     Thumbnails, max 600px, JPEG q75
├── CNAME                 Custom domain for GitHub Pages (www.mudranrityalaya.com)
└── .nojekyll             Tells GitHub Pages to serve files as-is (no Jekyll)
```

The page URLs `/Classes/` and `/Gallery/` match the old Namecheap site exactly, so existing links and search results keep working. GitHub Pages URLs are **case-sensitive**: keep the capital letters.

---

## Two versions of the site

### Original (root `/`)
A faithful rebuild of the old Namecheap site: same three pages, same text (with small typo fixes), same photos, and a deep-green and gold look matching the logo.

### v2 (`/v2/`)
A single-page redesign built around how parents and students actually decide on a dance school:

- **Hero** answers *what / who / where* in a few seconds, with quick-fact chips (Ages 5+, Adults welcome, Weekly 60-min classes, Aug–Jun) and one clear "Enquire" action.
- **Credibility strip**: guru–shishya lineage, Lady Andal Auditorium, Bharatanatyam and Mohiniyattam training, Bay Area performances.
- **"The name"**: *Mudrā* (hand gesture) and *Nṛtyālaya* (abode of dance) as the story hook, plus three pillars: Discipline, Artistry, Tradition.
- **Class cards by audience** (children 5+, adult semi-classical, event choreography). Each card opens a **pre-filled enquiry email** for that class.
- **Learning path**: Beginner → Intermediate → On Stage, using the real curriculum.
- **Teacher and lineage (paramparā)**: Kalamandalam Smt. Rema → Guru Madurai R. Muralidharan → Rekha → students; full bio behind "Read Rekha's full story".
- **Gallery**: 8 curated photos, with "View all 30" and a lightbox.
- **"New to Bharatanatyam?"**: Nṛtta, Nṛtya and Nāṭya explained for newcomers.
- **FAQ** and a final call to action; on phones, a fixed "Enquire" bar.
- **Look**: aged-parchment and sandalwood backgrounds with a subtle paper grain, kumkum red and temple gold, arch-shaped photo frames and a saree-border zigzag.

Everything on v2 comes from the original site's content. Nothing (fees, testimonials, trial offers) is invented.

v2 is **unlisted**: nothing links to it, and it carries `<meta name="robots" content="noindex">` so search engines don't index duplicate content. It uses the same images as the original (`../images/...`).

**To make v2 the main site:** move `v2/index.html` and `v2/style.css` to the root, change the `../images/` paths to `/images/`, remove the `noindex` meta tag, and add redirects or keep `/Classes/` and `/Gallery/` so old links still work. The original stays in git history.

---

## Editing the site

1. Edit the HTML or CSS files directly. The header and footer are repeated in each page (there are no templates), so a change to the menu or footer must be made in **every** page:
   - `index.html`, `Classes/index.html`, `Gallery/index.html`
   - `v2/index.html` (has its own header and footer)
2. Preview locally (from the repo folder, on one line):
   ```bash
   python3 -m http.server 8765
   ```
   Then open http://localhost:8765/ (original) or http://localhost:8765/v2/ (redesign). Press `Ctrl+C` to stop.
3. Commit and push to `main`. GitHub Pages rebuilds automatically, usually within a minute. Hard-refresh the browser (`Cmd+Shift+R`) to see changes.

### Adding photos
Keep photos web-sized; the original uploads were about 55 MB in total. On a Mac, `sips` (built in) does this:

```bash
# full-size (max 1600px) and thumbnail (max 600px)
sips -s format jpeg -s formatOptions 80 -Z 1600 original.jpg --out images/gallery/31.jpg
sips -s format jpeg -s formatOptions 75 -Z 600  original.jpg --out images/thumbs/31.jpg
```

Then add a link to the gallery page(s):

```html
<a href="/images/gallery/31.jpg"><img src="/images/thumbs/31.jpg" alt="Describe the photo" loading="lazy"></a>
```

(In `v2/index.html`, use `../images/...` paths and add `class="hidden"` to keep it out of the first 8 curated photos.)

### Things to keep as they are
- **`CNAME`**: must contain `www.mudranrityalaya.com`. Deleting it disconnects the custom domain. (GitHub itself sometimes rewrites this file when the domain is re-saved in Settings → Pages; just `git pull` before your next push.)
- **`.nojekyll`**: keep it.
- **Google Analytics tag** `G-VL1BTH26CC` is on every page, carried over from the old site so historical stats continue. In Analytics, filter by page path (`/` vs `/v2/`) to compare the two designs.

---

## Hosting, domain and DNS

### GitHub
- Organization: [`rekhatharayil`](https://github.com/rekhatharayil) (free plan). It's kept separate from personal accounts so the school's site can be shared with other maintainers without giving access to anything else.
- Repo: `rekhatharayil/mudranrityalaya`, **public** (free GitHub Pages requires a public repo; it contains only the website, with no secrets or keys).
- Settings → Pages: source `main` / root, custom domain `www.mudranrityalaya.com`, **Enforce HTTPS: on**.
- The domain `mudranrityalaya.com` is **verified** for the organization (Org Settings → Pages), which prevents anyone else from claiming it on GitHub.
- Commits use the GitHub noreply email so personal email addresses don't appear in the public history.

### Namecheap
The domain is registered at Namecheap. **Keep the domain registration renewed**; that's the only Namecheap item still needed. The old Namecheap hosting plan is no longer used.

Nameservers: **Namecheap BasicDNS** (`dns1/dns2.registrar-servers.com`). Records under Domain List → Manage → **Advanced DNS**:

| Type | Host | Value | Purpose |
|---|---|---|---|
| A | `@` | `185.199.108.153` | GitHub Pages |
| A | `@` | `185.199.109.153` | GitHub Pages |
| A | `@` | `185.199.110.153` | GitHub Pages |
| A | `@` | `185.199.111.153` | GitHub Pages |
| CNAME | `www` | `rekhatharayil.github.io.` | GitHub Pages |
| TXT | `_gh-rekhatharayil-o` | *(code from GitHub)* | GitHub domain verification |

There must be **no "URL Redirect Record" on `@`**: it conflicts with the A records and breaks HTTPS. GitHub already redirects `mudranrityalaya.com` → `https://www.mudranrityalaya.com`.

### Email
`info@mudranrityalaya.com` forwards to `contactmudra.n@gmail.com` via Namecheap's free email forwarding (Domain → Redirect Email). It's receive-only. The MX and SPF records for forwarding are managed automatically by Namecheap BasicDNS. The website itself shows the Gmail address directly.

### SSL / HTTPS
GitHub Pages issues and renews the Let's Encrypt certificate (covers `www.mudranrityalaya.com` and `mudranrityalaya.com`) automatically; nothing to renew by hand. All `http://` and non-`www` addresses redirect to `https://www.mudranrityalaya.com`.

If HTTPS ever breaks (for example after DNS changes): in repo Settings → Pages, **Remove** the custom domain, re-enter `www.mudranrityalaya.com`, wait for the certificate (minutes to a few hours), then tick **Enforce HTTPS**.

---

## Migration history (October 2026)

The site previously ran on Namecheap hosting (website builder), and its SSL certificate had expired. It was moved to GitHub Pages:

1. Downloaded the three pages' content and all 32 images from the old site; resized photos from about 55 MB to about 17 MB.
2. Rebuilt the site as static HTML/CSS with the same URLs; fixed small typos ("Nritylaya" → "Nrityalaya", etc.).
3. Created the `rekhatharayil` GitHub organization and this repo; enabled Pages with the custom domain.
4. Switched Namecheap nameservers from the hosting plan's DNS to BasicDNS and added the GitHub records; removed the old URL redirect record.
5. Verified the domain with GitHub; the free certificate was issued and HTTPS enforced once DNS caches cleared (about 3 hours).
6. Added the contact email, fixed the portrait's aspect ratio, shortened the home hero banner, set the copyright to "2023–present".
7. Built and published the v2 redesign at `/v2/`.

### Open items / ideas
- Cancel the old Namecheap **hosting** plan (keep the domain).
- Get a higher-resolution portrait of Rekha (current one is 514×731).
- For v2, if Rekha can provide them: a trial-class offer, a 30–60 second performance video, 2–3 parent quotes, and upcoming recital dates.
- Decide whether v2 replaces the original.
