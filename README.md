# eleventy-folio

An Eleventy v3 starter for chaptered literary sites. Polished defaults, extra features.

Part of a family of interoperable templates:
- **eleventy-pamphlet** - minimal, single layout
- **eleventy-chapbook** - separate layouts, feature-rich
- **eleventy-folio** (this) - polished, with extras

The `content/` directory is portable across all three. Swap templates to change the presentation without touching your content.

## Quick start

```
git clone <this-repo> my-project
cd my-project
npm install
npm run start
```

Then open `http://localhost:8084`.

## Customization

### Site metadata

Edit `content/_data/metadata.js`:

```js
export default {
  title: "Your Literary Work",
  subtitle: "A subtitle or tagline",
  url: "https://example.com/",
  language: "en",
  description: "A description of this work.",
  author: {
    name: "Your Name",
    email: "you@example.com",
    url: "https://example.com/"
  }
}
```

Note: `metadata.js` lives inside `content/_data/` so the entire `content/` directory is self-contained and portable.

### Chapters

Add files to `content/chapters/`. Each needs front matter:

```yaml
---
title: The Title of This Chapter
order: 1
dek: Optional one-line subtitle shown in the TOC
---
```

- `order` controls sort order in the TOC and prev/next navigation
- `dek` is optional
- Filename determines the URL: `01-threshold.md` → `/chapters/01-threshold/`

### Home page

Edit `content/index.njk`. The chapter list is generated automatically.

### About page

Edit `content/about.md`.

### Fonts, colors, and styles

Colors are CSS custom properties at the top of `css/index.css`:

```css
:root {
  --bg: #faf6ee;      /* page background */
  --paper: #fffdf8;   /* main content column */
  --ink: #1c1a18;     /* body text */
  --muted: #6d685f;   /* secondary text, captions */
  --rule: #d6d0c6;    /* borders and dividers */
  --accent: #8d3f2b;  /* links */
}
```

Change any of these to retheme the site without touching the rest of the stylesheet.

**Body font:** The body font stack uses CSS custom properties in `css/index.css`:

```css
:root {
  --font-body: p22-stickley-pro-text, neue-kabel, Palatino, Georgia, serif;
  --font-heading: neue-kabel, 'Gill Sans', 'Helvetica Neue', sans-serif;
}
```

**Adobe Fonts (Typekit):** This template uses `p22-stickley-pro-text` and `neue-kabel` from Adobe Fonts. The kit IDs are baked into `_includes/layouts/base.njk`. To use different fonts, replace the Typekit `<link>` tags and update the CSS variables.

**Other web fonts:** Add a `<link>` to your font provider in `_includes/layouts/base.njk` and update the `--font-body` and `--font-heading` variables in `css/index.css` to match.

## Project structure

```
content/
  _data/
    metadata.js          # Title, subtitle, author, URL
  index.njk              # Home page
  about.md               # About / colophon
  chapters/
    chapters.11tydata.js # Layout for all chapters
    01-threshold.md
    02-orchard.md
    ...
_includes/
  layouts/
    base.njk             # HTML shell
    home.njk             # Home page layout
    chapter.njk          # Chapter layout with prev/next
css/
  index.css              # All styles
```

The `content/` directory is designed to be portable. Copy it to eleventy-pamphlet or eleventy-chapbook to get a different presentation with the same content.

## npm scripts

| Command | Description |
|:--------|:------------|
| `npm run start` | Dev server at `localhost:8084` with live reload |
| `npm run build` | Production build to `_site/` |
| `npm run debug` | Build with Eleventy debug output |

## Deploy

The included `.github/workflows/pages.yml` builds and deploys to GitHub Pages on push to `main`. No configuration needed for custom domains — the workflow detects the repo name and sets the path prefix automatically.
