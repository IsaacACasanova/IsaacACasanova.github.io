# isaaccasanova.com

Source for my personal site: a Jekyll site hosted on GitHub Pages at
[www.isaaccasanova.com](https://www.isaaccasanova.com).

Two themes live in this repo. **Mono**, the one that's live, is a single-column site with a work
timeline, a writing list, and a dark/light toggle. **Menca**, by
[Artem Sheludko](https://jekyllthemes.io/developers/artem-sheludko), is the previous theme and is kept
intact so it can be switched back on.

## Run it locally

```bash
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>. Jekyll rebuilds on file changes, but not on changes to `_config.yml`;
restart the server after editing that.

## Switch themes

One line in `_config.yml`:

```yaml
layouts_dir: _themes/mono/layouts   # Theme switch. Comment out for Menca.
```

Present: mono. Commented out: Menca. Nothing else needs to change.

## Edit content

Everything on the mono homepage comes from `_data/`:

- `_data/facts.yml` — the lines under the name on the homepage.
- `_data/roles.yml` — the work timeline, newest first. Per role: `company`, `title`, `years`, an optional
  `url` (links the company name), an optional `logo` (omit it for no tile; add `logo_invert: true` for
  dark marks that should flip in dark mode, `logo_fill: true` for marks that carry their own background),
  and `projects`, each with a `name`, optional `summary`, and optional `impact` (shown on its own line
  beneath).
- `_data/links.yml` — the "elsewhere" list.

Pages are in `_pages/`: `about.md`, `contact.html` (Menca's Formspree form, styled for mono),
`posts.md` (every post), `tags.html`.

Posts go in `_posts/` as `YYYY-MM-DD-slug.markdown` with `layout: post`, `title`, `date`, `tags`, and optionally
`description` and `image`. Permalinks are `/:title`. The homepage lists the latest `home_post_count`
(set in `_config.yml`); `/posts/` lists them all.

## Where the mono theme lives

```
_themes/mono/layouts/   default, post, page
_includes/mono/         homepage and tags-page bodies
_includes/menca/        the Menca equivalents (moved out of index.html and _pages/tags.html)
index.html              dispatcher: includes whichever theme's homepage is active
css/mono.css            all mono styling; colours are the CSS variables at the top
images/favicon.svg      favicon, plus favicon.ico and images/apple-touch-icon.png
```

Menca's own files (`_layouts/`, `_includes/` outside `mono/` and `menca/`, `_sass/`) are unmodified.

A few mechanics worth knowing:

- The stylesheet link carries the build time as a query string, so a deploy always busts the browser cache.
- The theme toggle stores its choice in `localStorage` and follows the system preference until a choice
  is made.
- Mono loads no analytics, comments, search, or newsletter.

## Deploy

GitHub Pages builds `main` on every push, usually within a minute. Work happens on a branch and lands
through a pull request.

The Pages custom domain is `www.isaaccasanova.com`, and `url` in `_config.yml` matches it. The bare
domain redirects to `www` over HTTP; over HTTPS it fails certificate validation because GitHub's
certificate covers only `www`. Setting the Pages custom domain to the bare domain would fix that.

## License

- The code in this repo that I wrote (the mono theme, `_config.yml`, `index.html`, the dispatcher
  includes) is under the [MIT License](LICENSE).
- The content (posts in `_posts/`, the About and Contact text, `_data/*.yml`, and the images in
  `images/`) is © Isaac Casanova, all rights reserved. It is not covered by the MIT License.
- The Menca theme files (`_layouts/`, `_sass/`, and `_includes/` outside `mono/` and `menca/`) are by
  Artem Sheludko and remain under Menca's own license.
