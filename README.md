# Chulapa from RubyGems

This repository demonstrates the **chulapa-jekyll** gem on [GitHub Pages](https://dieghernan.github.io/chulapa-jekyll-gem/) and [Netlify](https://chulapa-jekyll-gem.netlify.app/).

[![Netlify Status](https://api.netlify.com/api/v1/badges/b3f36500-b15d-478f-8686-3d85ff93a7bb/deploy-status)](https://app.netlify.com/sites/chulapa-jekyll-gem/deploys)

## Getting started

1. Clone or fork this repository.
2. Edit `_config.yml`: set your title, description, author and repository.
3. Set `url` to your site origin and `baseurl` to `/repository` for a project site or `""` for a root site. The Pages workflow sets the deployment base path automatically.
4. Replace the sample posts, pages, images and navigation links.
5. Enable GitHub Pages with **GitHub Actions** as its source.

## Run locally

Install Ruby and Bundler, then run these commands from the repository directory:

```sh
bundle install
bundle exec jekyll serve --host localhost --baseurl ""
```

Open <http://localhost:4000>. Restart Jekyll after editing `_config.yml`.
The Pages workflow uses Ruby 3.4 and this template uses Jekyll 4.4.

## Configuration

[`_config.yml`](_config.yml) follows the current Chulapa configuration
structure:

- Site settings, social locales, author and optional JSON-LD publisher.
- Font Awesome, analytics, search and comment providers.
- Navigation, footer, fonts, skins and syntax highlighting.
- Pagination, collections, front matter defaults and Jekyll settings.

Blank settings use theme defaults where available. Replace the sample content
and identity settings before publishing. Image metadata must describe the actual
image.

The template uses Lunr search, four posts per blog page and a Markdown
cheatsheet collection. Autotheming is enabled with `lightskyblue` as the primary
color.

## Page options and examples

[`_pages/theme-options.md`](_pages/theme-options.md) demonstrates options
available in Chulapa 2.1.0: independent `seo_title` and `og_title`, a shared
`description`, social image metadata, page language, Open Graph locales,
`og_type: article`, `schema_image` and video metadata.

Use `canonical_url` only when a page should identify a different canonical URL;
ordinary pages use their generated URL. Set `robots: "noindex, follow"` for
pages such as search results, as shown in
[`_pages/search.md`](_pages/search.md). Robots metadata does not remove a page
from the sitemap; use `sitemap: false` when needed.

[`_pages/minimal-header.md`](_pages/minimal-header.md) demonstrates `layout:
minimal` with `show_header: true`.

See the complete [page and snippet reference](https://dieghernan.github.io/chulapa/docs/04-layouts), [site configuration](https://dieghernan.github.io/chulapa/docs/02-config) and [theming guide](https://dieghernan.github.io/chulapa/docs/03-theming).

## Included content

- Sample posts, a paginated blog and year, category and tag archives.
- Markdown and kramdown cheatsheets.
- A Bootstrap component demo and a 404 page.
- Lunr search, an Atom feed, an RSS feed and a generated sitemap.
- Custom include hooks in [`_includes/custom/`](_includes/custom/) and CSS in [`assets/css/`](assets/css/).
- Optional Algolia indexing configuration in [`algolia-search.yml`](algolia-search.yml).

## Theme updates

The site uses the installed RubyGems theme:

```yaml
theme: chulapa-jekyll
```

The Gemfile allows Chulapa 2.1 and later 2.x releases:

```ruby
gem "chulapa-jekyll", "~> 2.1"
```

Update the installed theme with:

```sh
bundle update chulapa-jekyll
```

Restart Jekyll or rebuild the site after updating. This installation uses the
packaged theme rather than downloading the repository with `remote_theme`.
Configuration, content and local overrides remain in this repository.

The Pages workflow reads Ruby 3.4 from `.ruby-version`. Set Ruby 3.4 in your
Netlify build environment as well. Netlify should run `bundle exec jekyll build`
and publish `_site`. Deployment settings are managed in Netlify.

Review the [Chulapa changelog](https://github.com/dieghernan/chulapa/blob/main/CHANGELOG.md) when updating.
