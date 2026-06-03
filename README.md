# Nord Newsletter — `jekyll-theme-nord-newsletter`

A config-driven Jekyll theme on the [Nord](https://www.nordtheme.com/) palette, extracted
from [systemhalted.in](https://systemhalted.in). It ships a responsive post grid, archive /
category / tag pages, a client-side search overlay, a keyboard-driven command-line overlay,
collection layouts, optional Giscus comments, and an optional newsletter CTA — all
configurable from `_config.yml`.

## Screenshots

The home page in both Nord themes (toggle with the `t` key):

| Dark | Light |
| --- | --- |
| ![Nord Newsletter home page in the dark theme](https://raw.githubusercontent.com/systemhalted/jekyll-theme-nord-newsletter/main/docs/screenshots/home-dark.png) | ![Nord Newsletter home page in the light theme](https://raw.githubusercontent.com/systemhalted/jekyll-theme-nord-newsletter/main/docs/screenshots/home-light.png) |

## Features

- Responsive post feed with featured images and excerpts.
- Light/dark Nord theme (defaults to `prefers-color-scheme`).
- Optional **glazed** (frosted-glass) look layered over either mode.
- A single masthead **theme menu** button opens a popover with two rows — *Mode*
  (Light / Dark) and *Style* (Flat / Glazed). Mode and glaze are remembered
  separately; `t` toggles mode and `Shift+G` toggles glaze from the keyboard.
- Client-side search overlay (elasticlunr) that indexes posts **and** every output
  collection — no external service.
- Keyboard shortcuts: `?` (help), `/` or `s` (search), `t` (theme), `Shift+G` (glazed look),
  `m` (sidebar), `g h/f/k/e/a` (go to Home / Featured / Newsletter / Emacs / About).
- A `webcmd` command-line overlay for power users.
- Archive, category (taxonomy-grouped), tag, and featured pages.
- Collection layouts for newsletters and an Emacs-style note wiki.
- Optional [Giscus](https://giscus.app) comments and social share buttons.
- Sidebar navigation driven by `_config.yml`.
- Math rendering via the KaTeX CDN; table of contents via `jekyll-toc`.

## Install

Add the theme to your site's `Gemfile`:

```ruby
gem "jekyll-theme-nord-newsletter"
```

Then in `_config.yml`:

```yaml
theme: jekyll-theme-nord-newsletter
plugins:
  - jekyll-paginate
  - jekyll-gist
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-feed
  - jekyll-toc
paginate: 8
paginate_path: "/page:num"
```

Install and serve:

```sh
bundle install
bundle exec jekyll serve --livereload
```

## Configuration

Everything site-specific is read from `_config.yml`; nothing is hardcoded in the theme.

| Key | Purpose |
| --- | --- |
| `title`, `tagline`, `description`, `url`, `baseurl` | Site identity (used in the masthead, footer, and SEO). |
| `author.name` / `author.email` | Author identity; email powers the footer and comment fallback. |
| `author.linkedin` / `author.github` | Footer social links (rendered only when set). |
| `author.avatar` | Footer avatar path. Defaults to `/assets/images/avatar.jpeg`. |
| `google_analytics_id` | Enables `gtag.js` when set. |
| `giscus.*` | Enables Giscus comments. See below. |
| `newsletter_cta.*` | Newsletter CTA content + optional Kit embed. See below. |
| `search.suggestions` | List of suggestion chips shown in the empty search overlay. |
| `sidebar.items` | Sidebar navigation (list of `{title, url}`). |

### Comments (Giscus)

Comments load only when `giscus.repo` is set, and only on posts with `comments: true` in
their front matter:

```yaml
giscus:
  repo:        owner/repo
  repo_id:     R_xxxxxxxx
  category:    Comments
  category_id: DIC_xxxxxxxx
  mapping:     pathname   # optional, defaults to pathname
```

Get these values from <https://giscus.app>. Without them, the comments section renders empty
and shows an email fallback for no-JS readers.

### Newsletter CTA

The `newsletter-cta` include is used on the newsletter landing page and at the end of each
issue. The Kit (ConvertKit) embed only loads when both `kit_uid` and `kit_url` are set:

```yaml
newsletter_cta:
  title:       "My Newsletter"
  lede:        "Occasional essays by email. Free, no spam."
  path:        /newsletter/          # landing page the footer links to
  feed_path:   /feed.xml             # RSS link in the CTA
  footer_blurb: "Get My Newsletter by email, or follow the blog by RSS."  # optional; overrides the footer subscribe sentence
  kit_uid:     abcdef1234            # optional
  kit_url:     https://you.kit.com   # optional
```

> **Note:** `newsletter` is also a common collection name (`site.newsletter`). The CTA config
> intentionally uses the `newsletter_cta` key to avoid colliding with the collection.

### Categories and tags

Category groupings live in `_data/taxonomy.yml`. The gem ships an example taxonomy as a
default — drop your own `_data/taxonomy.yml` in your site to override it (Jekyll merges site
data over theme data). The `categories` page groups categories by theme, and the post layout
uses the same taxonomy to suggest related posts. Tags are generated from post front matter.

## Layouts

| Layout | Use |
| --- | --- |
| `default` | Base chrome (masthead, sidebar, footer, search, shortcuts). |
| `page` | Standard content page. |
| `post` | Blog post: meta, featured image, TOC, share buttons, related posts, comments. |
| `category` | A single category archive. |
| `collections` | Generic collection index (set `collection_name` in front matter). |
| `newsletter` | A newsletter issue (kicker, reading time, CTA, prev/next). |
| `emacs` | A note-wiki entry (TOC, tags). |

### Post front matter

```yaml
---
layout: post
title: Sample Post
date: 2026-01-31
categories: [Technology]
tags: [jekyll, notes]
comments: true
featured: true
toc: true
featured_image: /assets/images/hero.jpg
featured_image_alt: Brief alt text
featured_image_caption: Photo credit or context
description: One-line summary for previews and search.
---
```

### Pages

The theme ships layouts; archive-style pages are **starter templates** in `example/` you can
copy to your site root: `index.html`, `archives.html`, `categories.html`, `tags.html`,
`featured.html`, `404.md`, plus `the-newsletter.html` (newsletter index), `emacs.html`
(collection index), and `webcmd/index.html` (command-line page).

## Collections

Output collections are searchable automatically. To add one:

1. Define it under `collections:` with `output: true` (set `collections_dir` if you keep
   collections in a subfolder).
2. Add docs under `collections/_<name>/`.
3. Add a `defaults` rule to assign a layout, e.g. `layout: newsletter`.
4. Optionally add a listing page using `layout: collections` with `collection_name: <name>`.

Exclude any document from search with `search_exclude: true` in its front matter.

## Demo site

A runnable demo lives in `example/`:

```sh
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --source example --destination example/_site --livereload
```

## Assets and styling

- CSS: `assets/css/nord.css` (hand-written, CSS custom properties — no Sass build).
- JS: `assets/js/script.js` (UI + search), `assets/js/webcmd.js` (search index + command
  line, Liquid-processed), `assets/js/elasticlunr.min.js`.
- Fonts, Font Awesome, and KaTeX load from CDNs in `_includes/head.html`.
- Favicons and the web manifest live in `assets/`.

## License

[MIT](LICENSE.md) © Palak Mathur
