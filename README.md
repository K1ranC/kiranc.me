# kiranc.me

Personal site for Kiran Chandra — Senior Security Operations Engineer.

## Design principles

- **Zero JavaScript.** The site is hand-written HTML and CSS. Nothing executes in the visitor's browser.
- **Zero dependencies.** No framework, no build step, no `node_modules` — no supply chain to patch.
- **Zero third-party requests.** System font stacks, self-hosted assets. Visitors talk to one origin.
- **Strict headers.** `default-src 'none'`-based CSP, HSTS (preload-ready), `frame-ancestors 'none'`,
  `Referrer-Policy: no-referrer`, COOP/CORP — configured in [`vercel.json`](vercel.json).
- **[RFC 9116](https://www.rfc-editor.org/rfc/rfc9116)** `security.txt` at `/.well-known/security.txt`.

## Structure

```
public/            deployed site root
  index.html       the site (single page)
  404.html         custom not-found page
  styles.css       all styling
  favicon.svg
  robots.txt
  badges/          self-hosted credential badge artwork
  .well-known/security.txt
vercel.json        security headers + static config
```

## Local development

No toolchain required:

```sh
python3 -m http.server 8000 --directory public
```

## Deploy

Hosted on Vercel, deployed from this git repo. Pushes to `main` go to production
at [kiranc.me](https://kiranc.me); every branch gets a preview URL.

Note: `python3 -m http.server` does not send the security headers — those are
applied by Vercel from `vercel.json`. Verify with `curl -sI https://kiranc.me`.
