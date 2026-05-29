# frozen_string_literal: true

source "https://rubygems.org"

# Build the theme from the local gemspec (runtime deps live there).
gemspec

# Plugins used by the demo site in example/ but not required by the theme itself.
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-paginate"
  gem "jekyll-gist"
  gem "jekyll-sitemap"
  gem "jekyll-seo-tag"
  gem "jekyll-toc"
end

# Math rendering is done client-side via the KaTeX CDN in _includes/head.html,
# so kramdown-math-katex is optional. Uncomment to render math at build time too:
# gem "kramdown-math-katex"

gem "faraday-retry"
