# 11ty Chaptered Literary Base

An Eleventy starter for chaptered narrative sites in the style of projects like `twohorses.lol` and `esther.lol`, updated to modern Eleventy v3 structure.

## Quick Start

1. Install dependencies:

```bash
npm install
```

2. Run local dev:

```bash
npm start
```

3. Build production output:

```bash
npm run build
```

## Project Shape

- `_data/book.js`: Core book metadata (`title`, `subtitle`, `author`, `description`).
- `content/chapters/`: One Markdown file per chapter.
- `content/blog.njk`: Table of contents page (kept at this path for compatibility).
- `content/index.njk`: Front page with chapter links.
- `_includes/layouts/chapter.njk`: Chapter page layout with previous/next chapter links.

## Creating a New Book

1. Update `_data/book.js` and `_data/metadata.js`.
2. Replace the sample chapter files in `content/chapters/`.
3. Set chapter front matter fields:
   - `title`
   - `order` (numeric sort order)
   - `chapterNumber` (display label: `I`, `II`, `1`, etc.)
   - `dek` (optional one-line subtitle)
4. Update homepage/about copy.

## Notes

- Legacy blog/tag outputs from `eleventy-base-blog` are disabled.
- `content/blog/` is retained as sample material but does not render.
