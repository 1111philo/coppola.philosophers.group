# coppola.philosophers.group

Landing page for **The 11:11 Philosopher’s Hôtel**: New Orleans, November 10–15, a limited NOAI edition for the [NOAI Arts & Ideas Festival](https://noai.philosophers.group/).

One static page with no build step and no JavaScript. Open `index.html` or serve the folder:

```sh
python3 -m http.server
```

## Hosting

Served by GitHub Pages from `main` at the repo root, like `noai.philosophers.group`.
`CNAME` sets the custom domain, and DNS has `coppola` as a CNAME to `1111philo.github.io`.
Asset paths are relative, so the page also works at the `1111philo.github.io/coppola.philosophers.group/` project URL.

## Booking link

The **Book a room** button is in `index.html`. Search for `book-a-room` and
replace the placeholder `href` with the real booking page, form, or `mailto:`.

## What loads

| File | Size | Notes |
| --- | --- | --- |
| `index.html` | ~6 KB gzipped | All CSS is inline. The filigree frame, crest and medallion are inline SVG. |
| `assets/portrait.avif` | ~10 KB | WebP (16 KB) and JPEG (21 KB) fallbacks via `<picture>` |
| `assets/cinzel.woff2` | ~16 KB | Latin subset, weights 400–700 |
| `assets/retreat-display.woff2` | ~3 KB | Cinzel Decorative, cut down to the title glyphs only |

Body text uses the system's book serif (Palatino, Iowan, Georgia), so it needs no font download.
`assets/og.jpg` is used only for link previews and is never loaded by the page.

If you change the headline, "Limited NOAI Edition" or the Ada Lovelace nameplate, regenerate the display subset:

```sh
pyftsubset CinzelDecorative-Bold.woff2 --text="The 11:11 Philosopher’s Hôtel'Limited NOAI Edition Ada Lovelace" \
  --flavor=woff2 --output-file=assets/retreat-display.woff2
```

## Accessibility

- Semantic landmarks, a single `h1`, real text everywhere. Capitals come from CSS, not the source.
- The portrait has descriptive alt text. Decorative SVG is `aria-hidden`.
- Dark ink on silver is ≥ 6:1 contrast. The button label is ~15:1.
- The button is at least 56px tall and has a high-contrast focus ring.
- Reflows down to 320px wide (400% zoom) with no horizontal scrolling.
- Handles `prefers-reduced-motion` and Windows High Contrast (`forced-colors`).
- Passes axe-core (WCAG 2.2 AA and best practices) with no violations.
