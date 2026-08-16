# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A [Hugo](https://gohugo.io/) static site: Yuval Bloch's personal/academic blog and research site
("Complexity & Ecology Research"), covering computational ecology, ecological modeling, and personal
essays. It uses the **ananke** theme, vendored as a git submodule under `themes/ananke/`. There is no
JavaScript build step, no package manager, and no test suite — this is a content + template project.

The repo doubles as an Obsidian vault (`.obsidian/`) — content markdown files are authored/edited in
Obsidian, and `temporal stuff/` holds drafts that haven't been turned into Hugo content yet.

## Commands

- **Local dev server (with drafts):** `hugo server -D`
- **Local dev server (published content only):** `hugo server`
- **Production build (matches CI):** `hugo --minify` → outputs to `public/`
- Requires the **extended** Hugo binary (the theme calls `css.Sass`; LibSass is enough, Dart Sass is
  not needed). CI and local are both on v0.147.7-extended.
- No lint/test/format commands exist in this repo (no `package.json`, no CI test job).
- **If a build appears to hang**, check for stale `hugo` processes (`Get-Process hugo`) and kill them.
  Leftover processes deadlock new builds indefinitely at near-zero CPU. A clean full build of this
  site takes ~0.5s in memory, ~2.5s to disk — anything longer is a stuck process, not a slow machine.

## Deployment

**The Hugo site root is `quickstart/`, not the repository root.** The git repo is one level up
(it also holds `.github/`, the Obsidian vault config, and `CNAME`). Any CI step that runs Hugo must
set `working-directory: ./quickstart` — a workflow that runs `hugo` at the repo root finds no config
and fails. (This was broken from May–Aug 2026 for exactly that reason; every run failed and the site
was updated by hand.)

`.github/workflows/hugo.yml` builds and deploys on every push to `main`:
checkout (with submodules, for `themes/ananke`) → `peaceiris/actions-hugo` (pinned `0.147.7`,
`extended: true`) → `hugo --minify` in `quickstart/` → publish `quickstart/public/` to the
**`gh-pages` branch** via `peaceiris/actions-gh-pages`. GitHub Pages serves that branch. There's no
PR preview workflow — pushing to `main` ships to production.

**Custom domain:** `yuvalbloch.com` depends on a `CNAME` file existing in the published output.
It comes from `static/CNAME`, and the workflow both asserts it survived the build and re-applies it
via the `cname:` input. Never remove `static/CNAME` — publishing a build without it takes the domain
offline.

`quickstart/public/` and `quickstart/resources/` are gitignored build output, not source. Content and
template edits should always go through `content/`, `layouts/`, `assets/`, `static/`, or `hugo.toml`.

## Configuration

`hugo.toml` at the repo root is the **only** active Hugo config file — it defines site params, the
`[[menu.main]]` entries, both languages, and the ananke theme's social/params overrides in one place.

## Content structure

Content sections live under `content/`: `blog/` (essays, ~40+ posts), `research/`, `about/`,
`teaching/` (includes a Hebrew-language Python course subfolder), `LEAN/`, `presentations/`. Each
section has an `_index.md` for its list page. `content/posts/` is effectively empty (no real posts);
the home page's "recent posts" logic (`layouts/index.html`) uses `site.Params.mainSections` (set to
`["blog"]` in `hugo.toml`) to find that content.

**Bilingual content:** the site is set up for English (default) + Hebrew (`languageDirection = "rtl"`)
via Hugo's multilingual config in `hugo.toml`. Hebrew translations are added as sibling files with a
`.he.md` suffix (e.g. `fungaia.md` / `fungaia.he.md`), not via `content/he/...` subdirectories.

Frontmatter is YAML (`---`) across most content, with keys like `title`, `date`, `draft`,
`description`, `featured_image`, `omit_header_text`; the default archetype (`archetypes/default.md`)
uses TOML instead — new pages created via `hugo new` will need their frontmatter format reconciled
with the rest of the content if that matters.

## Templates and theme overrides

Hugo resolves templates by checking the project's `layouts/` before falling back to
`themes/ananke/layouts/`. The project only overrides a few things:

- `layouts/_default/baseof.html` — full copy of the theme's base template (head, body shell, blocks).
- `layouts/index.html` — home page: renders `.Content` then a "recent posts" section driven by
  `site.Params.mainSections` (see the section mismatch noted above).
- `layouts/teaching/list.html` — custom list view for the teaching section (renders subsections as
  cards, then any direct pages, then pagination).
- `layouts/partials/opengraph.html`, `layouts/partials/site-scripts.html` — OG tags and MathJax setup.

Canonical link, favicon, and OpenGraph tags come from `baseof.html` directly; custom CSS loading and
MathJax come from the theme's `site-style.html` and this project's `site-scripts.html`. If you need to
add real `<head>` overrides beyond that, create `layouts/partials/head-additions.html` — that's the
override hook `baseof.html`'s `head` block actually calls (`partials.Include "head-additions.html"`).

## Styling

Site-wide CSS overrides live in `static/css/custom.css`, loaded via `site.Params.custom_css` in
`hugo.toml` (`custom_css = ["custom.css"]`). `assets/ananke/css/` contains the theme's Sass source if
deeper style changes are needed; simple color/layout tweaks belong in `static/css/custom.css`.
