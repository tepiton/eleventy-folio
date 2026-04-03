# Phase 0: Foundation

## Entry 1: Initial setup (2026-02-23)

**What**: Converted `eleventy-base-blog` v9 into a literary chaptered starter. Added GitHub Actions CI.

**Why**: Needed a base for literary/chaptered sites inspired by twohorses.lol and esther.lol. Compared three LLM implementations (codex, claude, opencode) — see docs/THREE-TAKES.md for the full comparison.

**How**:

- Forked from `eleventy-base-blog` v9
- Added `chapters` collection and `chapter.njk` layout
- Three-layout chain: `base.njk` → `home.njk` → `chapter.njk`
- Set title=Folio, URL=orobia.net, port=8084
- Added GitHub Actions workflow for Eleventy deployment to GitHub Pages
- Fixed branch syntax in workflow

**Files**: `eleventy.config.js`, `_includes/layouts/`, `.github/workflows/`
