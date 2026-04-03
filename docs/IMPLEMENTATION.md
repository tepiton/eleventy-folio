# Implementation — eleventy-folio

## Phase Overview

| # | Name | Status | Date Range |
|---|------|--------|------------|
| 0 | Foundation | ✅ Complete | 2026-02-23 |
| 1 | Cleanup & Portability | ✅ Complete | 2026-02-25–28 |
| 2 | Alignment | ✅ Complete | 2026-03-03 |
| 3 | Schema Parity | ✅ Complete | 2026-03-30 |

---

## Completed Phases

### Phase 0: Foundation (2026-02-23)

- Converted `eleventy-base-blog` v9 into literary chaptered starter
- Added GitHub Actions workflow for Eleventy deployment
- Set title to Folio, URL to orobia.net, port 8084
- Three-layout structure: `base.njk`, `home.njk`, `chapter.njk`

See: chronicles/phase-0-foundation.md

### Phase 1: Cleanup & Portability (2026-02-25–28)

- Rewrote README to match repo name and document actual structure
- Merged `_data/book.js` into `content/_data/metadata.js` (single metadata file)
- Switched chapters collection from tag-based to glob-based (`content/chapters/*.md`)
- Simplified `chapters.11tydata.js` — removed tags, added Typekit vars
- Added `--font-body` and `--font-heading` CSS vars, baked in Typekit kit IDs
- Deleted unused blog/tag/post/feed files and dependencies

See: chronicles/phase-1-cleanup.md

### Phase 2: Alignment (2026-03-03)

- Standardized chapter sort: `order` fallback 999, secondary sort by filename
- Renamed `index.njk` to `index.md` for consistency with pamphlet
- Simplified `chapter.njk` to use `{{ order }}` (not `chapterNumber`)
- Standardized `about.md` with colophon and GitHub source link
- Added `details/summary` CSS styling for collapsible content
- Added dark mode with three-way toggle (light/dark/system)

See: chronicles/phase-2-alignment.md

### Phase 3: Schema Parity (2026-03-30)

- Added `image: ""` to `content/_data/metadata.js`
- Made `og:image` conditional in `base.njk`
- Aligned OG meta and metadata schema with pamphlet and chapbook

See: chronicles/phase-3-parity.md

---

## Current State

The template family is stable. All three templates (folio, pamphlet, chapbook) share:

- Identical `content/` structure (fully portable)
- Identical metadata schema in `content/_data/metadata.js`
- Identical chapter sort behavior
- Identical OG meta conditional rendering

No active feature work. Future changes should track as Phase 4.

---

## Future Phases

### Phase 4: (Unplanned)

Ideas if needed:

- RSS/Atom feed for chapters
- sitemap improvements
- Additional CSS literary features (scene headings, character headings from chapbook)
- Pagination for long chapter lists
