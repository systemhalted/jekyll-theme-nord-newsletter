# Changelog

## 0.1.2

- README now shows light/dark home-page screenshots, served via absolute
  `raw.githubusercontent` URLs so they render on the RubyGems page as well as on GitHub.
- The `example/` demo site now auto-deploys to GitHub Pages on every push to `main`.

## 0.1.1

- Footer subscribe blurb is now configurable via `newsletter_cta.footer_blurb`. When unset,
  it falls back to the previous "Get <newsletter> by email, or follow the blog by RSS." text.

## 0.1.0

Initial release. Extracted from the systemhalted.in blog and made config-driven.

- Layouts: `default`, `page`, `post`, `category`, `collections`, `emacs`, `newsletter`.
- Includes: head, sidebar, footer, share buttons, post/collection list items, Giscus
  comments, newsletter CTA.
- Nord light/dark palette with a `t` keyboard toggle and `prefers-color-scheme` default.
- Client-side search overlay (elasticlunr) indexing posts and all output collections.
- Keyboard-driven command-line overlay (`webcmd.js`).
- Config-driven Giscus comments (`giscus.*`), newsletter CTA (`newsletter.*`), footer
  social links (`author.linkedin`, `author.github`), Google Analytics, sidebar, and
  search suggestions.
