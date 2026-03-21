# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bundle install                              # Install Ruby dependencies
bundle exec jekyll serve --livereload       # Run local dev server at localhost:4000
bundle exec jekyll build                    # Build site to _site/
```

CI builds with `JEKYLL_ENV=production` and a `--baseurl` flag set by GitHub Pages.

## Architecture

This is a Jekyll 4.4 personal site with two distinct pages:

- **Homepage** (`index.html`) — uses `_layouts/default.html`, styled with `assets/css/main.scss`
- **CV page** (`cv.html`) — uses `_layouts/compress.html` (HTML minification), all content driven by `_data/cv.yml`

### Data-driven CV

All CV content lives in `_data/cv.yml`. The CV page assembles content through 13 partials in `_includes/cv/` (sidebar, experiences, education, projects, publications, skills, etc.). To update any CV section, edit `_data/cv.yml` only — the templates read it automatically.

### Theming

Six color skins are in `_sass/skins/` (blue, turquoise, green, berry, orange, ceramic). The active theme is `ceramic`, imported at the top of `assets/css/cv.scss`. To switch themes, change that import line.

### External dependencies (CDN)

Bootstrap 5.3.3 and Font Awesome 6.7.2 are loaded from CDN in both `_includes/head.html` and `cv.html` directly — they are not bundled locally.

### Blog

Posts go in `_posts/` as standard Jekyll markdown files. The blog index is at `blog/index.html` with an Atom feed at `blog/atom.xml`.

Supported post front matter: `title`, `date`, `tags` (array). Add `<!--more-->` in the body to control excerpt cut-off.

The blog index groups posts by year (`group_by_exp`), shows excerpts and reading time, and has a client-side JS search filter (no plugin). Reading time is computed via Liquid: `content | number_of_words | plus: 199 | divided_by: 200`.

The post layout (`_layouts/post.html`) includes a reading progress bar, breadcrumb, sticky TOC (JS-generated from `h2`/`h3` headings), social share links, and a related posts section. All logic is inline JS in the layout — no external dependencies.
