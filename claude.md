# CLAUDE.md — yvens94.github.io

## Project overview
Personal blog and portfolio site for Jean Yvens Alberus, hosted on GitHub Pages.
All site files live in `docs/`. There is no build step — everything is plain HTML/CSS/JS, deployed as-is.

## File map
```
docs/
  index.html       — Blog listing page (fetches posts.json, renders post cards + modal)
  about.html       — Bio/profile page with social links
  admin.html       — CMS: create/edit/publish/delete posts, manage bio & settings
  posts.json       — Flat JSON array of published posts (source of truth for the blog)
  assets/css/main.css  — Single shared stylesheet (dark theme, all pages)
  images/          — Profile photo and other images
```

## How posts work
- `posts.json` is the live post store. The blog reads it on every page load via `fetch()`.
- The admin panel authenticates with a GitHub Personal Access Token (PAT) stored in `localStorage`.
- Publishing a post → writes directly to `posts.json` on GitHub via the Contents API (no CI needed).
- Drafts live only in `localStorage` and are never pushed to GitHub until explicitly published.
- Saving as draft removes the post from `posts.json` on GitHub if it was previously live.
- Markdown is rendered client-side with `marked.js` (loaded from jsDelivr CDN).

## Design system
- Dark background: `--bg: #0d0d0f`, surface: `--surface: #161618`
- Accent: `--accent: #a78bfa` (purple), `--accent2: #c4b5fd`
- Primary button: blue→purple→red gradient
- Font: Segoe UI / system-ui stack, base size 20px
- Breakpoint: 680px (single-column below)

## Key conventions
- No build tools, no npm, no bundler. Edit HTML/CSS/JS directly.
- All three pages share `assets/css/main.css` — changes there affect every page.
- Social icon SVGs are inline (no icon font or sprite sheet).
- CSS attribute selectors (`[href*="linkedin"]`, etc.) are used to brand social buttons by platform — do not add classes to individual anchors for this purpose.
- Bio and display name are stored in `localStorage` under the key `jya_bio` and read dynamically; they are not hard-coded in the HTML.
- GitHub repo config (owner/repo/branch/path) defaults are set in `admin.html` under `DEFAULTS` and can be overridden via the Settings tab.

## What NOT to do
- Do not introduce a build system, package.json, or bundler unless explicitly asked.
- Do not split CSS into multiple files.
- Do not add TypeScript, React, or any framework.
- Do not add comments or docstrings to code that was not changed.
- Do not add error handling for scenarios that cannot happen (e.g. missing DOM elements that are always present).
