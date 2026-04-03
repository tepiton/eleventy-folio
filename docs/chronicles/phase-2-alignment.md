# Phase 2: Alignment

## Entry 1: Standardize across template family (2026-03-03)

**What**: Aligned folio with pamphlet and chapbook on chapter sorting, layout simplification, content files, and dark mode.

**Why**: The three templates had diverged in small ways that broke `content/` portability. Needed identical behavior across all three.

**How**:

- Changed chapter `order` fallback from 0 to 999 (chapters without order sort to end) — see DEC-006
- Added secondary sort by filename for deterministic tie-breaking — see DEC-006
- Renamed `index.njk` to `index.md` for consistency with pamphlet
- Fixed `index.md`: changed `{{ book.title }}` to `{{ metadata.title }}`
- Simplified `chapter.njk` to use `{{ order }}` instead of `{{ chapterNumber or order }}`
- Updated `about.md` with colophon and GitHub source link
- Added `details/summary` CSS styling for collapsible content
- Added dark mode with three-way toggle (light/dark/system)

**Decisions**: DEC-006

**Files**: `eleventy.config.js`, `content/index.md`, `_includes/layouts/chapter.njk`, `content/about.md`, `css/index.css`, `js/`
