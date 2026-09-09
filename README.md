# bitstyle.co.uk

Static one-page site for **BitStyle.co.uk**. No build step, no dependencies —
plain HTML, CSS and a small amount of vanilla JS, deployed straight from this
repo by Cloudflare Pages.

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | The whole site — hero, about, contact |
| `styles.css` | All styling. Brand colours live in the `:root` block at the top |
| `main.js` | Sticky header, mobile nav, scroll reveals, section highlighting |
| `404.html` | Not-found page (Cloudflare Pages serves this automatically) |
| `_headers` | Security headers + cache policy for Cloudflare Pages |
| `robots.txt`, `sitemap.xml` | Search-engine basics |
| `assets/` | Logos, chevron mark, social share image |
| `favicon.ico`, `favicon-32.png`, `apple-touch-icon.png` | Icons |

## Brand

Both blues are sampled straight from the logo artwork:

| Token | Value | Use |
| --- | --- | --- |
| `--blue` | `#29abe2` | Bright accent, links, icons |
| `--blue-deep` | `#0071bc` | Gradient end, deep accent |
| `--bg` | `#080b10` | Page background |

`assets/bitstyle-logo.png` is the original artwork (black wordmark, for light
backgrounds). `assets/bitstyle-logo-dark.png` is a recoloured variant with a
white "Bit" for use on the dark site. Regenerate the dark variant from new
artwork by inverting only the low-saturation (black) pixels and leaving the
blues untouched.

## Deploying with Cloudflare Pages

1. Push this repo to GitHub.
2. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** →
   **Connect to Git**, and pick this repository.
3. Build settings:
   - **Framework preset:** `None`
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
4. Deploy. Then **Custom domains** → add `bitstyle.co.uk` and `www.bitstyle.co.uk`.
   Cloudflare creates the DNS records itself if the zone is already on your account.
5. Recommended once live: **Rules → Redirect Rules** to send `www` → apex (or the
   reverse), and **SSL/TLS → Edge Certificates → Always Use HTTPS: On**.

Every push to `master` redeploys. Pull requests get their own preview URL.

## Local preview

Just open `index.html` in a browser — asset paths in `index.html` are
document-relative, so it works straight off the filesystem over `file://`.

For a closer match to production (correct MIME types, absolute paths, the 404
page):

```sh
python3 -m http.server 8787
# http://localhost:8787
```

Note that `404.html` uses **root-relative** paths on purpose. Cloudflare Pages
serves it at whatever URL was requested, so relative paths would resolve
against the wrong directory. It therefore looks unstyled over `file://` — check
it through the local server instead.

## Content to personalise

Search the source for `EDIT:` — there are two spots:

- `index.html` → the two **About** paragraphs, which are written generically and
  should be replaced with your own background.
- `index.html` → the commented-out footer block. If BitStyle trades as a limited
  company, the Companies Act 2006 requires the registered company name, company
  number, registered office and (if registered) VAT number on the website.

If you change the tagline or email, update them in the `<meta>` description,
the JSON-LD block and `assets/og-image.png` too.
