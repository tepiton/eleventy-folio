# eleventy-folio

An Eleventy v3 starter for chaptered literary sites with both a blog and chapter navigation. Built for long-form prose that mixes serialized chapters with standalone posts.

## Quick start

```
git clone <this-repo> my-project
cd my-project
npm install
npm run start
```

Then open `http://localhost:8080`.

## Customization

### Site metadata

This template uses two data files:

**`_data/book.js`** — the work itself:

```js
export default {
  title: "The Sample Book",
  subtitle: "A starter for chaptered narrative sites",
  author: "Your Name",
  description: "Replace this with a one-sentence hook for your story.",
}
```

**`_data/metadata.js`** — site and SEO settings:

```js
export default {
  title: "Chaptered Literary Site",
  url: "https://example.com/",
  language: "en",
  description: "An Eleventy starter for chaptered, long-form literary projects.",
  author: {
    name: "Your Name",
    email: "youremailaddress@example.com",
    url: "https://example.com/"
  }
}
```

`book.title` and `book.author` take precedence in the layout; `metadata` provides the URL, language, and SEO fallbacks.

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

### Blog posts

Add files to `content/blog/`. These use the standard post layout with tags and are listed on the blog index.

### Home page

Edit `content/index.njk`. The hero section pulls from `book.js`. Below it, the chapter list is generated automatically.

### About page

Edit `content/about.md`.

## Project structure

```
content/
  index.njk              # Home page (hero + chapter list)
  about.md               # About / colophon
  blog/                  # Blog posts
  chapters/
    chapters.11tydata.js # Tags, layout for all chapters
    01-threshold.md
    02-orchard.md
    ...
_data/
  book.js                # Title, subtitle, author, description
  metadata.js            # URL, language, SEO metadata
_includes/
  layouts/
    base.njk             # HTML shell
    home.njk             # Home page layout
    chapter.njk          # Chapter layout with prev/next
    post.njk             # Blog post layout
css/
  index.css              # All styles
```

## npm scripts

| Command | Description |
|:--------|:------------|
| `npm run start` | Dev server with live reload |
| `npm run build` | Production build to `_site/` |
| `npm run debug` | Build with Eleventy debug output |

## Deploy

The included `.github/workflows/pages.yml` builds and deploys to GitHub Pages on push to `main`. No configuration needed for custom domains — the workflow detects the repo name and sets the path prefix automatically.
