source "https://rubygems.org"

# Use the github-pages gem to ensure compatibility with GitHub Pages
# This gem pins all dependencies to versions that are compatible with GitHub Pages
gem "github-pages", "~> 231", group: :jekyll_plugins

# If you prefer to use Jekyll directly without GitHub Pages compatibility:
# gem "jekyll", "~> 4.3"

group :jekyll_plugins do
  # Essential Jekyll plugins
  gem "jekyll-feed", "~> 0.17"        # Generate an Atom feed
  gem "jekyll-sitemap", "~> 1.4"      # Generate a sitemap
  gem "jekyll-seo-tag", "~> 2.8"      # SEO meta tags
  gem "jekyll-gist", "~> 1.5"         # Embed gists
  
  # Optional plugins (uncomment as needed)
  # gem "jekyll-paginate", "~> 1.1"   # Pagination support
  # gem "jekyll-redirect-from", "~> 0.16" # Redirect support
  # gem "jemoji", "~> 0.12"           # Emoji support
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library for platform-specific gems
platforms :mingw, :x64_mingw, :mswin do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance enhancement (optional but recommended)
gem "webrick", "~> 1.7"
