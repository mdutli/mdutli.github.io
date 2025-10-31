# Repository Guidelines

## Project Structure & Module Organization
The site runs on Jekyll with the GitHub Pages `minimal` theme. Published articles belong in `_posts/` using the `YYYY-MM-DD-title.md` pattern so they list chronologically. Work-in-progress notes live in `_drafts/` until promoted. Store supporting files in `assets/<slug>/` and reference them with relative paths. Keep small helper automation in `scripts/`; each script should print a short usage banner. Pages such as the archive are regular Markdown files at the repo root (for example `archive.md`).

## Build, Test, and Development Commands
Install dependencies once per machine:  
`bundle install` — fetches the `github-pages` gem set pinned in the `Gemfile`.  
`bundle exec jekyll serve` — builds the site with drafts enabled, serves at `http://localhost:4000`, and reloads on save.  
`bundle exec jekyll build` — produces the `_site/` folder exactly as GitHub Pages will publish it.

## Coding Style & Naming Conventions
Front matter should declare `title`, optional `summary`, and `tags`. Stick to one H1 per post; nested headings descend sequentially. Wrap lines at roughly 100 characters to keep diffs tidy. Use fenced code blocks with language hints (```bash, ```python). Image filenames mirror their post slug (`assets/starting-the-learning-log/diagram.png`). Prefer ordered steps for procedures and finish each article with a short takeaway list.

## Testing Guidelines
Run `bundle exec jekyll doctor` after structural changes to catch missing front matter or Liquid errors. Lint Markdown with `npx markdownlint-cli2 "_posts/**/*.md" "_drafts/**/*.md"`. For larger updates, spot-check links via `npx linkinator http://localhost:4000 --skip "localhost"` while the dev server is running. Validate any shell snippets in a clean terminal before publishing.

## Commit & Pull Request Guidelines
History uses concise, imperative subjects (`Add shell session primer`). Limit each commit to one topical change and include the relevant post slug in the body when useful. Pull requests should provide a summary, screenshots if the layout changes, references to related issues, and a checklist of verification commands you ran (serve, build, lint). When a post adds substantial code, link to supporting repos or gists for cross-reference.

## Content Workflow Tips
Draft an outline (context → steps → lessons) before writing. Promote a draft by renaming it into `_posts/`; Jekyll will auto-publish on the next build. Close each post with a “What I’ll revisit” bullet list and cite external sources inline. Capture frequently reused snippets in `snippets.md` or convert them into scripts if they need parameters.
