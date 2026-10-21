# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal GitHub Pages site (`severn-gg.github.io`). The whole site is a single static file, `index.html`, with inline CSS and JS. There is no build step, package manager, linter, or test suite; GitHub Pages serves the file from `main` as-is. To preview, open `index.html` in a browser or run `python3 -m http.server` in the repo root.

## Structure notes

- `index.html` holds everything: a `<style>` block, the markup, and two inline `<script>` blocks at the bottom. The only external dependency is p5.js (pinned to 1.9.4, loaded from cdnjs); avoid adding others unless the user asks.
- The cmatrix-style background is a p5 instance-mode sketch that renders into `#matrix` (fixed, blurred, dimmed to look distant). `.mask` sits between it and `<main>`: a radial gradient in the page background colour that is dark in the centre for readability and fades out at the edges. Both are `position: fixed; z-index: 0`, so their stacking relies on DOM order, with `<main>` at `z-index: 1` above them. The sketch's background colour `rgb(11, 15, 26)` duplicates `--bg` and the mask gradient, so change all three together. Under `prefers-reduced-motion` the sketch draws a static frame and stops.
- The "Hello World!" heading is plain text in the HTML. The script splits it into per-letter `<span class="letter">` elements and sets a `--i` CSS variable on each. The CSS uses `--i` to stagger the `pop-in`, `wave`, and `shine` animation delays, so changing the heading text or the class names requires updating the script and CSS together.
- The bio section fades in after the heading animation (`animation-delay: 1.6s`). A `prefers-reduced-motion` media query disables the animations, so new animations should be added to that block too.
- Page language is Indonesian (`lang="id"`), and the CSS and JS comments are in Indonesian. Match that when adding comments.
- The bio section shows `pro gif.gif` (an `<img class="pro-gif">`) in place of a text paragraph. The filename contains a space, so it is referenced as `pro%20gif.gif`; keep the two in sync if the file is renamed.
