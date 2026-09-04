# Changelog

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
