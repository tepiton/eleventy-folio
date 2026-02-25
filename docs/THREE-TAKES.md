# Three Takes: Comparison of Implementations

Reviewed trees:
- `codex-tree` (this repo, commit `86da11c`)
- `claude-tree` (commit `2f203ba`)
- `opencode-tree` (commit `07cf9fa`)

All three can generate chapter pages and pass a clean Eleventy build when output is redirected to `/tmp`.

## Quick Scorecard

| Criterion | codex-tree | claude-tree | opencode-tree |
|---|---:|---:|---:|
| Meets chaptered-site goal | 4/5 | 5/5 | 4/5 |
| Setup/customization docs | 4/5 | 5/5 | 4/5 |
| Clean conversion from blog starter | 3/5 | 5/5 | 4/5 |
| Technical coherence | 4/5 | 5/5 | 4/5 |
| Literary styling quality | 4/5 | 5/5 | 4/5 |
| Operational fit (all-host dev + explicit port) | 5/5 (`8084`) | 4/5 (`8082`) | 4/5 (`8086`) |

## What Each One Did

### 1) codex-tree
Approach:
- Converted base-blog to chapter-first model but retained some legacy scaffold files (disabled).
- Added `chapters` collection, dedicated chapter layout, homepage + TOC, and chapter prev/next links.
- Added `showAllHosts: true` and dev port `8084`.

Strengths:
- Solid chapter workflow with explicit `order` + `chapterNumber`.
- Clear docs (`README.md`) and detailed work log (`docs/CHRONICLE.md`).
- Matches your latest runtime requirement (`8084`) and all-host serving.

Weaknesses:
- Leaves unused legacy files/deps from `eleventy-base-blog` (e.g., old blog/tag/post artifacts and some unused dependencies).
- TOC lives at `/blog/` for compatibility, which is functional but semantically odd for a literary base.

### 2) claude-tree
Approach:
- Most thorough cleanup: removed blog/tag/feed/post scaffolding and rebuilt as a focused chaptered starter.
- Uses modern Eleventy config, chapter collection, chapter layout, literary CSS, and optional Typekit metadata.

Strengths:
- Cleanest architecture and strongest internal consistency.
- Best README for onboarding/customization (metadata, chapter front matter, typography conventions, CSP notes).
- Strong literary styling system and good defaults.

Weaknesses:
- Dev port is `8082` (not `8084`).
- Slightly richer than necessary for minimalists (e.g., image transform plugin) but still coherent.

### 3) opencode-tree
Approach:
- Simpler restructure using `content/` as Eleventy input, one base layout with chapter behavior toggled by `isChapter`.
- Keeps RSS feed and social metadata.

Strengths:
- Straightforward mental model; fewer moving pieces.
- Supports both single-file and chaptered mode reasonably well.
- Includes feed generation and OG/Twitter fields out of the box.

Weaknesses:
- Less idiomatic separation (no dedicated chapter layout file; chapter logic embedded in base layout via `isChapter`).
- README/chronicle claim some files/choices that do not exactly match final structure.
- Port is `8086` (not `8084`).

## Build Validation Notes

Validated with:
- `npx @11ty/eleventy --output=/tmp/three-takes-codex`
- `npx @11ty/eleventy --output=/tmp/three-takes-claude`
- `npx @11ty/eleventy --output=/tmp/three-takes-opencode`

Generated outputs:
- `codex`: `/`, `/about/`, `/blog/`, `/chapters/...`, `sitemap.xml`
- `claude`: `/`, `/about/`, `/chapters/...`, `sitemap.xml`
- `opencode`: `/`, `/about/`, `/chapters/...`, `/feed/feed.xml`

## Recommendation

If picking the strongest baseline purely on implementation quality: `claude-tree`.

If prioritizing your current requested runtime behavior (all-host + port `8084`) with minimal additional work: `codex-tree` (current repo).

Practical synthesis:
1. Keep `codex-tree` as base (already on `8084` and committed).
2. Port over claude-tree’s cleanup discipline:
   - remove disabled legacy blog/tag/post files
   - trim unused dependencies
   - optionally move `/blog/` TOC to `/contents/` (or `/`) for semantics.
