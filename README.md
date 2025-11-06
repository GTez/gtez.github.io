# gtez.com - Personal Website

This is the source code for Jesse Houston's personal website, hosted at [gtez.com](http://gtez.com).

## Technology Stack

- **Jekyll**: Static site generator natively supported by GitHub Pages
- **GitHub Pages**: Free hosting with automatic builds
- **Markdown**: Simple format for writing content

## How to Add a New Blog Post

Adding a new blog post is simple and can be done on both Linux and Mac without any special development environment:

### Step 1: Create a New Markdown File

1. Navigate to the `_posts` directory
2. Create a new file with the naming convention: `YYYY-MM-DD-title-of-post.md`
   - Example: `2025-11-06-my-new-post.md`

### Step 2: Add Front Matter

At the top of your markdown file, add the following header (called "front matter"):

```markdown
---
layout: post
title: "Your Post Title Here"
date: 2025-11-06
---
```

### Step 3: Write Your Content

Below the front matter, write your blog post in markdown format. Some examples:

```markdown
## This is a heading

This is a paragraph with **bold text** and *italic text*.

- Bullet point 1
- Bullet point 2

1. Numbered list item 1
2. Numbered list item 2

[This is a link](https://example.com)

![This is an image](path/to/image.jpg)
```

### Step 4: Commit and Push

```bash
git add _posts/YYYY-MM-DD-your-post.md
git commit -m "Add new blog post: Your Post Title"
git push
```

GitHub Pages will automatically build and publish your site within a few minutes!

## Editing Existing Content

### Update the About Page

Edit `about.md` and commit/push your changes.

### Update the Home Page

Edit `index.md` and commit/push your changes.

## Local Preview (Optional)

If you want to preview your site locally before pushing:

1. Install Ruby and Bundler (see [Jekyll installation guide](https://jekyllrb.com/docs/installation/))
2. Run `bundle install`
3. Run `bundle exec jekyll serve`
4. Visit `http://localhost:4000` in your browser

**Note:** Local preview is completely optional. You can write and publish posts without ever running Jekyll locally - GitHub will build it for you automatically!

## Site Structure

```
.
├── _config.yml          # Site configuration
├── _layouts/            # HTML templates
│   ├── default.html
│   └── post.html
├── _posts/              # Blog posts (markdown files)
├── assets/
│   └── css/
│       └── style.css    # Site styles
├── about.md             # About page
├── blog.md              # Blog index page
├── index.md             # Home page
└── CNAME                # Domain configuration
```

## Markdown Editors

You can use any text editor to write posts, but here are some good markdown editors:

**Cross-platform:**
- Visual Studio Code (with markdown preview)
- Typora
- Mark Text

**Mac:**
- iA Writer
- Ulysses
- MacDown

**Linux:**
- ReText
- Ghostwriter
- Remarkable

## Domain Configuration

The site is configured to use the custom domain `gtez.com` via Cloudflare. The CNAME file contains the domain configuration, and DNS settings should be configured in Cloudflare to point to GitHub Pages.
