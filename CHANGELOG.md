# Changelog

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
