# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- `hugo server --buildDrafts` — run the local dev server at http://localhost:1313 with live reload, including draft posts.
- `hugo new content posts/<slug>.md` — create a new post from the archetype in `archetypes/default.md` (pre-fills date, `draft = true`, title).
- `hugo` — production build; writes static output to `public/` (gitignored — this is the only directory that gets deployed to S3, never committed).
- After cloning: `git submodule update --init --recursive` is required, or `themes/PaperMod` will be empty and the build will fail.

## Architecture

This is a [Hugo](https://gohugo.io) static site using the **PaperMod** theme, installed as a git submodule at `themes/PaperMod` (tracked via `.gitmodules`, not vendored — do not copy theme files directly into this repo).

- `content/posts/` — the actual blog posts (Markdown with TOML front matter, `+++` delimited). This is the primary directory for day-to-day writing.
- `hugo.toml` — site config and PaperMod theme params (e.g. `ShowCodeCopyButtons`). `baseURL` is currently a placeholder (`https://example.org/`) pending the real S3/CloudFront domain.
- `layouts/` — local template overrides. Empty by default; only add files here to override a specific PaperMod template rather than forking the whole theme.
- `assets/` vs `static/` — `assets/` is for files Hugo processes (e.g. Sass), `static/` is for files copied through unchanged (favicons, etc.). Both are currently empty.
- Deploy target is **Amazon S3** (static website hosting), not GitHub Pages — only the generated `public/` directory is ever meant to be uploaded there.
