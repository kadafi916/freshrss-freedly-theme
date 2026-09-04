# Freedly

A Feedly-inspired dark theme for [FreshRSS](https://freshrss.org). Real
Feedly color tokens, self-hosted Inter type, larger rounded thumbnails,
and article rows restructured to read like Feedly's list view (bold-until-
read titles, byline, excerpt, action icons trailing the title) instead of
FreshRSS's classic layout.

> **Freedly is an independent, unaffiliated fan theme.** It is not
> endorsed by, affiliated with, or associated with Feedly in any way —
> the name is a nod to its inspiration, not a claim of association.
> Feedly and its trademarks belong to their respective owners.

![list view](screenshots/list-view.png)
![reading pane](screenshots/reader-view.png)

> Screenshots above are from a live install — add your own if you fork
> this (see [Screenshots](#screenshots) below).

## Why this looks like Feedly, specifically

The palette isn't eyeballed — it's pulled from Feedly's own shipped CSS
(`feedly.com`'s `main.*.css` bundle exposes `--semanticColorBackground*` /
`--semanticColorBorder*` custom properties for both its light and dark
themes), the thumbnail size is Feedly's actual image-resize CDN request
(163×98, captured from a saved Feedly page's live DOM), and the type is
Feedly's actual font: **Inter**, self-hosted here as the variable font so
there's no external request to a CDN.

## Features

- Dark palette matching Feedly's real tokens (`#121212` base, `#2bb24c`
  accent green reserved for controls only — buttons, badges, focus rings
  — never for link/body text, matching how Feedly actually uses it).
- Self-hosted `InterVariable` (roman + italic).
- Article rows restructured: rounded 163×98 thumbnails, title/byline/
  excerpt stacked instead of absolutely positioned, unread titles bold
  and full-brightness, read titles dimmed, and the read/favorite/favicon
  icons moved to trail the title instead of leading the row.
- Rounded, ghost-style icon buttons in the toolbar and header; pill-
  shaped search box.
- Sidebar nav toned to Feedly's restraint: rows default to a dimmer,
  regular-weight look and only brighten on hover or when active, rather
  than every row competing at the same weight.
- Reading pane rendered as an elevated card with a comfortable measure.
- Muted (not alarm-red) styling for FreshRSS's per-feed error indicator;
  the noisier folder-level summary indicator is hidden entirely while the
  per-feed one (which tells you exactly which feed is broken) stays.

## Requirements

- FreshRSS 1.29+ (developed/tested against 1.29.1; should work on nearby
  versions since it only relies on documented theme hooks).
- FreshRSS's built-in **Origine** theme must be present (it ships by
  default with every FreshRSS install) — this theme layers on top of it
  rather than redefining structural CSS from scratch, the same approach
  FreshRSS's own official Dark/Nord themes use.

## Installation

FreshRSS themes are a folder under `FreshRSS/p/themes/<Name>/` picked up
from a `metadata.json` inside it — see FreshRSS's own
[theming docs](https://freshrss.github.io/FreshRSS/en/admins/11_Themes.html)
and [theme-writing guide](https://freshrss.github.io/FreshRSS/en/developers/04_Frontend/02_Design.html)
for the general mechanism this follows.

> **FreshRSS's own docs note that custom themes aren't officially
> supported and can be overwritten when FreshRSS updates**, unless
> they live outside the path FreshRSS's own files get replaced from.
> Both install methods below account for that — the plain install by
> reminding you to keep a copy elsewhere, the Docker method by bind-
> mounting from outside the container entirely.

### Option A: plain install

1. Clone (or download and extract) this repository directly into
   `FreshRSS/p/themes/Freedly/`:
   ```sh
   git clone https://github.com/kadafi916/freshrss-freedly-theme.git \
     /path/to/FreshRSS/p/themes/Freedly
   ```
2. Make it readable by your web server user (commonly `www-data`):
   ```sh
   chown -R www-data:www-data /path/to/FreshRSS/p/themes/Freedly
   ```
3. In FreshRSS: **Settings → Display → Theme → Freedly**.
4. Keep the clone (or this repo) somewhere outside the FreshRSS install
   too, since an update could overwrite `p/themes/Freedly/` directly.

### Option B: Docker (bind mount, survives image updates)

Clone to a persistent path on the Docker **host** (not inside the
container), then bind-mount it over the theme directory instead of
copying into the container's writable layer — this is the pattern
[FreshRSS's own docs recommend](https://freshrss.github.io/FreshRSS/en/admins/11_Themes.html)
for Docker specifically:

```sh
git clone https://github.com/kadafi916/freshrss-freedly-theme.git \
  /path/to/persistent/theme-freedly
```

Add a volume to your `docker run` / compose file:

```sh
-v /path/to/persistent/theme-freedly:/var/www/FreshRSS/p/themes/Freedly
```

Recreate the container so the mount takes effect, then in FreshRSS:
**Settings → Display → Theme → Freedly**.

<details>
<summary>Full example <code>docker run</code> command</summary>

```sh
docker run -d --restart unless-stopped \
  -p 8080:80 \
  -v /path/to/freshrss/data:/var/www/FreshRSS/data \
  -v /path/to/freshrss/extensions:/var/www/FreshRSS/extensions \
  -v /path/to/persistent/theme-freedly:/var/www/FreshRSS/p/themes/Freedly \
  --name freshrss \
  freshrss/freshrss
```

Only the last `-v` line is specific to this theme — the rest is a
standard FreshRSS container; adapt paths/ports to your existing setup.
</details>

## Recommended FreshRSS settings

The theme scales to whatever's configured, but a couple of FreshRSS's own
settings (under **Settings → Reading**) get you closer to Feedly's actual
layout:

- **Display an excerpt of the article** (`topline_summary`) — off by
  default in FreshRSS; turning it on is what makes the gray preview text
  under each title appear (this is a FreshRSS content setting, not
  something the theme can turn on by itself). Some feeds simply don't
  publish a description in their RSS, so a few entries may still show no
  excerpt regardless of this setting.
- **Thumbnail shape** (`topline_thumbnail`) → **Landscape**. The theme's
  163×98 sizing is Feedly's actual magazine-view thumbnail dimension;
  Square/Portrait scale proportionally from the same baseline if you
  prefer those instead, but only Landscape reproduces Feedly's crop.

## Known limitations

- **Dark only.** There's no light variant yet. The theme forces a dark
  palette regardless of FreshRSS's `darkMode` setting or OS preference.
- **No RTL stylesheet.** FreshRSS falls back to requesting
  `freedly.rtl.css` for right-to-left languages, which this theme
  doesn't ship. FreshRSS's own theme-writing guide recommends generating
  RTL variants with [CSSJanus](https://github.com/cssjanus/cssjanus) via
  `make rtl` in the FreshRSS repo — a PR adding `freedly.rtl.css` that
  way would be very welcome.
- Sidebar/toolbar icon glyphs are FreshRSS's own icon set (recolored via
  CSS filters), not Feedly's actual iconography — a pixel-exact icon set
  swap was out of scope.
- Title/byline/excerpt font *sizes* approximate Feedly's proportions
  rather than matching exactly — Feedly sets that sizing through
  runtime-injected CSS-in-JS that isn't visible in a saved page's source,
  unlike the color tokens and thumbnail dimension above. Exact values
  would need to come from a browser's DevTools Computed panel.

## Screenshots

Add your own under `screenshots/` and reference them from the top of this
README (`list-view.png`, `reader-view.png` are just suggested names). The
`thumbs/original.png` FreshRSS uses in its own theme picker (Settings →
Display) is a placeholder card — replace it with a real UI screenshot at
roughly the same size (1900×920) for a proper preview there.

## Credits

- Color tokens and thumbnail dimensions sourced from Feedly's own
  production CSS and CDN requests (`feedly.com` / `s1.feedly.com` /
  `visuals.feedly.com`).
- [Inter](https://rsms.me/inter/) by Rasmus Andersson and the Inter
  Project Authors, licensed under the
  [SIL Open Font License 1.1](fonts/LICENSE-OFL.txt).
- Built on top of FreshRSS's **Origine** theme by Marien Fressinaud, and
  the **Dark**/**Nord** community themes, which this theme's layering
  approach (`_frss.css` → `Origine/origine.css` → theme CSS) follows.
- [FreshRSS](https://freshrss.org) itself, and its
  [theme-writing documentation](https://freshrss.github.io/FreshRSS/en/developers/04_Frontend/02_Design.html).

## License

This theme's original code (`freedly.css`, `metadata.json`, this README)
is licensed under the [MIT License](LICENSE).

The bundled font (`fonts/InterVariable*.woff2`) is licensed separately
under the [SIL Open Font License 1.1](fonts/LICENSE-OFL.txt) — it is
**not** MIT, and that license text must stay with the font files if you
redistribute them.

Feedly itself, its name, and its trademarks are the property of their
respective owners; this project is an independent, unaffiliated fan
theme and is not endorsed by or affiliated with Feedly.
