# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

Jesse Houston's personal site and blog, live at **https://gtez.com**. A Jekyll static
site hosted on GitHub Pages (repo: `GTez/gtez.github.io`). No JavaScript build step,
no framework — just Markdown, Liquid layouts, and one hand-written stylesheet.

## Layout of the repo

```
_config.yml              Site config: title, URL, author, SEO defaults, GA id, plugins
_layouts/default.html    Master template: <head> meta, JSON-LD, nav, footer
_layouts/post.html       Blog post wrapper (inherits default)
_includes/analytics.html GA4 snippet, production-only
_posts/                  Blog posts, YYYY-MM-DD-slug.md
index.md                 Home page (big "GET SHIT DONE" text, no nav)
about.md                 Career page with inline <figure> images
blog.md                  Post index, iterates site.posts
assets/css/style.css     All styling (~500 lines, CSS custom properties at top)
assets/images/           All images
robots.txt               Static, not Liquid-processed
CNAME                    gtez.com — do not delete, GitHub Pages needs it
.github/workflows/jekyll.yml  Build + deploy
```

`_site/` and `.jekyll-cache/` are build output, gitignored, and stale in the working
tree — never edit them, never commit them. `Gemfile.lock` **is** committed on purpose,
so local and CI installs resolve identically; regenerate it with `bundle install` or
`bundle update` rather than editing it.

`CLAUDE.md` and `README.md` are listed under `exclude:` in `_config.yml`. Any new
top-level `.md` file is published to the live site and added to `sitemap.xml` unless
it is excluded there — check that before adding one.

## Deployment

Push to **`main`** → GitHub Actions builds and deploys to GitHub Pages. Live in
~1 minute. `workflow_dispatch` also allows manual runs from the Actions tab.
(The branch was renamed from `master` to `main` in September 2026; older commits and
run history still reference the old name.)

The workflow (`.github/workflows/jekyll.yml`) takes its Ruby version from
`.ruby-version`, runs
`bundle exec jekyll build` with `JEKYLL_ENV=production`, and deploys `_site/` via
`actions/upload-pages-artifact` + `actions/deploy-pages`. Concurrency group `pages`,
in-progress runs are not cancelled.

Check deploys with `gh run list --limit 5`.

DNS for gtez.com is managed through Cloudflare; SSL is handled by GitHub Pages.

## Local development

Ruby version is pinned in `.ruby-version` (3.3.0) and shared with CI. Requires
`bundle install` first — without it every command fails with
`Could not find gem 'github-pages'`.

```bash
bundle install                 # once, and after any Gemfile change
bundle exec jekyll serve       # http://localhost:4000, auto-reloads
bundle exec jekyll build       # one-shot build into _site/
```

Always use `bundle exec`. The `github-pages` gem pins **Jekyll 3.10**, not Jekyll 4 —
even though `gem list` may show Jekyll 4.x installed system-wide, and a bare `jekyll`
would use that wrong version. Anything written here must work on Jekyll 3.x syntax.

Local builds set `JEKYLL_ENV=development`, so Google Analytics is correctly absent
from local output. To reproduce a production build exactly:
`JEKYLL_ENV=production bundle exec jekyll build`.

## Adding a blog post

Create `_posts/YYYY-MM-DD-slug.md`. The date in the filename must not be in the
future — Jekyll silently skips future-dated posts and the post will simply not appear.

```markdown
---
layout: post
title: "Post Title"
date: 2025-11-05
description: One to two sentences, used for meta description and social cards.
keywords: comma, separated, terms
image: /assets/images/something.jpg
categories: [announcements, personal]
---
```

`description`, `keywords`, and `image` are optional but the site's SEO depends on
them — include all three on new posts and pages. Without `description` the layout
falls back to the post excerpt, then to `site.description`. Without `image` it falls
back to `site.default_image` (`/assets/images/jesse-houston.jpg`).

Post URLs are `/blog/:year/:month/:day/:title/` (set twice in `_config.yml`, under
both `permalink` and `collections.posts`).

## SEO conventions — important

All meta tags are **hand-written in `_layouts/default.html`**: title, description,
keywords, canonical, Open Graph, Twitter card, plus JSON-LD `Person` on every page
and `BlogPosting` on posts. Do not add `{% seo %}` — `jekyll-seo-tag` is listed in
`_config.yml` plugins but is never invoked, and calling it now would emit a second
set of duplicate tags.

Similarly, `jekyll-feed` generates `/feed.xml`, but `{% feed_meta %}` is not in the
layout, so there is no `<link rel="alternate">` discovery tag. `jekyll-sitemap`
generates `/sitemap.xml`, which `robots.txt` points at.

If you change the JSON-LD (`worksFor`, `alumniOf`, `jobTitle`), keep it consistent
with the prose in `about.md`.

`robots.txt` is static (no front matter, so no Liquid). It allows everything and
points at the sitemap. It previously carried `Disallow: /assets/`, which blocked
crawlers from both the Open Graph/Twitter card images and `style.css`; that was
removed, so don't reintroduce a blanket `/assets/` block.

## Styling

Edit `assets/css/style.css` directly. Colors are CSS custom properties on `:root`:

```css
--bg-primary: #0f0f0f;   --bg-secondary: #1a1a1a;
--text-primary: #e8e8e8; --text-muted: #a0a0a0;
--goose-green: #8b9556;  --gold: #d4af37;
--border: #2a2a2a;
```

Dark theme only, `.container` capped at 720px, breakpoints at 768px and 480px.
The home page is deliberately chrome-free: `<body>` gets `page-home` when
`page.url == '/'`, and `.page-home header { display: none }` hides the nav.

## Conventions

- Images go in `assets/images/`, referenced as `/assets/images/name.ext`.
  Paths are case-sensitive on GitHub Pages.
- Use `{{ '/path' | relative_url }}` for internal links in layouts and pages.
- Commit messages are short and imperative ("Add Google Analytics 4 tracking").
- Commit and push only when asked — a push publishes to the live site.
