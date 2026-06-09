# Kaffeine — Website

Static website for Kaffeine, a specialty coffee shop at 154 University Ave, Toronto, ON.

No build step — plain HTML/CSS. Just push the files and host them.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Landing page (hero, about, hours & location, contact) |
| `hiring.html` | "We're Hiring" page (open roles + how to apply) |
| `styles.css` | Shared styles (dark/charcoal + cream/gold brand theme) |
| `404.html` | Custom not-found page |
| `assets/logo.svg` | Full logo + wordmark |
| `assets/mark.svg` | Icon-only mark (used as favicon) |
| `CNAME` | Custom domain for GitHub Pages (`kaffeinecanada.com`) |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |

## Deploy — GitHub Pages

1. Create a new repo on GitHub (e.g. `kaffeine-site`).
2. Push these files to the `main` branch (see commands below).
3. Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → **Save**.
4. Under **Settings → Pages → Custom domain**, enter `kaffeinecanada.com` and Save (the `CNAME` file already sets this).
5. Tick **Enforce HTTPS** once the certificate is issued (can take a few minutes).

### Push from your computer

```bash
cd path/to/Kaffeine
git init
git add .
git commit -m "Initial Kaffeine website"
git branch -M main
git remote add origin https://github.com/<your-username>/kaffeine-site.git
git push -u origin main
```

## DNS — Cloudflare

Point the domain at GitHub Pages. In the Cloudflare dashboard for `kaffeinecanada.com` → **DNS**:

**Apex (kaffeinecanada.com)** — add four `A` records to GitHub's IPs:

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**www** — add a `CNAME`:

| Type | Name | Value |
|------|------|-------|
| CNAME | www | `<your-username>.github.io` |

> Set these records to **DNS only** (grey cloud) first while GitHub provisions the SSL cert. You can switch to **Proxied** (orange cloud) afterward if you want Cloudflare's CDN/caching.

### Redirect the `.ca` domain to `.com`

In Cloudflare, on the `kaffeinecanada.ca` zone, add a **Redirect Rule** (Rules → Redirect Rules):
- When incoming requests match: Hostname equals `kaffeinecanada.ca` (and `www.kaffeinecanada.ca`)
- Then: Static redirect → `https://kaffeinecanada.com` → Status **301**, preserve path/query.

## Editing content

- **Hours**, **address**, **phone**, **email** live in `index.html` — search for the text and edit inline.
- **Open roles** live in `hiring.html` inside the `.role` blocks — duplicate a block to add a role, delete one to remove.
- Colors and fonts are all in `styles.css` under `:root`.
