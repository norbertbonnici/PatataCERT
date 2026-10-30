# cert.patata.mt

Website for **PATATA CERT Malta**, a digital forensics and incident response team based in Malta.

It's a single static page served by GitHub Pages. It uses plain HTML and CSS, with no framework and no build step.

## Structure

```
index.html                 the page
404.html                   not-found page
assets/css/site.css        styles (colour tokens at the top)
assets/fonts/              Inter variable font + OFL licence
assets/img/                logo and social card
.well-known/security.txt   RFC 9116 security contact
CNAME                      custom domain
.nojekyll                  serve files as-is (required for .well-known)
```

## Local preview

```sh
python3 -m http.server 8000
```

Then open http://localhost:8000. Paths are root-relative, so the site has to be served from a domain root.

## Deployment

GitHub Pages deploys from `main`, folder `/ (root)`. The custom domain `cert.patata.mt` is a DNS `CNAME` record for `cert` that points to `norbertbonnici.github.io.`.

## Maintenance

- Renew `Expires` in `.well-known/security.txt` before 30 Oct 2027.
- Update `lastmod` in `sitemap.xml` when the page changes.

## Contact

security@patata.mt
