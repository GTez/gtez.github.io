# Getting Shit Done - Personal Website

This is the source code for Jesse Houston's personal website, hosted at [gtez.com](http://gtez.com).

## Technology Stack

- **Jekyll**: Static site generator natively supported by GitHub Pages
- **GitHub Pages**: Free hosting with automatic builds
- **Markdown**: Simple format for writing content
- **Design**: Dark mode with green/gold gaming-inspired aesthetic

## Quick Start: Adding a Blog Post

The easiest way to add a blog post:

1. Create a file in `_posts/` named `YYYY-MM-DD-title.md` (use TODAY's date)
2. Add the header and write your content
3. Commit and push
4. GitHub builds automatically in ~2 minutes

## How to Add a New Blog Post (Detailed)

### Step 1: Create a New Markdown File

Navigate to the `_posts` directory and create a new file:

**Important:** Use the current date (or past date), not a future date!

```bash
cd _posts
```

**Naming convention:** `YYYY-MM-DD-title-of-post.md`

Examples:
- ✅ `2025-11-05-my-thoughts-on-game-design.md`
- ✅ `2025-11-05-building-great-teams.md`
- ❌ `2025-11-06-future-post.md` (Jekyll skips future dates!)

### Step 2: Add Front Matter

At the top of your markdown file, add this header:

```markdown
---
layout: post
title: "Your Post Title Here"
date: 2025-11-05
---
```

**Note:** The date in the filename and front matter should match!

### Step 3: Write Your Content

Below the front matter, write your blog post in markdown format:

```markdown
## Section Heading

This is a paragraph with **bold text** and *italic text*.

### Subsection

Here's how to add various elements:

**Lists:**
- Bullet point 1
- Bullet point 2

**Numbered lists:**
1. First item
2. Second item

**Links:**
[Link text](https://example.com)

**Images:**
![Alt text](/assets/images/your-image.png)

**Code:**
Inline `code` or code blocks:

\```javascript
function example() {
  return "Hello World";
}
\```

**Quotes:**
> This is a blockquote
```

### Step 4: Preview Locally (Optional)

Before pushing, you can preview locally:

```bash
jekyll serve --host=0.0.0.0
```

Visit `http://localhost:4000` in your browser. The site will auto-reload when you save changes.

**Troubleshooting:** If you see "Skipping: has a future date", change the post date to today or earlier.

### Step 5: Commit and Push

```bash
git add _posts/2025-11-05-your-post.md
git commit -m "Add blog post: Your Post Title"
git push
```

**GitHub Pages will automatically build and publish within 2-3 minutes!**

You can check the build status in your repository's "Actions" tab on GitHub.

## Updating Other Content

### Update the About Page

1. Edit `about.md`
2. Commit and push:
   ```bash
   git add about.md
   git commit -m "Update about page"
   git push
   ```

### Update the Home Page

The home page shows the big "GET SHIT DONE" text and two links. To change it:

1. Edit `index.md`
2. Commit and push

**Note:** The home page has no header/navigation - it's intentionally minimal!

### Adding Images to Blog Posts

1. Add your image to `assets/images/`
2. Reference it in your post:
   ```markdown
   ![Description](/assets/images/your-image.png)
   ```

Example:
```bash
# Add image
cp ~/Downloads/screenshot.png assets/images/

# Reference in post
![My Screenshot](/assets/images/screenshot.png)

# Commit everything
git add assets/images/screenshot.png _posts/2025-11-05-my-post.md
git commit -m "Add blog post with screenshot"
git push
```

## Local Preview & Development

### First Time Setup

1. Install Ruby (if not installed):
   - **Mac:** `brew install ruby` or use rbenv
   - **Linux:** `sudo apt-get install ruby-full` or use rbenv

2. Install Jekyll:
   ```bash
   gem install bundler jekyll
   ```

### Running Locally

```bash
# Navigate to the site directory
cd ~/path/to/gtez.github.io

# Start the server
jekyll serve --host=0.0.0.0

# Or if you have a Gemfile:
bundle exec jekyll serve --host=0.0.0.0
```

Visit `http://localhost:4000` in your browser.

**The server will auto-reload when you save changes!**

### Common Jekyll Commands

```bash
# Serve with drafts visible
jekyll serve --drafts

# Serve and watch for changes
jekyll serve --watch

# Build without serving
jekyll build

# Clean generated files
jekyll clean
```

**Note:** Local preview is completely optional! You can write and publish posts without ever running Jekyll locally - GitHub builds automatically.

## Site Structure

```
.
├── _config.yml           # Site configuration (title, URL, etc.)
├── _layouts/             # HTML templates
│   ├── default.html      # Main layout (header, footer, nav)
│   └── post.html         # Blog post layout
├── _posts/               # Blog posts (markdown files)
│   └── YYYY-MM-DD-title.md
├── assets/
│   ├── css/
│   │   └── style.css     # All site styles (dark mode, colors)
│   └── images/           # Images for about page and blog posts
├── about.md              # About page with career timeline
├── blog.md               # Blog index (lists all posts)
├── index.md              # Home page (big GSD text)
├── CNAME                 # Domain configuration (gtez.com)
└── README.md             # This file
```

### Key Files to Know

- **`_config.yml`**: Site title, description, URL - restart Jekyll after editing
- **`assets/css/style.css`**: All styling (colors, fonts, layout)
- **`_layouts/default.html`**: Header/footer/navigation template
- **`about.md`**: Your career timeline with images
- **`index.md`**: Home page (minimal GSD design)

## Workflow Tips

### Writing on Different Computers

You can write and publish from any computer with git:

1. **Clone the repo** (first time only):
   ```bash
   git clone https://github.com/GTez/gtez.github.io.git
   cd gtez.github.io
   ```

2. **Pull latest changes** (every time):
   ```bash
   git pull
   ```

3. **Create your post**, commit, and push

### Quick Commands Reference

```bash
# Create new post
touch _posts/2025-11-05-my-post.md

# Check what changed
git status
git diff

# Commit and push
git add .
git commit -m "Add blog post"
git push

# Pull latest
git pull
```

## Markdown Editors

You can use any text editor, but these make writing easier:

**Recommended:**
- **Visual Studio Code** - Free, with live markdown preview
- **Typora** - Clean WYSIWYG markdown editor
- **iA Writer** (Mac) - Distraction-free writing

**Other Options:**
- Mark Text (cross-platform)
- Ulysses (Mac)
- MacDown (Mac)
- ReText (Linux)
- Ghostwriter (Linux)

## Troubleshooting

### "Skipping: has a future date"
- Your post date is in the future
- Change the date in both the filename and front matter to today or earlier

### Images not showing
- Check the path: `/assets/images/your-image.png`
- Make sure you committed and pushed the image file
- Image paths are case-sensitive!

### Changes not appearing on gtez.com
- Wait 2-3 minutes for GitHub to rebuild
- Check the "Actions" tab on GitHub for build status
- Hard refresh your browser (Ctrl+F5 or Cmd+Shift+R)

### Jekyll won't start locally
- Make sure Ruby is installed: `ruby --version`
- Install Jekyll: `gem install jekyll bundler`
- Try: `bundle install` then `bundle exec jekyll serve`

## Design & Colors

The site uses a dark gaming-inspired aesthetic:

- **Background:** Dark (#0f0f0f)
- **Primary Accent:** Goose green (#8b9556)
- **Secondary Accent:** Gold (#d4af37)
- **Text:** Light gray (#e8e8e8)

To modify colors, edit `assets/css/style.css` and change the CSS variables at the top.

## Domain & Hosting

- **Domain:** gtez.com (managed via Cloudflare)
- **Hosting:** GitHub Pages (free, automatic)
- **SSL:** Automatic via GitHub Pages
- **Builds:** Automatic on every push to main branch

The CNAME file tells GitHub which domain to use.
