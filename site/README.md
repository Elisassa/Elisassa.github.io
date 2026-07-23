# Personal site — Jekyll on GitHub Pages

A minimal, professional portfolio + blog. White background, IBM Plex type,
custom SVG category icons.

## Deploy (one-time, ~5 minutes)

1. On GitHub, create a repo named **`yourusername.github.io`**
   (replace with your actual username). Public repo.
2. Put all the files in this folder at the **root** of that repo and push:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/yourusername/yourusername.github.io.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root)**.
4. Wait 1–2 minutes, then open `https://yourusername.github.io`.

GitHub builds Jekyll for you — no local install needed.

## Before you publish — edit these

- `_config.yml` — your name, tagline, email, GitHub/LinkedIn usernames, and `url`
- `about.md` — fill in everything in `[brackets]`
- `_projects/volunteer-check-in-workflow.md` — review the wording; before
  adding the org name, exact thresholds, or screenshots, check what your
  confidentiality agreement allows

## Writing a new blog post

Create a file in `_posts/` named `YYYY-MM-DD-title.md`:

```markdown
---
title: "My post title"
lede: One-line summary shown under the title.
category: sharepoint   # optional — shows a small icon badge on the post
---

Your content in Markdown.
```

Push it — the blog page lists posts newest first with their publish date.
The category line is optional; if you include one, the post shows a small
icon badge (keys are defined in `_data/categories.yml`).

## Adding a new project

Create a file in `_projects/` (see the volunteer workflow file as a template)
with `title`, `summary`, `stack`, `role`, `timeline` in the front matter.
It appears on the home page and the Projects page automatically.

## Adding a new category

Add an entry in `_data/categories.yml` and drop a matching 24×24 line-style
SVG into `_includes/icons/`. That's it.
