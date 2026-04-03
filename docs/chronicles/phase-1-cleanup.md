# Phase 1: Cleanup & Portability

## Entry 1: README and docs (2026-02-25)

**What**: Rewrote README to correctly document the repo structure and name.

**Why**: Initial README had incorrect paths and referenced `index.njk` instead of `index.md`.

**How**:

- Corrected title to `eleventy-folio`
- Documented single metadata file (book.js merged into metadata.js)
- Added fonts, colors, and styles section

**Files**: `README.md`, `docs/CHRONICLE.md`

---

## Entry 2: Content portability (2026-02-28)

**What**: Made `content/` portable across all three templates by normalizing the data and collection structure.

**Why**: Goal was to let users swap templates (change the look) without touching content. See DEC-001, DEC-002, DEC-003.

**How**:

- Merged `_data/book.js` into `content/_data/metadata.js` — see DEC-005
- Deleted root `_data/` directory
- Switched chapters collection from tag-based to glob-based — see DEC-002
- Simplified `chapters.11tydata.js` — removed `tags`
- Updated `base.njk` to remove `book.` references
- Deleted unused files: blog, tag, post, feed, postslist, prism CSS

**Decisions**: DEC-001, DEC-002, DEC-003, DEC-004, DEC-005

**Files**: `content/_data/metadata.js`, `content/chapters/chapters.11tydata.js`, `eleventy.config.js`

---

## Entry 3: Fonts and Typekit (2026-02-27)

**What**: Added CSS font vars and baked Typekit kit IDs into `base.njk`.

**Why**: Font configuration was scattered; wanted a single place to change fonts. See DEC-007.

**How**:

- Added `--font-body` and `--font-heading` CSS custom properties in `:root`
- Baked Typekit kit IDs `ztn6rcs` and `pgn7ley` into `base.njk` unconditionally
- Removed `typekit` field from `metadata.js`

**Decisions**: DEC-007

**Files**: `css/index.css`, `_includes/layouts/base.njk`
