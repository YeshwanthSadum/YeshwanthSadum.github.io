# Blog — Yeshwanth Sadum

Personal blog built with Jekyll, hosted at [YeshwanthSadum.github.io/blogs](https://YeshwanthSadum.github.io/blogs).

## Setup & Deploy

Since you already have `YeshwanthSadum.github.io`, copy these files into a `blogs/` folder inside that existing repo and use a GitHub Actions workflow to build it.

### 1. Copy files into your existing repo

```bash
# Clone your existing site repo
git clone https://github.com/YeshwanthSadum/YeshwanthSadum.github.io.git
cd YeshwanthSadum.github.io

# Create blogs subfolder and copy all blog files into it
mkdir blogs
cp -r /path/to/blog-repo-final/. ./blogs/
```

### 2. Add a GitHub Actions deploy workflow

Create `.github/workflows/deploy-blog.yml` in the **root** of your repo:

```yaml
name: Deploy Blog

on:
  push:
    branches: [main]
    paths:
      - 'blogs/**'

permissions:
  contents: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true
          working-directory: blogs

      - name: Build Jekyll site
        run: |
          cd blogs
          bundle exec jekyll build --destination ../_site_blogs

      - name: Deploy to gh-pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site_blogs
          destination_dir: blogs
```

### 3. Commit and push

```bash
git add blogs/ .github/
git commit -m "Add /blogs Jekyll site with deploy workflow"
git push origin main
```

### 4. Enable GitHub Pages (if not already)

- Repo → **Settings → Pages**
- Source: **Deploy from a branch**
- Branch: `gh-pages`, folder: `/ (root)`

Live at: **https://YeshwanthSadum.github.io/blogs**

---

## Writing a new post

Add a file to `blogs/_posts/` named `YYYY-MM-DD-your-title.md`:

```markdown
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
date: 2026-04-01
tags: [agents, evals]
---

Your content in Markdown.
```

Push to `main` — the workflow auto-rebuilds.

---

## Local preview

```bash
cd blogs
gem install bundler
bundle install
bundle exec jekyll serve
# Open http://localhost:4000/blogs
```
