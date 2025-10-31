# mdutli.github.io

Personal learning log built with Jekyll and the GitHub Pages `minimal` theme.

## Local Setup

1. Install Ruby dependencies once per machine:
   ```bash
   bundle install
   ```
2. Run the site locally with drafts enabled:
   ```bash
   bundle exec jekyll serve
   ```
3. Build the static output exactly as GitHub Pages will publish it:
   ```bash
   bundle exec jekyll build
   ```

## Content Workflow

1. Draft outlines in `_drafts/` using the `YYYY-MM-DD-title.md` naming pattern once ready to publish.
2. Store supporting media in `assets/<slug>/` and reference them with relative paths.
3. Write posts with front matter that declares at least `title`, optional `summary`, and `tags`; keep a single H1 and descend heading levels sequentially.
4. Promote a draft by moving it into `_posts/` with its final publish date in the filename.
5. Validate the site structure before committing:
   ```bash
   bundle exec jekyll doctor
   npx markdownlint-cli2 "_posts/**/*.md" "_drafts/**/*.md"
   ```
   Optionally spot-check links while the dev server runs:
   ```bash
   npx linkinator http://localhost:4000 --skip "localhost"
   ```
6. Open a pull request with a concise summary, verification checklist, and any relevant screenshots.
7. Merge approved changes into `main`, push to `origin`, and delete the feature branch locally and remotely.
