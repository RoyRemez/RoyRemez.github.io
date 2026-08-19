# royremez.github.io

Portfolio site for Roy Remez — Automation &amp; Process Specialist.

Static HTML and CSS. No build step, no dependencies, no external requests:
fonts are self-hosted and every graphic is inline SVG.

## Layout

| Path | What it is |
|---|---|
| [index.html](index.html) | Hebrew (RTL) — the primary page, served at the site root |
| [en/index.html](en/index.html) | English |
| [assets/styles.css](assets/styles.css) | The whole stylesheet, including `@font-face` and the RTL block |
| [assets/fonts/](assets/fonts/) | Heebo woff2, Latin and Hebrew subsets, weights 300/400/500 |
| [assets/media/](assets/media/) | Portrait and tool demos — currently empty |
| [design/](design/) | Design-canvas sources (`.dc.html` artboards). Not part of the site |

The two language pages share one stylesheet. Layout mirrors automatically
because the CSS uses logical properties (`border-inline-end`,
`padding-inline-start`) rather than physical ones — so **don't reintroduce
`left`/`right`/`border-right`**, or RTL will break.

## Adding your portrait

Drop a square image at `assets/media/portrait.jpg`, then in **both** pages
replace the placeholder div with the commented-out `<img>` sitting directly
above it:

```html
<img class="portrait" src="assets/media/portrait.jpg" alt="Roy Remez" width="96" height="96">
```

Note the path differs by page — `assets/…` from the root, `../assets/…` from
`en/`. Crop square; CSS handles the circle and the cover fit.

## Adding tool demos

Each work card has a commented hint inside `.card-fig`. Drop a file into
`assets/media/` and uncomment:

```html
<img src="assets/media/det-01.gif" alt="Preview render tool">
```

It fills the frame and replaces the line drawing. **Prefer a muted looping
`<video>` over a GIF** — same result at roughly a tenth the size:

```html
<video src="assets/media/det-01.mp4" autoplay muted loop playsinline></video>
```

Keep each demo under ~2 MB. If a card has no media it keeps its drawing, so
you can add them one at a time.

## Editing content

Copy lives directly in the HTML — there is no CMS or data file. Anything you
change in one language needs the same change in the other; the pages are
deliberately independent rather than templated, since a build step would buy
very little at this size.

## Deploying

GitHub Pages serves `main` from the repo root. Push and it updates.

## Regenerating the design canvas

`design/portfolio-canvas.html` is gitignored — it is ~2 MB of vendored editor
code, rebuilt from the `.dc.html` sources by the `/design` skill's
`seed-canvas.mjs`. The canvas records the design exploration; the site is the
product, and the two can drift.
