# CLAUDE.md

Guidance for working in this repo. Read this first each session.

## What this is

Manu Rathi's personal website & technical blog, served at **https://manurathi1.github.io**
(a GitHub Pages *user site* — the repo name must stay `manurathi1.github.io` and the
default branch serves the site root).

Focus of the writing: **quant finance and AI/LLM engineering, explained from first
principles** — math-heavy, chart-heavy technical deep-dives. The site title "101" is
**intentional** (reads as "fundamentals / intro-level"). Do not rename it.

## Source of truth for Manu's work

**`../resume`** (i.e. `/Users/manurathi/Documents/src/resume`) is the canonical,
frequently-updated record of Manu's roles, projects, skills, and metrics. It is far more
current and complete than anything in this repo. **Before writing any bio, About page,
projects/work section, or post that references his experience, read from there** — start
with:
- `../resume/resumes/detailed.md` — exhaustive reference
- `../resume/work/**` — per-company / per-project deep dives (e.g. Windmill Capital → FinLens AI)

Treat that repo as read-only context; don't edit it from here.

## Current stack (being migrated)

Today the site is **Jekyll + the Minimal Mistakes theme, fully vendored** into the repo
(`_layouts/`, `_includes/`, `_sass/` are copies of the theme, not a gem/remote_theme).
It builds with `bundle exec jekyll build`. Content is 4 posts under `_posts/YYYY/Mon/`,
with assets in a parallel tree under `assets/images/YYYY/Mon/`.

## Direction (decided)

We are revamping the site onto **Quarto** with a **distinctive, custom-branded** design —
chosen because equations, charts, executable code, and Jupyter notebooks are first-class
in Quarto, which fits the content. Planned target structure:

```
_quarto.yml            site config, nav, theme
index.qmd              landing page (hero + featured writing + projects)
about.qmd              bio (sourced from ../resume)
projects.qmd           work showcase (FinLens AI, Agentic Smallcases, quant infra)
posts/
  _metadata.yml        shared post defaults
  <slug>/index.qmd     one folder per post; assets colocated with the post
theme/custom.scss      custom branding, light + dark mode
```

Organization is **metadata-driven** via frontmatter (`categories`, `tags`, and a `series`
field for multi-part deep-dives) — not folder-by-year. **Preserve existing post URLs** on
migration (aliases) to avoid breaking indexed links. Deploy via a GitHub Action that builds
Quarto and publishes to Pages, replacing the native Jekyll build.

Migration runs *alongside* the live Jekyll site; retire Jekyll only after the Quarto site is
verified live.

## Conventions

- Don't commit `.DS_Store` or build output (`_site/`, `.quarto/`) — see `.gitignore`.
- Commit only when asked; branch off `master` first if starting a larger change.
- Canonical contact (keep consistent with `../resume`): manurathi.jaipur@gmail.com,
  GitHub `manurathi1`, Twitter `manurathi2`, LinkedIn `manurathi`.
