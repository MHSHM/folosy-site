# folosy-site

The Folosy pre-launch landing page. Plain static HTML — no build step, no dependencies.

**Live at:** https://mhshm.github.io/folosy-site/

## Deploy

1. Create a public GitHub repo named `folosy-site`.
2. Push everything in this folder to `main`.
3. Settings → Pages → Source: **Deploy from a branch**, Branch: **main / (root)**.

Leave the separate `folosy-legal` repo alone — its URL is filed in the Play Console paperwork.

## Before it goes live

`index.html` has **one placeholder**: the «دوس هنا» link in the banks section is `href="#"`,
marked with a `TODO` comment. Point it at the bank-request Google Form.

## Files

| Path | What |
|---|---|
| `index.html` | The whole page — markup, CSS and ~15 lines of JS in one file |
| `fonts/*.woff2` | IBM Plex Sans Arabic 400/700 + Plex Mono 500, subset to the characters used (120 KB total) |
| `shots/*.webp` | The four Arabic Play Store panels, 540×960 (63 KB total) |
| `og.png` | Social preview image, shown when the link is posted to Facebook/WhatsApp |
| `favicon.png` | Browser tab icon |
| `.nojekyll` | Tells GitHub Pages to serve files as-is rather than running Jekyll |

## Editing

Everything is in `index.html`. The colour tokens at the top are copied from the app's
`src/global.css`, so keep them in sync if the app's palette changes.

Two things that are load-bearing and easy to break:

- **Amounts are wrapped in `dir="ltr"`.** Without it the minus sign drifts to the wrong
  side of the number under RTL. Same reason `core/money.ts` uses LTR isolates in the app.
- **The screenshot deck is centred with symmetric negative margins.** One-sided physical
  properties (`margin-left`, `left`) do not centre correctly in an RTL page.

## Regenerating assets

Fonts were subset from `node_modules/@expo-google-fonts` in the app repo:

```
python -m fontTools.subset <font>.ttf \
  --unicodes="U+0020-007E,U+00A0-00FF,U+0600-06FF,U+FB50-FDFF,U+FE70-FEFF,U+200B-206F,U+20A0-20BF,U+2212" \
  --layout-features='*' --flavor=woff2 --output-file=fonts/<name>.woff2
```

Screenshots came from `docs/play-assets/screenshots/ar/` in the app repo, resized to
540×960 and saved as WebP at quality 82.
