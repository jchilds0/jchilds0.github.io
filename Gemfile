source "https://rubygems.org"

gem "jekyll-theme-chirpy", "~> 6.4"

group :jekyll_plugins do
  # If you have any plugins, put them here!
  # gem "jekyll-xxx", "~> x.y"
end

group :test do
  gem "html-proofer", "~> 4.2"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", ">= 1", "<3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?

gem 'rogue'

gem "webrick", "~> 1.7"

gem "json"
