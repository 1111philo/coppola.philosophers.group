# coppola.philosophers.group

Landing page for **Hôtel 11:11**: New Orleans, November 10–15, a limited NOAI edition for the [NOAI Arts & Ideas Festival](https://noai.philosophers.group/).

One static page with no build step and no JavaScript. Open `index.html` or serve the folder:

```sh
python3 -m http.server
```

## Hosting

Served by GitHub Pages from `main` at the repo root, like `noai.philosophers.group`.
`CNAME` sets the custom domain, and DNS has `coppola` as a CNAME to `1111philo.github.io`.
Asset paths are relative, so the page also works at the `1111philo.github.io/coppola.philosophers.group/` project URL.

## Booking (Stripe Payment Links)

Each room card has its own **Book** button that opens a Stripe Payment Link from the
11:11 Philosopher’s Stripe account. The hero’s **Choose a room** button only scrolls down to the rooms.

Every room is sold as one package for the full stay, November 10–15, at 4 × the nightly rate:

| Room | Package price | Placeholder in `index.html` |
| --- | --- | --- |
| Don Ciccio Suite | $1,332.00 | `REPLACE_DON_CICCIO` |
| Kurosawa Apartment | $2,220.00 | `REPLACE_KUROSAWA` |
| Artist Outcoves (2 rooms) | $888.00 each | `REPLACE_ARTIST_OUTCOVE` |
| Dracula’s Attic | $842.40 | `REPLACE_DRACULA` |

To set them up, in the Stripe Dashboard (Payment Links → New):

1. Create one product per room with a one-time price matching the table, and mention
   VIP access to the NOAI Festival and parties in the description.
2. Turn on "Collect customers’ names" and phone number so you know who is arriving.
3. Limit each link to the number of rooms you have: 1 for most, 2 for Artist Outcoves.
   Stripe can deactivate a link after a set number of completed payments.
4. Replace each `https://buy.stripe.com/REPLACE_…` href with the link Stripe gives you.

## What loads

| File | Size | Notes |
| --- | --- | --- |
| `index.html` | ~6 KB gzipped | All CSS is inline. The filigree frame, crest and medallion are inline SVG. |
| `assets/portrait.avif` | ~10 KB | WebP (16 KB) and JPEG (21 KB) fallbacks via `<picture>` |
| `assets/cinzel.woff2` | ~16 KB | Latin subset, weights 400–700 |
| `assets/retreat-display.woff2` | ~3 KB | Cinzel Decorative, cut down to the title glyphs only |

Body text uses the system's book serif (Palatino, Iowan, Georgia), so it needs no font download.
`assets/og.jpg` is used only for link previews and is never loaded by the page.

If you change the headline, "Limited NOAI Edition", the Ada Lovelace nameplate or the room names, regenerate the display subset:

```sh
pyftsubset CinzelDecorative-Bold.woff2 --text="Hôtel 11:11 Limited NOAI Edition Ada Lovelace Rooms Don Ciccio Suite Kurosawa Apartment Artist Outcoves Dracula’s Attic" \
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
