source "https://rubygems.org"
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby "3.0.3"

gem "rails", "~> 7.0.0.rc1"
gem "propshaft", ">= 0.4.1"
gem "pg", "~> 1.1"
gem "puma", "~> 5.0"
gem "jsbundling-rails", ">= 0.2.2"
gem "cssbundling-rails", ">= 0.2.7"
gem "jbuilder", "~> 2.11"
gem "tzinfo-data", platforms: %i[ mingw mswin x64_mingw jruby ]
gem "bootsnap", ">= 1.4.4", require: false

group :development, :test do
  gem "debug", ">= 1.0.0", platforms: %i[ mri mingw x64_mingw ]
end

group :development do
  gem "web-console", ">= 4.1.0"
end

group :test do
  gem "capybara", ">= 3.26"
  gem "selenium-webdriver", ">= 4.0.0"
  gem "webdrivers"
end
