# Changelog

## 1.1.1 — 2026-09-04

- Removed the row-separator lines in the article list: the horizontal
  one (this theme's own `border-top` between rows) and a vertical one
  between the thumbnail and title that didn't trace back to any rule
  this theme, Origine, or frss.css set — reset border/outline broadly
  on the row's flex items rather than leave the source unexplained.

## 1.1.0 — 2026-09-04

- **Renamed the theme from "Feedly" to "Freedly"** (folder, CSS filename
  `feedly.css` → `freedly.css`, `metadata.json` name field, install
  paths) to be clear this is an independent fan theme, not the actual
  Feedly product — the README now states that explicitly.
- Added the `thumbs/original.png` preview image FreshRSS's theme picker
  (Settings → Display) expects — previously missing entirely. It's a
  placeholder card for now; see the Screenshots section of the README.
- Rewrote the README's install instructions around FreshRSS's own
  theming docs and Docker guidance, including the official warning that
  custom themes can be overwritten on update, and documented the
  official `make rtl` / CSSJanus path for anyone who wants to contribute
  an RTL stylesheet (not shipped yet).
- Fixed version drift: `metadata.json`'s `version` field on the live
  install had been stuck at the initial `1.0` release value since 1.0.1
  — each release since had bumped it in this repo but never re-deployed
  that specific file. Now in sync.

## 1.0.8 — 2026-09-04

- Suppressed the underline that appeared on a sidebar feed/category link
  on hover (the browser's default `a:hover` behavior, inherited since
  nothing overrode it for the tree). Feedly's sidebar signals hover with
  its background pill alone; sidebar rows now do the same.

## 1.0.7 — 2026-09-04

- Sidebar feed list toned down to match Feedly's more restrained look:
  feed rows now default to regular weight and a dimmer secondary text
  color, brightening to full text color + medium weight only on hover
  and for the active feed/category. Previously every row rendered at
  the same bold/bright weight regardless of selection state.

## 1.0.6 — 2026-09-04

- Removed green from all link/body text (generic `a` links, in-article
  content links, the header wordmark hover, the mark-read footer hover).
  Feedly reserves its accent green for controls — buttons, badges, focus
  rings, the unread dot — not for text. Links now render in the same
  neutral tone as body text; in-article content links pick up an
  underline so they stay discoverable now that they're not color-coded.

## 1.0.5 — 2026-09-04

- Moved the read/favorite-toggle icons and favicon from the start of
  each article row to the end (after the title/byline/excerpt block),
  matching where Feedly places its per-entry action icons. Required
  switching the row from FreshRSS's default CSS table layout to flex so
  `order` could move them without touching PHP templates; thumbnail and
  title stay first, everything else falls in after in its existing
  relative order.

## 1.0.4 — 2026-09-04

- Fixed: favicons could render squished/stretched into a thin sliver
  after 1.0.3's column-width tightening. Locked `img.favicon` to an
  explicit 16×16px box with `object-fit: contain` so it can't distort
  regardless of the surrounding cell width.

## 1.0.3 — 2026-09-04

- Tightened the read/favorite-toggle icons and the favicon column in the
  article list — FreshRSS's default ~40px-wide cells for these left
  visible gaps between them; narrowed to a snug Feedly-style cluster.

## 1.0.2 — 2026-09-04

- Hid the category-level ⚠ error marker (shown on a folder like "Apple"
  when any feed inside it is broken) while keeping the per-feed marker
  (shown directly on the actual broken feed, e.g. "Redmond Pie") intact.
  FreshRSS renders these via two independent selectors, so this was a
  matter of targeting the folder-level one specifically.

## 1.0.1 — 2026-09-04

- Thumbnails re-sized to Feedly's actual dimensions: 163×98 (landscape),
  scaled proportionally for the square/portrait variants and their
  `.small` counterparts. Previous release used a guessed 108px square;
  this one is sourced from Feedly's own image-resize CDN request
  (`visuals.feedly.com/v1/resize?sizes=163x98!0.8`), captured from a
  saved copy of a live Feedly page's DOM.
- README now recommends the `landscape` thumbnail-shape setting (under
  Settings → Reading) to actually get that crop — `square` can't produce
  it regardless of CSS sizing.

## 1.0.0 — 2026-09-04

Initial release.

- Dark palette built from Feedly's real shipped color tokens.
- Self-hosted `InterVariable` (roman + italic).
- Article list rows restructured (thumbnail, title, byline, excerpt
  stacked; bold-until-read titles instead of a colored left border).
- Thumbnails scaled up (~108px, all shape variants) to match Feedly's
  larger imagery.
- Rounded ghost-style toolbar/header buttons, pill search box, rounded
  sidebar nav.
- Reading pane rendered as an elevated card.
- Fixed: unread/starred rows no longer draw Origine's default colored
  left border (was rendering as one continuous vertical line down the
  article list).
- Fixed: feed favicons no longer forced onto a white background box.
- Muted the built-in feed-error indicator from alarm-red to a softer
  amber so it stays legible without dominating the sidebar.
