# Feedly for FreshRSS

A dark [FreshRSS](https://freshrss.org) theme that borrows Feedly's look and
feel: real Feedly color tokens, self-hosted Inter type, larger rounded
thumbnails, and article rows restructured to read like Feedly's list view
(bold-until-read titles, byline, excerpt) instead of FreshRSS's classic
colored-sidebar-tree layout.

![list view](screenshots/list-view.png)
![reading pane](screenshots/reader-view.png)

> Screenshots above are from a live install — add your own if you fork this
> (see [Screenshots](#screenshots) below).

## Why this looks like Feedly, specifically

The palette isn't eyeballed — it's pulled from Feedly's own shipped CSS
(`feedly.com`'s `main.*.css` bundle exposes `--semanticColorBackground*` /
`--semanticColorBorder*` custom properties for both its light and dark
themes), and the type is Feedly's actual font: **Inter**, self-hosted here
as the variable font so there's no external request to a CDN.

## Features

- Dark palette matching Feedly's real tokens (`#121212` base, `#2bb24c`
  accent green, layered `#1a1a1a`/`#202020`/`#262626`/`#333333` surface
  levels).
- Self-hosted `InterVariable` (roman + italic), the same font Feedly ships.
- Article rows restructured: rounded ~108px thumbnails (up from FreshRSS's
  default 80px), title/byline/excerpt stacked instead of absolutely
  positioned, unread titles bold and full-brightness, read titles dimmed —
  mirroring how Feedly signals read state instead of a colored border.
- Rounded, ghost-style icon buttons in the toolbar and header; pill-shaped
  search box.
- Sidebar nav with rounded active/hover pills.
- Reading pane rendered as an elevated rounded card with a comfortable
  measure instead of edge-to-edge text.
- Muted (not alarm-red) styling for FreshRSS's real feed-error indicator,
  so it stays informative without shouting.

## Requirements

- FreshRSS 1.29+ (developed/tested against 1.29.1; should work on nearby
  versions since it only relies on documented theme hooks).
- FreshRSS's built-in **Origine** theme must be present (it ships by
  default with every FreshRSS install) — this theme layers on top of it
  rather than redefining structural CSS from scratch.

## Installation

FreshRSS themes are just a folder under `FreshRSS/p/themes/<Name>/` picked
up from `metadata.json`. Pick whichever install method matches your setup.

### Plain install

1. Copy (or clone) this repository's contents into
   `FreshRSS/p/themes/Feedly/` inside your FreshRSS install, e.g.:
   ```sh
   git clone https://github.com/<you>/freshrss-feedly-theme.git \
     /path/to/FreshRSS/p/themes/Feedly
   ```
2. Make sure the files are readable by your web server user (commonly
   `www-data`):
   ```sh
   chown -R www-data:www-data /path/to/FreshRSS/p/themes/Feedly
   ```
3. In FreshRSS, go to **Settings → Display** and pick **Feedly** as the
   theme.

### Docker (bind mount, survives image updates)

If FreshRSS runs in Docker and you don't want the theme to disappear the
next time the container is recreated (e.g. on an image update), clone this
repo to a persistent path on the host and bind-mount it over the theme
directory instead of copying into the container's writable layer:

```sh
git clone https://github.com/<you>/freshrss-feedly-theme.git \
  /path/to/persistent/theme-feedly
```

Add a volume to your `docker run` / compose file:

```
-v /path/to/persistent/theme-feedly:/var/www/FreshRSS/p/themes/Feedly
```

then recreate the container so the mount takes effect. Select **Feedly**
under **Settings → Display** as above.

## Recommended FreshRSS settings

The theme scales to whatever's configured, but a couple of FreshRSS's own
settings (under **Settings → Reading**) get you closer to Feedly's actual
layout:

- **Display an excerpt of the article** (`topline_summary`) — off by
  default in FreshRSS; turning it on is what makes the gray preview text
  under each title appear (this is a FreshRSS content setting, not
  something the theme can turn on by itself). Note some feeds simply don't
  publish a description in their RSS, so a few entries may still show no
  excerpt regardless of this setting.
- **Thumbnail shape** (`topline_thumbnail`) — set to **Landscape** for the
  closest match. The theme's default sizing (163×98) is Feedly's actual
  magazine-view thumbnail dimension, captured from its own image-resize
  CDN request; Square/Portrait are scaled proportionally from the same
  baseline if you prefer those instead.

## Known limitations

- **Dark only.** There's no light variant yet. The theme forces a dark
  palette regardless of FreshRSS's `darkMode` setting or OS preference.
- **No RTL stylesheet.** FreshRSS falls back to requesting
  `feedly.rtl.css` for right-to-left languages, which this theme doesn't
  ship; RTL users will get an unstyled/missing stylesheet for the
  theme-specific layer. Contributions welcome.
- Sidebar/toolbar icon glyphs are FreshRSS's own icon set (recolored via
  CSS filters), not Feedly's actual iconography — a pixel-exact icon set
  swap was out of scope.

## Screenshots

Add your own under `screenshots/` and reference them from the top of this
README (`list-view.png`, `reader-view.png` are just suggested names).

## Credits

- Color tokens sourced from Feedly's own production CSS
  (`feedly.com` / `s1.feedly.com`).
- [Inter](https://rsms.me/inter/) by Rasmus Andersson and the Inter
  Project Authors, licensed under the
  [SIL Open Font License 1.1](fonts/LICENSE-OFL.txt).
- Built on top of FreshRSS's **Origine** theme by Marien Fressinaud, and
  the **Dark**/**Nord** community themes, which this theme's layering
  approach (`_frss.css` → `Origine/origine.css` → theme CSS) follows.
- [FreshRSS](https://freshrss.org) itself.

## License

This theme's original code (`feedly.css`, `metadata.json`, this README) is
licensed under the [MIT License](LICENSE).

The bundled font (`fonts/InterVariable*.woff2`) is licensed separately
under the [SIL Open Font License 1.1](fonts/LICENSE-OFL.txt) — it is
**not** MIT, and that license text must stay with the font files if you
redistribute them.

Feedly itself, its name, and its trademarks are the property of their
respective owners; this project is an independent, unaffiliated fan theme
and is not endorsed by or affiliated with Feedly.
