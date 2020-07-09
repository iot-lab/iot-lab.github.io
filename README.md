# IoT-LAB website

Code and content of the IoT-LAB website published at https://www.iot-lab.info, licensed under [CC BY SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/).

## Installation
With Ruby setup, you can install Jekyll by running the following in your terminal:

    gem install jekyll bundler

Then install dependencies defined in `Gemfile` with bundler:

    bundle install

You will be able to update your gem versions later with `bundle update`.

## Running

    bundle exec jekyll serve

This restricts your Ruby environment to only use gems set in your `Gemfile`.

To take drafts post into account, use the `--drafts` option.

You can also add livereload for hot-reloading the browser page when the sources change:

    bundle exec jekyll serve --livereload

## Update publications
Publications are managed with a Google scholar public profile. To update them on Jekyll you have to export the list to Bibtex format on your computer:

1. Log in to [Google Scholar](https://scholar.google.com) with IoT-LAB account
2. Click *My citations*
3. Click the leftmost checkbox (i.e. *Title*) on the bar at the top of the list of citations
4. Click *Export>BibTex>Export all my articles*
5. *Save as...* page in publications.bib file

Finally you have to generate the YAML file in the *_data* directory and commit it.

    sudo apt-get install pandoc-citeproc
    pandoc-citeproc -y publications.bib > _data/publications.yml
