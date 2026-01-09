# Repo guide for AI coding agents

This is a Hugo-based personal website that uses the `hugo-coder` theme (bundled under `themes/hugo-coder`). The goal of these instructions is to help an AI agent make precise, low-risk changes and be productive immediately.

Key facts
- Site config: `hugo.toml` — baseURL, language, theme, params and menus live here.
- Content: `content/` — markdown files with Hugo front matter. Example: talks are in `content/talks.md`.
- Theme: `themes/hugo-coder/` — override layout templates and partials here when site-level changes are insufficient.
- Static assets: `static/` — public-facing assets (images, fonts). Use `assets/` for SCSS/JS processed by Hugo Pipes.
- Generated site: `public/` — build output (committed here). Avoid committing generated files for new projects; this repo includes them.

Build & dev workflow
- Serve locally: `hugo server -D` (or `make serve`). This runs a live server at http://localhost:1313.
- Build production: `hugo --minify` (or `make build`). Output is written to `public/`.
- Clean generated artifacts: `make clean` removes `public/` and `resources/_gen`.

Conventions & patterns
- Theme-first: Most visual/layout changes are in `themes/hugo-coder/layouts/partials/` and `themes/hugo-coder/layouts/_default/` — prefer overriding templates in `layouts/` only when site-specific customization is needed.
- SCSS pipeline: `assets/scss/` and `themes/hugo-coder/assets/scss/` contain SCSS sources. `resources/_gen/assets/scss` holds compiled results. Use Hugo Pipes for compilation; avoid manual CSS concatenation.
- Menus & params: Site menus are declared in `hugo.toml` under `[languages.en].menu.main`. Social links and visual options are in `[params]`.
- Front matter: Content uses standard Hugo front matter; keep `date`, `title`, and `tags` consistent. For new content, follow existing files in `content/`.

Testing & CI
- CI workflow: `.github/workflows/build.yml` runs on pushes/PRs to `main`. It installs Hugo and runs `hugo --minify`, then uploads `public/` as an artifact.
- When modifying content or templates, run `hugo server -D` locally and check rendered output visually. Automated tests are not present in this repo.

Safe-edit rules for AI agents
- Never delete `themes/hugo-coder/` — it is the canonical theme source.
- When changing templates, prefer adding minimal overrides in `layouts/` (site root) so theme updates remain possible.
- Do not remove files in `public/` without user confirmation; this folder is used as committed output and may be intentionally present.
- Keep commits small and descriptive. Follow `CONTRIBUTING.md` style (imperative prefix: `feat(...)`, `fix(...)`, `docs:`).

Useful file references (examples)
- Site config: [hugo.toml](hugo.toml)
- Theme docs: [themes/hugo-coder/README.md](themes/hugo-coder/README.md)
- Layout overrides: [layouts/partials/footer.html](layouts/partials/footer.html)
- Example generated output: public/index.html

If unsure
- Run the dev server and inspect the affected page before changing `public/` or merging large template changes.
- Ask for clarification when a requested change affects site publishing (DNS, baseURL, or external analytics keys).
