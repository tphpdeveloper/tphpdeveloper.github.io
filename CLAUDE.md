# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not a source project** — it's the deployed GitHub Pages output of
[`mooved_map_new`](../mooved_map_new) (sibling directory), the Nuxt 4 / Vue 3
/ Vuetify 3 rewrite of the star-map annotation app. The repo name
(`tphpdeveloper.github.io`) is a GitHub user page, served at the repo root
(no path prefix) — `mooved_map_new` has no `app.baseURL` override, matching.

Everything here except `.nojekyll`, `README.md`, and `CLAUDE.md` is the
committed output of `nuxt generate` run inside `../mooved_map_new`
(`.output/public/` there):

- `index.html`, `200.html`, `404.html` — SPA entry + GitHub Pages SPA-fallback
  (GitHub Pages natively serves `404.html` for any unmatched path; `200.html`
  is Nuxt's own equivalent convention — both are generated automatically by
  `nuxt generate`, unlike the old Nuxt 2 `mooved_map` build which only
  produced `200.html`).
- `_nuxt/` — hashed, minified JS/CSS chunks (Vite output — do not confuse with
  the differently-structured Nuxt 2/webpack `_nuxt/` that used to be deployed
  here from `mooved_map`).
- `map/` — the star-map images (`main.jpg`, `stars.png`, `move_circle.png`,
  `background-image.jpg`, `коло.jpg`), copied from `mooved_map_new/public/map/`.
  Note the path: `mooved_map_new` references these at `/map/...`, not `/...`
  like the old `mooved_map` build did — don't reintroduce root-level copies.
- `favicon.ico`, `robots.txt`, `_payload.json` — static assets / Nuxt payload,
  copied verbatim from the build output.
- `.nojekyll` — disables GitHub Pages' Jekyll processing (required for the
  underscore-prefixed `_nuxt/` directory to be served as-is). This file is
  **not** part of the Nuxt build output — it must be preserved (or recreated
  empty) across every redeploy by hand.
- `README.md` — Nuxt's default `static/README.md` boilerplate; not describing
  this repo.

### History

This repo previously deployed the older Nuxt 2 `mooved_map` build (root-level
images, webpack `_nuxt/`, no `404.html`/`map/`/`robots.txt`). It was switched
over to `mooved_map_new`'s Nuxt 4 build wholesale — old generated files were
deleted, not merged, so there's no leftover mix of the two builds' assets to
worry about.

## Making changes

There is no source to edit here. To change anything about the app itself:

1. Make the change in `../mooved_map_new` (the actual source project — see
   its own `CLAUDE.md`).
2. From `../mooved_map_new`, run `pnpm run generate` (needs Node ≥20 — the
   shell's default Node is too old; `nvm use` a newer version first). Output
   lands in `.output/public/`.
3. Replace this repo's `index.html`, `200.html`, `404.html`, `_nuxt/`, `map/`,
   `favicon.ico`, `robots.txt`, and `_payload.json` with the fresh build
   output. Make sure `.nojekyll` still exists afterward (the build doesn't
   produce it).
4. Preview locally before pushing (e.g. `npx serve .` from this repo's root)
   to catch broken asset paths or console errors.
5. Commit and push — there is no CI; deployment is just GitHub Pages serving
   whatever is on the default branch (`master`).

## Commands

No install/build/test commands apply to this repo directly — there is no
`package.json`. To preview the site locally, serve the directory with any
static file server (e.g. `npx serve .` or `python3 -m http.server`) from the
repo root.
