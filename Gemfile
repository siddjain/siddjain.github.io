source "https://rubygems.org"

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
gem "jekyll", "~> 3.8.5"

# from https://github.com/asciidoctor/jekyll-asciidoc-quickstart/blob/master/Gemfile
gem 'coderay', '~> 1.1.0'
gem 'rake-jekyll', '~> 1.1.0'

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.0"

# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
# gem "github-pages", group: :jekyll_plugins

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
  # from https://github.com/asciidoctor/jekyll-asciidoc-quickstart/blob/master/Gemfile
  gem 'jekyll-asciidoc', '~> 3.0.0'
  gem 'asciidoctor-diagram', '~> 2.0.5'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.0" if Gem.win_platform?

# WEBrick is an HTTP server toolkit that can be configured as an HTTPS server, a proxy server, and a virtual-host server.
gem "webrick", "~> 1.7.0"

# a low-level dependency; An XML toolkit for Ruby
gem "rexml", "~> 3.2.5"

# for syntax highlighting of source code
gem "pygments.rb", "~> 2.2.0"