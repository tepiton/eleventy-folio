# Chronicle

## Overview

`eleventy-folio` is an Eleventy v3 starter for chaptered literary sites. One of three interoperable templates (pamphlet, chapbook, folio) that share portable `content/` directories. Served from orobia.net.

## Origin

Converted from `eleventy-base-blog` v9 into a literary starter. See `docs/THREE-TAKES.md` for comparison with parallel implementations.

## Key Architecture

- **Single input dir**: `content/`
- **Layouts**: `_includes/layouts/base.njk`, `home.njk`, `chapter.njk`
- **Chapters collection**: Glob-based `content/chapters/*.md` (no tags)
- **Chapter frontmatter**: Just `order` and `title` (optional `dek`)
- **Layout assignment**: Via `chapters.11tydata.js` and `content.11tydata.js`
- **Port**: 8084 in `package.json` start script
- **Fonts**: Typekit kits `ztn6rcs` and `pgn7ley` baked into `base.njk`
- **CSS vars**: `--font-body` and `--font-heading` in `:root`

## Directory Structure

```
content/
  _data/metadata.js
  chapters/
    chapters.11tydata.js    # layout: layouts/chapter.njk
    *.md
  content.11tydata.js       # layout: layouts/base.njk
  index.md, about.md, 404.md
_includes/layouts/
  base.njk, home.njk, chapter.njk
css/index.css
```

## Unique Features

- Chapter layout supports optional `dek` (subtitle)
- Uses `@zachleat/heading-anchors` for anchor links
- Includes sitemap generation

---

## Recent Changes

### 2026-03-30: Schema and OG meta alignment

Aligned with chapbook and pamphlet for cross-template parity.

1. Added `image: ""` to `content/_data/metadata.js` (canonical schema now includes image)
2. Made `og:image` conditional in `base.njk` (only rendered when `metadata.image` is set)

### 2026-03-03: Simplify chapter layout

Aligned with pamphlet and chapbook for full portability.

1. Updated `chapter.njk` to use `{{ order }}` instead of `{{ chapterNumber or order }}`

### 2026-03-03: Fix and standardize content files

1. Fixed `index.njk` - changed `{{ book.title }}` to `{{ metadata.title }}` (book.js was merged)
2. Renamed `index.njk` to `index.md` for consistency with pamphlet
3. Updated `about.md` with colophon and GitHub source link

### 2026-03-03: Standardize chapter sorting

1. Changed `order` fallback from 0 to 999 (chapters without order sort to end)
2. Added secondary sort by filename for deterministic ordering when order is equal

### 2026-02-28: Content portability

Made `content/` portable across all three templates.

1. Merged `_data/book.js` into `content/_data/metadata.js` (single file now)
2. Deleted `_data/` directory
3. Changed chapters collection from `getFilteredByTag("chapter")` to `getFilteredByGlob("content/chapters/*.md")`
4. Simplified `chapters.11tydata.js` - removed `tags`
5. Updated `base.njk` to remove `book.` references
6. Deleted unused files: `content/blog/`, `content/blog.njk`, `content/tags.njk`, `content/tag-pages.njk`, `_includes/postslist.njk`, `_includes/layouts/post.njk`, `css/message-box.css`, `css/prism-diff.css`

### 2026-02-27: Fonts and Typekit

Added `--font-body` and `--font-heading` CSS vars. Baked Typekit kit IDs into `base.njk`. Removed `eleventyNavigation` block from home page.

### 2026-02-25: README rewrite

Corrected title to `eleventy-folio`, documented single metadata file (book.js merged).
