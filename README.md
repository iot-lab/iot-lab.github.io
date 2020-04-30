# www
[WIP] new version of the FIT IoT-LAB website, based on Jekyll

## Installation
With Ruby setup, you can install Jekyll by running the following in your terminal:

    gem install jekyll bundler

Then install dependencies defined in `Gemfile` with bundler:

    bundle install

You will be able to update your gem versions later with `bundle update`.

## Running

    bundle exec jekyll serve

This restricts your Ruby environment to only use gems set in your `Gemfile`.
You can also add livereload for hot-reloading the browser page when the sources change:

    bundle exec jekyll serve --livereload
