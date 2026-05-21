# Ayumu Kawasaki — personal site

academicpages-based Jekyll site for Home / Projects / Publications.
Source content lives in `_pages/about.md` (Home), `_pages/projects.md`, `_pages/publications.md`.

## Local preview

Ruby 3.3.10 is pinned via mise (`../mise.toml`).

```bash
cd docs/others/HP/site
bundle install            # first run only
bundle exec jekyll serve --host 127.0.0.1 --port 4000 --livereload
# open http://127.0.0.1:4000/
```

Or via mise / VS Code tasks:

| What | mise | VS Code (Run Task) |
|---|---|---|
| Local server | `mise run serve` | HP: serve |
| One-shot build | `mise run build` | HP: build |
| Commit + push (deploy) | `mise run deploy` | HP: deploy |

> CV (`docs/others/CV/CV.pdf`) is intentionally **not** included on the site to keep it private.

## Deploy / publish

The deploy path is "push the Jekyll source — GitHub Actions builds it via `.github/workflows/pages.yml`".

### Current state

- Repo: <https://github.com/Kwskayumu/Kwskayumu.github.io> — **private** (work in progress).
- GitHub Pages is **not yet active** (Free plan cannot publish Pages from a private repo).
- Day-to-day pushes work fine: `mise run deploy` commits and pushes to the private repo.

### Going public (when ready)

Two commands flip everything on:

```bash
gh repo edit Kwskayumu/Kwskayumu.github.io --visibility public --accept-visibility-change-consequences
gh api repos/Kwskayumu/Kwskayumu.github.io/pages -X POST -f 'build_type=workflow'
```

First command flips repo visibility to public; second enables Pages with the GitHub Actions workflow as the build source. The next `mise run deploy` (or any push) will trigger a build, and the site appears at `https://Kwskayumu.github.io/`.

### Going back to private

```bash
gh repo edit Kwskayumu/Kwskayumu.github.io --visibility private --accept-visibility-change-consequences
```

(Pages itself will then go offline; the workflow remains but won't publish until the repo is public again.)

## Day-to-day workflow

- Edit `_pages/*.md` → save → livereload updates the local browser.
- Push changes: `mise run deploy` (single commit + push).

## Source of content

Draft text comes from `../HP_draft.md`. Update that file in lockstep so the
two stay in sync.
