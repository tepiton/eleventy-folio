# Phase 3: Schema Parity

## Entry 1: Align OG meta and metadata schema (2026-03-30)

**What**: Final alignment pass across all three templates for metadata schema and OG meta tags.

**Why**: Folio, pamphlet, and chapbook had drifted slightly in their `metadata.js` schema and OG meta rendering. Needed identical schemas for `content/` portability to be complete.

**How**:

- Added `image: ""` to `content/_data/metadata.js`
- Made `og:image` conditional in `base.njk` — see DEC-008
- Aligned schema with pamphlet and chapbook

**Decisions**: DEC-008

**Files**: `content/_data/metadata.js`, `_includes/layouts/base.njk`
