# cert.patata.mt

Static, single-page site for PATATA CERT Malta, hosted on GitHub Pages. It has no build step and no framework, deliberately: plain HTML/CSS is served as-is, so there is nothing to update or break. If the site grows (advisories, blog), move to Astro or Eleventy deployed via GitHub Actions rather than Jekyll. The visual rules come from the CERT-Patata brand kit (`brand/tokens.json`).

```
index.html                 the page
404.html                   GitHub Pages serves this for missing paths
assets/css/site.css        styles (colour tokens at the top)
assets/fonts/              Inter variable font (woff2) + OFL licence
assets/img/                logo derivatives (resized only) + og.png social card
.well-known/security.txt   RFC 9116 disclosure contact
CNAME                      custom domain for GitHub Pages
.nojekyll                  serve files as-is (needed for .well-known)
robots.txt, sitemap.xml, favicon-32.png, apple-touch-icon.png
```

## Before going live

- [ ] Make sure `security@patata.mt` is live and monitored. It is the only address on the site (incidents, enquiries, briefings and security.txt); subject lines tell them apart.
- [ ] Confirm the certification line in the Services section is accurate for the team.
- [ ] Renew `Expires` in `.well-known/security.txt` before 30 Oct 2027. Optionally add an `Encryption:` line pointing to a PGP key.

## Publish on GitHub Pages

1. Create a repository, for example `cert-patata-site`. Pages is free for public repositories; a private repository needs a paid plan.
2. Push this folder to `main`:
   ```sh
   git init && git add . && git commit -m "cert.patata.mt site"
   git branch -M main
   git remote add origin git@github.com:<account>/cert-patata-site.git
   git push -u origin main
   ```
3. Go to **Settings → Pages → Build and deployment**. Set the source to **Deploy from a branch**, with branch `main` and folder `/ (root)`.
4. Under **Custom domain**, enter `cert.patata.mt`. The `CNAME` file already contains it.

## DNS for patata.mt

| Type  | Name   | Value                  |
|-------|--------|------------------------|
| CNAME | `cert` | `<account>.github.io.` |

- Point the record at the account or organisation host. Do not include the repository name.
- Protect against subdomain takeover by verifying the domain in GitHub. Go to **Account (or Org) settings → Pages → Add a domain**, then add the TXT record GitHub shows, `_github-pages-challenge-<account>.patata.mt`.
- Once DNS resolves and the certificate is issued, tick **Enforce HTTPS** in the Pages settings.

## Local preview

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Root-relative paths (`/assets/...`) assume the site is served at a domain root. They work locally and on `cert.patata.mt`, but not at `<account>.github.io/<repo>/`.
