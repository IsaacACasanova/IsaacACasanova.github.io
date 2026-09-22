# Mono theme for isaaccasanova.com

A second theme that lives beside Menca. One line in `_config.yml` switches between them.
Menca's files (`_layouts/`, `_includes/`, `_sass/`) are not modified.

## Install (once)

1. Copy everything in this folder into the repo root. Nothing here overwrites an existing file
   except `index.html` (step 2) and the two profile images.

2. Open your **current** `index.html`. Move everything below its front matter into
   `_includes/menca/home.html` (replacing the placeholder comment). Then replace `index.html`
   with the one in this folder. If your old front matter used a layout other than `default`,
   tell me — the new `index.html` assumes `layout: default`.

3. In `_config.yml`, add:

   ```yaml
   # Theme switch — comment this line out to go back to Menca.
   layouts_dir: _themes/mono/layouts

   home_post_count: 5
   ```

   and update the identity fields (these were still Menca defaults):

   ```yaml
   title: Isaac Casanova
   description: Mobile engineer in New York. Notes on iOS, privacy, and the ethics of building software.
   url: "https://isaaccasanova.com"
   ```

4. Optional but recommended, in `_config.yml`:
   - `google-analytics: UA-180637374-1` — Universal Analytics stopped processing data in 2023.
     Remove it, or replace with a GA4 ID / Plausible. The mono layout doesn't load analytics at all.
   - `color_scheme: dark` — only Menca reads this; harmless to leave.

5. `_pages/about.suggested.md` is a draft About page written from your résumé. Rename it to
   `about.md` (replacing the old one) if you want it, or cherry-pick paragraphs.

## Switch themes

- **Mono:** `layouts_dir: _themes/mono/layouts` present in `_config.yml`.
- **Menca:** comment that line out.

Restart `jekyll serve` after changing it — `_config.yml` isn't watched.

## Edit content

- `_data/roles.yml` — the work timeline. One entry per role; one line per project.
  `logo` is optional (omit it for no tile); optional `url` links the company name.
- `_data/facts.yml` — the four lines under your name.
- `_data/links.yml` — the "elsewhere" list.
- `images/logos/` — company marks. Add `logo_invert: true` for dark marks, `logo_fill: true`
  for marks that carry their own background.
- `css/mono.css` — all styling; colours are the CSS variables at the top.

## Notes

- Posts and pages keep `layout: post` / `layout: page`. Both themes provide those names.
- The Contact page still renders Menca's form include; it works, but it's unstyled under mono.
  If you keep the contact form, I'll write a mono version of that include.
- `/posts/` is a new page listing every post; the homepage shows the latest `home_post_count`.
- The theme toggle stores its choice in `localStorage` and follows the system preference before
  a choice is made.
