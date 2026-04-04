# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Architecture

Single-page static web app — one `index.html` with embedded `<style>` and `<script>`. No frameworks, no build step, no external dependencies.

## Running

Open `index.html` directly in a browser, or:

```sh
docker build -t pe-calc . && docker run -p 8080:80 pe-calc
```

## Structure

- `index.html` — the entire application (HTML + CSS + JS)
- `Dockerfile` — nginx:alpine serving the HTML file
- `docker-compose.yml` — local orchestration
- `.github/workflows/docker.yml` — CI: build and push to GHCR on push to main

## Key design decisions

- **i18n**: All UI strings go through the `i18n` object and `t(key)` function in JS. Languages: `en`, `sv`. Adding a language means adding a key to the `i18n` object.
- **Theme**: Three-state (light/dark/system) via `data-theme` attribute on `<html>` and CSS custom properties in `:root` / `[data-theme="dark"]`.
- **Persistence**: Language and theme stored in `localStorage` (`lang`, `theme` keys).
- **Calculation**: All inputs trigger `calculate()` which recomputes every output value. No debouncing needed for this scale.

## P/E formula reference

```
pe15 = Σ(t=1..15) (1+g)^t / (1+r)^t
terminalPE = ((1+g)^15 * (1+tg)) / ((r - tg) * (1+r)^15)
justifiedPE = pe15 + terminalPE  (terminal can be toggled off)
targetPrice = justifiedPE * eps
buyPrice = targetPrice * 0.80
```
