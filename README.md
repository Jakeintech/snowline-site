# snowline-site

Public website for **Snowline**, a calm, strategic ski-resort game for iPhone and iPad.
*A little mountain. A thousand possibilities.*

Live at <https://jakeintech.github.io/snowline-site/> (GitHub Pages, from `main` /).

| Page | URL |
|---|---|
| Home | `/` |
| Privacy Policy (App Store privacy URL) | `/privacy-policy.html` |
| Support and FAQ (App Store support URL) | `/support.html` |
| Terms of Use | `/terms-of-service.html` |

## How it is built

Plain HTML and one stylesheet (`assets/site.css`), no build step and no third-party requests.

- **Type:** Young Serif (display) and Figtree (text), self-hosted as woff2 in `assets/fonts/` with their SIL Open Font License texts.
- **Colour:** the game's palette (evergreen, glacier blue, ivory snow, lavender shadow, amber, coral, sunset peach, twilight navy). Light and dark themes follow `prefers-color-scheme`.
- **Accessibility:** skip link, landmarks, 44 pt targets, AA contrast in both themes, trail markers by shape as well as colour, and the hero illustration's animation stops under `prefers-reduced-motion`.

## Updating it from the game repo

Generated files come from the Snowline repo (`~/Developer/GitHub/Snowline`):

```bash
scripts/publish-site.sh            # copy, regenerate, show git status here (never pushes)
scripts/publish-site.sh --push     # ...and commit + push to main
fastlane site                      # capture + frame screenshots, then publish-site.sh
```

It writes:

- `assets/img/icon-512.png`, `icon-192.png`, `apple-touch-icon.png`, `favicon.png`, `og.png` from `docs/press/icon.png`
- `assets/img/shots/*.webp` — the first four framed App Store screenshots, and the block between `<!-- screenshots:start -->` and `<!-- screenshots:end -->` in `index.html` (until screenshots exist, that block holds an SVG illustration of the mountain, not a fake screenshot)
- `assets/listing.json` and the hero paragraph between `<!-- promo:start -->` and `<!-- promo:end -->`, from `appstore/listing.json`

Everything else (copy, layout, the other pages) is edited here by hand.

## Contact

info@jakeawilliams.com
