[![Netlify Status](https://api.netlify.com/api/v1/badges/b3f36500-b15d-478f-8686-3d85ff93a7bb/deploy-status)](https://app.netlify.com/sites/chulapa-jekyll-gem/deploys)

# chulapa-jekyll-101

This repo is the source of <https://dieghernan.github.io/chulapa-jekyll-101/>, that is a website deployed with GH Pages and Jekyll 4.0, using a GitHub Action.
Additionally is deployed also in [Netlify](https://chulapa-jekyll-gem.netlify.app/) setting the Ruby version to 3.4 ([Environment variable method](https://docs.netlify.com/configure-builds/manage-dependencies/#ruby)).

Uses the `chulapa-jekyll` gem (`">= 2.0.0"`)

## Setup

### [_config.yml](_config.yml)


```yaml
theme: chulapa-jekyll
github: [metadata]
repository: dieghernan/chulapa-jekyll-101

# remote_theme: dieghernan/chulapa (comment or delete this line)

...

```


### [Gemfile](Gemfile)

```ruby
source 'https://rubygems.org'	
# Latest jekyll release
gem "jekyll", "~> 4.4.1" 
gem "chulapa-jekyll", "~> 2.0.0"

...
```


### [.github/workflows/build-chulapa-gh-pages.yml](.github/workflows/build-chulapa-gh-pages.yml)


```yaml
# Based on https://github.com/actions/starter-workflows/blob/main/pages/jekyll.yml
name: Deploy Chulapa Jekyll site to Pages

on:
  push:
    branches: ["master","main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      GITHUB_PAT: ${{ secrets.GITHUB_TOKEN }}
      JEKYLL_GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # Needed to work out-of-the-box with jekyll-github-metadata
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Ruby
        # https://github.com/ruby/setup-ruby/releases/tag/v1.207.0
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1' # Not needed with a .ruby-version file
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically
          cache-version: 1 # Increment this number if you need to re-download cached gems
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Build with Jekyll
        run: |
          bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"
        shell: bash
        env:
          JEKYLL_ENV: production
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
       
  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```