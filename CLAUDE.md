# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Marketing site for the Hubbard Heights Men's Golf Club (Stamford, CT). One-page site with anchor-link navigation to membership, sponsors, photos, officers, news, and contact sections.

## Architecture

Everything lives in a single `index.html` — markup, `<style>`, and `<script>` are all inlined in that one file. There is no build system, package manager, framework, or test suite. To make any change, edit `index.html` directly.

Key structural notes when editing:

- **Section layout.** The top-level `<nav>` links point to `#id` anchors on sibling `<div class="section">` elements (`#home`, `#about`, `#sponsors`, `#photos`, `#membership`, `#officers`, `#news`, `#contact`). The scroll-spy JS at the bottom of the file reads `document.querySelectorAll('[id]')` — if you add a new section, give it an id and a matching nav link and it will light up automatically.
- **Fade-in animation.** Any element with class `fade-in` is picked up by an `IntersectionObserver` and transitions to `.visible` when scrolled into view. Re-use this class rather than adding new animation code.
- **Design tokens.** Brand colors are not variables — navy `#1a2a3a`, gold `#c8a84b`, green accent `#4a8c5c` are repeated inline. If restyling, grep for those hexes rather than assuming a variable exists.
- **Images.** The hero, sponsor logos, photo gallery, and social icons are hot-linked from `static.wixstatic.com` (legacy Wix CDN). They are not stored in this repo. Treat those URLs as external dependencies that could break.
- **Payments.** "Join Now" buttons on the four membership cards currently link to `https://www.paypal.com` as placeholders — they are not real PayPal buttons yet. Replace with hosted-button-id URLs when wiring up payments.
- **Contact form.** `handleSubmit` just calls `alert()` and resets the form — no backend, no email delivery. Anything real needs a form service (Formspree, Netlify Forms, etc.) or a backend.

## Deploying

There is no deploy command. The repo is served directly by GitHub Pages from `main`. Push to `main` and the live site updates in ~60 seconds. To preview locally, open `index.html` in a browser or run `python3 -m http.server` from the repo root.

## Domain / DNS

The custom domain is managed via Wix (DNS only) pointing at GitHub Pages. DNS changes happen in the Wix dashboard, not this repo.
