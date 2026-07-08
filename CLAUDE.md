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

## Stack

**Quarto**, custom-branded, deployed via GitHub Actions
(`.github/workflows/publish-quarto.yml`) to GitHub Pages. Chosen because equations,
charts, executable code, and Jupyter notebooks are first-class in Quarto, which fits the
content.

```
_quarto.yml            site config, nav, theme
index.qmd              homepage (hero + writing-first post listing)
about.qmd              bio (sourced from ../resume)
projects.qmd           work showcase (FinLens AI, Agentic Smallcases, quant infra)
posts/
  _metadata.yml        shared post defaults
  <slug>/index.qmd     one folder per post; images colocated with the post
theme/
  light.scss           custom branding — light mode (default)
  dark.scss            custom branding — dark mode
  styles.css           small shared tweaks that don't need SCSS variables
static/                personal media not tied to a specific post (photos, resume PDF)
```

Organization is **metadata-driven** via frontmatter (`categories`, and a `series` field
for multi-part deep-dives) — not folder-by-year. Every migrated post carries `aliases:`
entries preserving its original Jekyll URL — preserve this pattern for any future URL
changes.

The site previously ran on Jekyll + a fully-vendored Minimal Mistakes theme; that has
been fully retired (files removed, not just excluded) now that Quarto is verified live.

## Conventions

- Don't commit `.DS_Store` or build output (`_site/`, `.quarto/`) — see `.gitignore`.
- Commit only when asked; branch off `master` first if starting a larger change.
- Canonical contact (keep consistent with `../resume`): manurathi.jaipur@gmail.com,
  GitHub `manurathi1`, Twitter `manurathi2`, LinkedIn `manurathi`.
- New posts: one folder under `posts/`, `index.qmd` inside, images alongside it. Use
  Quarto's native `$$ ... $$ {#eq-label}` equations (auto-numbered, cross-reference with
  `@eq-label`) rather than raw `\begin{equation}\tag{}` blocks.
