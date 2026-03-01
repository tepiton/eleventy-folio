# Chronicle

Date: February 24, 2026

## Objective

Create a modern Eleventy v3 base for chaptered literary sites, using local references from `twohorses.lol` and `esther.lol`, and replacing the off-the-shelf blog starter structure.

## Work Log

1. Reviewed the starter repository structure and identified it as `eleventy-base-blog` with blog/feed/tags defaults.
2. Located the reference sites at:
   - `/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.lol`
   - `/Users/philip/projects/mimeo-sites/esther.lol`
3. Analyzed both reference sites:
   - Minimal Eleventy setup.
   - Single long-form narrative pages.
   - Literary typography-focused presentation.
4. Refactored Eleventy config in [eleventy.config.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/eleventy.config.js):
   - Removed active blog/feed/image/syntax-highlighter features from starter flow.
   - Kept navigation plugin and base URL transforms.
   - Added `chapters` collection sorted by numeric `order`.
   - Added server option `showAllHosts: true` for printing all local host URLs.
5. Updated metadata in [metadata.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/_data/metadata.js) for literary-site defaults.
6. Added book-level data model in [book.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/_data/book.js).
7. Reworked base HTML shell in [base.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/_includes/layouts/base.njk):
   - Metadata title/description tied to book data.
   - Simplified content rendering.
   - Top navigation retained.
   - Footer shows author.
8. Added chapter layout [chapter.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/_includes/layouts/chapter.njk):
   - Chapter heading block (`chapterNumber`/`order`, title, optional `dek`).
   - Previous/next chapter navigation using `collections.chapters`.
9. Cleaned home layout wrapper in [home.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/_includes/layouts/home.njk) by removing starter instructions box.
10. Replaced global styles in [index.css](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/css/index.css) with a reading-oriented literary theme.
11. Replaced homepage content in [index.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/index.njk):
    - Hero with book title/subtitle/description.
    - Rendered chapter list from `collections.chapters`.
12. Repurposed archive route as contents in [blog.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/blog.njk):
    - Title changed to Table of Contents.
    - Chapter listing replaces blog archive.
13. Updated about page in [about.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/about.md) with chaptered workflow guidance.
14. Changed default content layout in [content.11tydata.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/content.11tydata.js) from `layouts/home.njk` to `layouts/base.njk`.
15. Disabled legacy blog post output in [blog.11tydata.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/blog/blog.11tydata.js) by setting `permalink: false`.
16. Disabled legacy tag outputs by setting `permalink: false` in:
    - [tags.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/tags.njk)
    - [tag-pages.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/tag-pages.njk)
17. Added chapter data defaults in [chapters.11tydata.js](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/chapters/chapters.11tydata.js).
18. Added sample chapters:
    - [01-threshold.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/chapters/01-threshold.md)
    - [02-orchard.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/chapters/02-orchard.md)
    - [03-lantern-room.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/chapters/03-lantern-room.md)
19. Updated package identity and scripts in [package.json](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/package.json):
    - Renamed package to `eleventy-chaptered-literary-base`.
    - Updated description/repo/author/homepage placeholders.
    - Set dev server scripts to port `8084`.
20. Replaced project docs in [README.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/README.md) with chaptered-starter documentation.

## Build and Runtime Issues Encountered

1. Initial build attempts failed in restricted environment due to blocked npm network access when resolving `npx` binaries.
2. Once dependencies were available, Eleventy failed on JS front matter parsing:
   - Error: `'import' and 'export' may only appear at the top level`
   - Root cause: used `export default` inside `---js` front matter blocks.
3. Fixed front matter by converting affected templates to YAML front matter:
   - [content/index.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/index.njk)
   - [content/blog.njk](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/blog.njk)
   - [content/about.md](/Users/philip/projects/mimeo-sites/EXPERIMENT/twohorses.new.worktree/codex-tree/content/about.md)
4. Build then succeeded and generated:
   - `/`
   - `/blog/`
   - `/about/`
   - `/chapters/01-threshold/`
   - `/chapters/02-orchard/`
   - `/chapters/03-lantern-room/`
5. Dev server bind tests in this sandbox returned `EPERM` for `0.0.0.0` (environment restriction), but config is set for all-host visibility and port `8084`.

## Final State

- Project is now a chaptered literary Eleventy starter rather than a blog starter.
- Chapter navigation, contents page, and sample chapter workflow are in place.
- Dev server scripts use port `8084`.
- Server host visibility is configured with `showAllHosts: true`.

## Wrap-up: Three-Implementation Review

Date: February 25, 2026

Performed a comparative review of three parallel implementations of the same task:

- `codex-tree` (this repository)
- `../claude-tree`
- `../opencode-tree`

### What was reviewed

- Repository structure and changed files
- Eleventy config, layouts, content model, CSS approach
- README quality and customization guidance
- Build behavior and generated output

### Validation method

- Ran `npm run build` in each tree where possible.
- For fair write-permission behavior, also ran:
  - `npx @11ty/eleventy --output=/tmp/three-takes-codex`
  - `npx @11ty/eleventy --output=/tmp/three-takes-claude`
  - `npx @11ty/eleventy --output=/tmp/three-takes-opencode`

All three produced valid static output with chapter pages when writing to `/tmp`.

### Outcome

- Added comparative report: `docs/THREE-TAKES.md`
- Report includes:
  - scorecard across major criteria
  - strengths/weaknesses for each implementation
  - recommendation and practical synthesis

### Key conclusion recorded

- `claude-tree` scored highest for architectural cleanliness and overall implementation quality.
- `codex-tree` remains the best immediate fit for this repo’s current requirements because it already matches the requested dev behavior:
  - all-host serving visibility
  - explicit port `8084`

### Next-step direction noted

Use `codex-tree` as base and selectively port cleanup improvements inspired by `claude-tree`:

1. Remove disabled legacy blog/tag/post artifacts entirely.
2. Trim unused dependencies inherited from the original blog starter.
3. Optionally rename the TOC route from `/blog/` to a semantically literary route such as `/contents/`.

---

## README rewrite (2026-02-25)

Rewrote `README.md` from scratch. The previous README had the wrong title ("11ty Chaptered Literary Base" — that's chapbook's description) and did not document the two-data-file structure.

New README covers:
- Correct repo name `eleventy-folio` as title
- Both `_data/book.js` and `_data/metadata.js` documented with their actual schemas and the fallback chain (`book.title or metadata.title`) explained
- Chapters and blog posts both covered
- Project structure tree
- npm scripts table
- Deploy section noting the workflow handles pathprefix automatically

---

## Font parameterization and Typekit (2026-02-27)

Added `--font-body` and `--font-heading` CSS custom properties to `:root` in `css/index.css`:

```css
--font-body: p22-stickley-pro-text, neue-kabel, Palatino, Georgia, serif;
--font-heading: neue-kabel, 'Gill Sans', 'Helvetica Neue', sans-serif;
```

The hardcoded `font-family` on `body` was replaced with `var(--font-body)`.

Baked the two esther.lol Typekit kit IDs directly into `base.njk` rather than routing through `metadata.js`. Since the CSS vars reference these font names explicitly, the coupling is honest.

## Site URL, title, and nav cleanup (2026-02-27)

- Set `metadata.url` to `https://orobia.net/`
- Set `book.title` to `"Folio"`
- Set `metadata.title` to `"Folio"`
- Updated `content/about.md` to reference orobia.net
- Removed the `eleventyNavigation` block from `content/index.njk` — the home page no longer generates a "Home" nav link

---

## Content portability (2026-02-28)

Made `content/` fully portable across the three template family (pamphlet, chapbook, folio).

### Changes

1. Merged `_data/book.js` into `content/_data/metadata.js` (single file now)
2. Deleted `_data/` directory
3. Updated `eleventy.config.js` data path from `../_data` to `_data`
4. Changed chapters collection from `getFilteredByTag("chapter")` to `getFilteredByGlob("content/chapters/*.md")`
5. Simplified `chapters.11tydata.js` - removed `tags`, kept layout only
6. Updated `base.njk` to remove `book.` references (now uses `metadata.` directly)
7. Deleted unused files:
   - `content/blog/` directory
   - `content/blog.njk`
   - `content/tags.njk`
   - `content/tag-pages.njk`
   - `_includes/postslist.njk`
   - `_includes/layouts/post.njk`
   - `css/message-box.css`
   - `css/prism-diff.css`

### Result

The `content/` directory is now self-contained. Drop it into any of the three templates and it works. Each template provides its own layouts, CSS, and personality.
