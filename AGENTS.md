# Repository Guidelines

## Project Structure & Module Organization
This repository is a Jekyll static site based on **al-folio**. Source content and site structure are intentionally separate from generated output.

Key locations:
- `_layouts/`, `_includes/`, `_sass/`, `_data/`, `_pages/`, `_posts/`, `_news/`, `_projects/`, and `assets/` contain the site source.
- `_config.yml` is the central site configuration.
- `bin/` holds helper scripts, while `lighthouse_results/` and `readme_preview/` are generated/auxiliary assets.
- `_site/` is the built output directory and should be treated as ephemeral.

## Build, Test, and Development Commands
Preferred local workflow is Docker-based:
- `docker compose up` starts a local site at `http://localhost:8080` and rebuilds on changes.
- `docker compose pull` refreshes the upstream image before starting.
- `docker compose -f docker-compose-slim.yml up` runs the slim image.
- `docker compose up --build` rebuilds the container image for Ruby/Jekyll changes.

Local legacy workflow without Docker:
- `bundle install`
- `bundle exec jekyll serve` launches the site at `http://localhost:4000`.
- `bundle exec jekyll build` produces static output in `_site/`.
- `purgecss -c purgecss.config.js` optionally removes unused CSS in `_site/assets/css/`.

Code quality tooling:
- `npx prettier . --check` for formatting checks.
- `npx prettier . --write` for local auto-formatting.
- `bundle exec jekyll build` before major content structure changes.

## Coding Style & Naming Conventions
Formatting is enforced by Prettier with liquid support and `.prettierrc` settings (`printWidth: 150`, `trailingComma: es5`). Pre-commit also checks trailing whitespace, EOF newlines, and YAML validity.

Use the existing naming patterns:
- Blog posts in `_posts/` follow `YYYY-MM-DD-title.md`.
- Keep front matter keys in lowercase and use 2-space YAML indentation.
- Keep generated/minified assets out of manual edits (`assets/css/main.scss`, `assets/js/*.min.js`, etc. are in `.prettierignore`).

## Testing Guidelines
There is no dedicated unit-test suite. Quality checks are site-oriented:
- `prettier` (formatting check)
- `lychee` (broken link check in workflows)
- `axe` (accessibility testing, manually triggered in CI)

After edits, run at least local build/render commands to catch template, include, and permalink issues before commit.

## Commit & Pull Request Guidelines
Use a clear, imperative commit title and keep the scope limited (example: `Update projects page content`). For PRs:
- open an issue first for feature or bug work,
- link the issue in the PR description,
- ensure local build succeeds,
- mention preview behavior changes.

## Security & Configuration Tips
Do not commit secrets, local credentials, or machine-specific settings in `_config.yml`. Verify personal profile/API values before deployment, and keep GitHub Pages/public branch settings aligned with your repository type (`<user>.github.io` vs project repo path).
