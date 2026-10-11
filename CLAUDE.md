# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-page scoring helper for the card game *Courtisans*. The whole app is `index.html`: inline CSS, inline vanilla JS in one IIFE, no build step, no dependencies, no tests, no linter. Fonts (Gloock, Alegreya Sans, Alegreya Sans SC) are self-hosted in `fonts/` via `@font-face` (latin + latin-ext subsets, only the weights in use), so the page makes no third-party requests. The README's privacy section depends on that, so don't add external resources. New font files need their copyright notice in `fonts/OFL.txt`. It deploys to GitHub Pages from `main` at the repo root; `.nojekyll` must stay so Pages serves files as they are.

To run: open `index.html` in a browser. To check a change, reload the page.

## Architecture (inside `index.html`)

- **Data drives the DOM.** `FAMILIES` (six families in Queen's-table order) and `TYPES` (noble ×4 worth 2, courtier ×4, guard ×3, assassin ×2, spy ×2) are the source of truth. The header, status toggles, card tiles and subtotals are all generated from them at startup. Add or change families or card types there, not in the markup. Only the static sections (the headings, the legend, the two mission buttons, the total bar) are hand-written HTML.
- **Family ids differ from display names.** `moth` = Butterfly and `hawk` = Nightingale. Each id is also a CSS custom property name (`--moth`, `--toad`, `--hawk`, …), and `paint()` sets `--fc` / `--fc-ink` / `--fc-line` per column from it. Butterfly gets extra handling because its pale colour needs a darker outline (`--moth-line`) and dark ink.
- **State and render loop.** One `state` object `{ status: {fid: -1|0|1}, cards: {fid: {typeId: count}}, missions: {white, blue} }`. Every event handler mutates `state` and calls `render()`. `render()` syncs `aria-pressed` on every button, recomputes subtotals and the total, and writes to `localStorage` itself. Card tiles store a **count per type**, not per-tile booleans. Tile `i` is lit when `i < count`, and clicking sets the count (see the click handler for the toggle-off rule).
- **Scoring:** per family `Σ(count × type.value) × status`, plus 3 per fulfilled mission.
- **Persistence:** the `localStorage` key is `courtisans-scorer-v1`. The loader validates and clamps every field and also accepts an older mission shape (`{done: bool}`). If you change the state shape, keep it backward-compatible or bump the key.

## Conventions

- Selected states use `aria-pressed="true"` for styling. They show as solid border plus diagonal stripes, and unselected as a dashed border, so they never rely on colour alone. Keep that pattern for new toggles.
- Theme: colour tokens live on `:root` (light by default, matching the sibling Lost Cities scorer). The dark values are repeated in two places, under `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }` and `:root[data-theme="dark"]`, so update both together.
- Icons are inline SVG path strings wrapped by the `SVG()` helper (24×24 viewBox, stroke-based, `currentColor`).
- Minus signs in displayed numbers use U+2212 (`−`) through `fmt()`, not a hyphen.
- UI copy uses British spelling and sentence case.
