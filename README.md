# Shuai's Blog

This repository hosts my personal blog for long-form essays on whatever I'm learning or building.

## Local development

1. Install Ruby (>= 2.7) and Bundler.
2. Install dependencies:
   ```bash
   bundle install
   ```
3. Start the preview server:
   ```bash
   bundle exec jekyll serve
   ```
4. Visit `http://localhost:4000` to inspect changes as you write.

## Content workflow

- Draft new posts in `_drafts/` using Markdown; move them into `_posts/` when ready to publish. File names should follow `YYYY-MM-DD-title.md`.
- Site-wide settings live in `_config.yml`; navigation is controlled by `_data/navigation.yml`.
- Images go in `images/` and are referenced with absolute paths such as `/images/figure.png`.

## Deployment

GitHub Pages rebuilds the site whenever changes land on the `master` branch. Push updates and the blog will refresh automatically.
