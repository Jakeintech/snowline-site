# snowline-site

Public website for **Snowline**, a calm, clever ski-resort builder for iPhone and iPad.
*A little mountain. A thousand possibilities.*

Live at <https://jakeintech.github.io/snowline-site/> (GitHub Pages, from `main` /).

| Page | URL |
|---|---|
| Home | `/` |
| Press kit | `/press.html` |
| Support and FAQ (App Store support URL) | `/support.html` |
| Privacy Policy (App Store privacy URL) | `/privacy-policy.html` |
| Terms of Use | `/terms-of-service.html` |

Keep the support and privacy URLs exactly as they are: App Store Connect points at them.

## How it is built

Plain HTML and one stylesheet (`assets/site.css`). No build step, and no third-party requests of any kind: fonts and images are served from this repo, and there are no analytics, cookies or CDNs.

- **Type:** Young Serif (display) and Figtree (text), self-hosted as woff2 in `assets/fonts/` with their SIL Open Font License texts.
- **Colour:** the art kit's palette: ivory `#F8F8F0`, evergreen `#244C45`, glacier `#8EC9E5`, mint `#A6DCAA`, alpine blue `#6EAAE8`, amber `#F4C673`, with deeper tints for text so every pairing meets WCAG AA. Light and dark themes follow `prefers-color-scheme`.
- **Accessibility:** skip link, landmarks, alt text, 44 px targets, visible focus, AA contrast in both themes, trail markers by shape as well as colour, smooth scrolling only without `prefers-reduced-motion`. Mobile first: no horizontal scroll at 375 px.
- **Images:** chapter art as WebP (768 and 1536 px, `srcset`), icons as PNG, every `img` with `width` and `height`.
- **Honesty:** the copy describes the planned 1.0 in the same terms as the App Store listing (`appstore/listing.json` in the game repo). The five paintings are the Journey's chapter art and are always captioned that way, never as captures of play. Screenshots and a trailer arrive with 1.0.

## What is generated

`scripts/publish_site.py` in the Snowline repo (`~/Developer/GitHub/Snowline`) writes these files; edit the sources there, not the outputs here:

| Output here | Source in the Snowline repo |
|---|---|
| `assets/img/icon-512.png`, `icon-192.png`, `apple-touch-icon.png`, `favicon.png` | `Snowline/Resources/Assets.xcassets/AppIcon.appiconset/icon-1024.png` |
| `assets/press/snowline-icon[-dark\|-tinted]-{1024,512}.png` | the same folder's `icon-1024.png`, `icon-1024-dark.png`, `icon-1024-tinted.png` |
| `assets/press/snowline-logo-on-{ivory,evergreen}.png` | the icon plus the wordmark, drawn in Young Serif from `assets/fonts` |
| `assets/img/art/<mountain>-{768,1536}.webp`, `assets/press/snowline-chapter-<mountain>.jpg` | `art-source/Snowline_Asset_Kit_v2/maps/*.png` |
| `assets/img/og.png` (1200 x 630) | `appstore/marketing/social/link-preview-1200x630.png` when it exists, otherwise a card drawn from the icon and chapter art |
| `assets/listing.json` | `appstore/listing.json` (public copy only) |
| `assets/img/shots/*.webp` | `appstore/screenshots/final/` (only with `--with-screenshots`; deleted otherwise) |

It also rewrites the text between these marker comments. Everything outside them is edited here by hand.

| Marker | Page | Contents |
|---|---|---|
| `<!-- promo -->` | index | hero paragraph: the listing's promotional text, minus the tagline |
| `<!-- ld -->` | index | JSON-LD `VideoGame` (adds `downloadUrl` with `--store-live`) |
| `<!-- screenshots -->` | index | the five mountains with their chapter art; with `--with-screenshots`, the screenshots come first |
| `<!-- press-copy -->` | press | one-line, short and long descriptions from the listing |
| `<!-- press-mountains -->` | press | the five mountains with full-size downloads |
| `<!-- appmeta -->` | every page | empty, or `<meta name="apple-itunes-app" content="app-id=6834599728">` with `--store-live` |
| `<!-- store-cta -->` | index (twice) | "Coming soon to the App Store", or "Download on the App Store" with `--store-live` |
| `<!-- store-release -->` | press | the Release line of the fact sheet |

The mountain names, captions and alt text live in `MOUNTAINS` in `publish_site.py`.

## Publishing

From the Snowline repo:

```bash
scripts/publish-site.sh                  # regenerate here, show git status (never pushes)
scripts/publish-site.sh --push           # ...then commit and push to origin main
fastlane site                            # the same, through fastlane (store_live:true, with_screenshots:true, push:true)
```

`--push` refuses to run unless this repo is on `main`, so a branch cannot be published by accident. To publish a branch, merge it first:

```bash
git switch main
git merge --ff-only release/site-refresh   # or open a pull request
git push origin main                       # or: scripts/publish-site.sh --push from the Snowline repo
```

### Launch day

Once Snowline is live on the App Store (id 6834599728):

```bash
scripts/publish-site.sh --store-live             # review: git -C ../snowline-site diff
scripts/publish-site.sh --store-live --push
```

From then on pass `--store-live` on every run; without it the site goes back to "Coming soon" (the script warns when that is about to happen). When screenshots of the shipping interface exist, add `--with-screenshots`, and update the "Screenshots and trailer" note on `press.html` by hand.

## Contact

info@jakeawilliams.com
