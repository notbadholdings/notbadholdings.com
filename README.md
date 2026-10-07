# notbadholdings.com

The landing page and legal information for Not Bad Holdings. Static HTML, no build step, no
external requests — open `index.html` in a browser and it works.

```
index.html                     markup + meta
legal-info/index.html          company details at /legal-info/
styles.css                     tokens, wordmark, layout
assets/
  icon-128.png                 favicon / apple-touch-icon
  nbh-badge-ink.png            og:image (the wordmark on ink)
  fonts/*.woff2                IBM Plex Mono 400 + 500, latin & latin-ext
CNAME                          custom domain for GitHub Pages
.nojekyll                      serve files as-is, skip Jekyll processing
```

## Editing

The three pieces of copy are plain text in `index.html`: the jurisdiction in
`<header>`, the line in `<p class="line">`, and the contact address in
`<footer>`. Colours are custom properties at the top of `styles.css` —
`--accent` is the lime on "bad".

The wordmark tracks each row out to a shared measure so "not", "bad" and
"holdings" stack flush on both edges. Its metrics are all derived from
`--measure`, so changing that one value rescales the whole mark.

## Preview

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

## Deploying

GitHub Pages serves this repo's root on the `main` branch. Push to `main` and
the live site updates a minute or so later — there is nothing to compile.

The custom domain is set by the `CNAME` file. It requires these DNS records at
the registrar for `notbadholdings.com`:

```
A     @   185.199.108.153
A     @   185.199.109.153
A     @   185.199.110.153
A     @   185.199.111.153
AAAA  @   2606:50c0:8000::153
AAAA  @   2606:50c0:8001::153
AAAA  @   2606:50c0:8002::153
AAAA  @   2606:50c0:8003::153
CNAME www notbadholdings.github.io.
```

GitHub issues the TLS certificate only once those resolve; "Enforce HTTPS"
in Settings → Pages becomes available at that point.

Two absolute URLs assume the site is served from `https://notbadholdings.com/`:
`<link rel="canonical">` and `og:image`. Update both if that changes.

## Notes

- `og:image` is 408×400, so link previews render as a square card rather than
  a wide banner. A 1200×630 version would upgrade that if you want it.
- Fonts are IBM Plex Mono, self-hosted under the SIL Open Font License 1.1.
  Only the latin and latin-ext subsets ship; the page never renders Cyrillic
  or Vietnamese.
