# Changelog

## 1.2.0 — 2026-09-04

- Article panel (normal/list view) now slides in from the right instead
  of expanding inline as an accordion, Feedly-style. Achieved with no
  custom JS: overrode frss.css's `display:none` on collapsed
  `.flux_content` to keep it in the DOM off-screen via `transform`
  instead, so FreshRSS's own existing click/close logic (click a row,
  click a different row, click the article's margin if "close article
  by clicking its sides" is enabled) now drives a real slide-in panel.
  Enabled that "sides_close_article" setting as part of this, since the
  panel needs it to be closable by clicking its own padding.
- Known limitation: no dedicated close (✕) button like Feedly's -
  closing relies on the interactions above. A real X button would need
  this theme to ship a small JS file (FreshRSS supports that per its
  theme-writing docs); noted as a possible follow-up, not done here.

## 1.1.5 — 2026-09-04

- Article title sizing measured directly from Feedly's DevTools Computed
  panel rather than approximated: 16px at weight 650 (InterVariable's
  fractional weight, not just 600/700) for the unread/current state, up
  from a guessed 0.95rem/600. First theme value backed by an actual
  computed-style reading instead of screenshot proportions.

## 1.1.4 — 2026-09-04

- Sidebar unread-count numbers sized down to 0.75rem, distinctly smaller
  than the feed/category label next to them (Feedly's counts are subtle,
  not label-sized). frss.css had them fixed at 0.9rem, which read as
  merely fine against the old 1rem category titles but became oversized
  once 1.1.3 sized those titles down to 0.85rem.

## 1.1.3 — 2026-09-04

- Sidebar type sized down to match Feedly's more compact scale.
  Category-folder titles (`.tree-folder-title`) shipped from base.css
  at 1rem with a loose 2.5 line-height; sized to 0.85rem/1.8 with
  tighter vertical padding. Feed rows (already 0.8rem via Origine)
  got a trimmed line-height (1.7 → 1.5) to match the tighter rhythm.
  Sidebar icons and favicons scaled down proportionally so they don't
  look oversized against the smaller text.

## 1.1.2 — 2026-09-04

- Actually fixed the horizontal line between article rows this time.
  1.1.1 removed this theme's own `border-top` on `.flux_header`, but
  missed that Origine sets the exact same declaration directly on that
  selector too — so the line never actually went away, just lost its
  redundant second source. Explicitly overridden now.

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
