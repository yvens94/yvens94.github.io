# Progress log

A running journal of things learned while building this site.

---

## 2026-04-07

### CSS attribute selectors for brand styling

Instead of adding a class to every anchor tag, you can target elements by a substring of their `href`:

```css
.socials a[href*="linkedin"] { background: #0A66C2; }
.socials a[href*="instagram"] { background: linear-gradient(...); }
```

`[attr*="value"]` matches if the attribute *contains* the string anywhere. Useful for links where the URL is the natural identifier.

### SVG icons and `currentColor`

Inline SVG paths use `fill: black` by default. To make them inherit the surrounding text color (so they turn white on a dark background, for example), add:

```css
.socials svg { fill: currentColor; }
```

Then controlling `color` on the parent element controls the icon color too.

### GitHub Pages — no build step needed

Static HTML/CSS/JS in the `docs/` folder is served directly by GitHub Pages. No CI, no bundler, no npm. You can ship a change by just committing the file.

### Admin panel authentication pattern

The admin uses a GitHub Personal Access Token as the password. The PAT is validated by hitting `GET /repos/{owner}/{repo}` — if GitHub returns 200, the token is good. The PAT is stored in `localStorage` and used for all subsequent GitHub API calls. This means zero backend infrastructure.

### Writing directly to GitHub from the browser

The GitHub Contents API (`PUT /repos/{owner}/{repo}/contents/{path}`) lets you create or update a file entirely from client-side JavaScript. You need:

1. The file's current SHA (fetch it first with a GET to the same endpoint)
2. The new content encoded as base64
3. A commit message

---

<!-- Add new entries above this line, newest first -->
