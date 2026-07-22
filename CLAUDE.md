# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page "link-in-bio" site (Linktree-style) for the cosplay photographer A.Z.Production, served by **GitHub Pages** at the custom domain in `CNAME` (`azproductioncosp.me`). There is no build step, no package manager, and no dependencies — the browser loads the files as-is.

## Files

- `index.html` — the entire page: a header (avatar + logo) and a `<ul class="b-content">` of social/shop link buttons.
- `index.css` — all styling.
- `CNAME` — the custom domain for GitHub Pages. Deleting/renaming it changes the live URL.
- `404.html` — the GitHub Pages not-found page.
- `*.webp` / image assets — served directly; referenced by URL.

## Deploy

Commit and push to `main`. GitHub Pages publishes automatically; there is nothing to build or run locally beyond opening `index.html` in a browser.

## Conventions

- **CSS classes use BEM**: `b-block`, `b-block__element`, `b-block__element_modifier` (e.g. `b-content__link-button_youtube`). Each link button gets a `_<platform>` modifier that sets only its brand `background-color`. Adding a new link means: a new `<li class="b-content__item">` in `index.html` plus a matching `_<platform>` rule in `index.css`.
- **Dark mode** is driven by `prefers-color-scheme` via the `--text`/`--bg` CSS variables in `:root`. Keep new colors working on both black and white backgrounds.
- **Icons** are inline SVGs embedded directly in the markup (no icon font, no external requests). Prefer `fill="currentColor"` so an icon inherits the button's text color; use a fixed color only when reproducing a brand mark.
- **The Email link is intentionally obfuscated** — the address is XOR+base64 encoded and decoded in the inline `onclick` to copy it to the clipboard, keeping it out of the page source for scrapers. Do not replace it with a plaintext `mailto:`; if the address changes, re-encode it the same way rather than hardcoding it in the clear.
- Analytics is Google `gtag` (`UA-68597572-3`) loaded at the bottom of `index.html`.
- **Never add a commit tag crediting Claude**.