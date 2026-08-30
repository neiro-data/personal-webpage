# Plan — Scaffold the real Astro build (astro-modern) + GitHub Pages

## Brief

The design decision is made: **`astro-modern`** (full-width minimal, large type, single accent
color). This phase replaces the static mockup with a **real Astro project**, recreating the same
four pages (Home/About, CV, Projects, Blog) as Astro pages/components, porting the existing
placeholder content **verbatim** from `variants/astro-modern/*.html`, and wiring **GitHub Pages
deployment via GitHub Actions** on push to `main`. GitHub account is `neiro-data`; deploys as a
**project site** (`neiro-data.github.io/personal-webpage`) — no account rename, no custom domain.
`/variants/` is moved to `deprecated/variants/` as reference. The root `README.md` is rewritten to
document the real dev/build/preview/deploy workflow. No content is invented in this phase; no push
or merge to `main`.

## Goals & constraints

- Deliverable: an Astro project at repo root that builds cleanly, 4 pages matching the mockup,
  a Pages deploy workflow, an updated `README.md`, delivered on a branch via PR.
- Hard constraints:
  - **Content is ported verbatim** — same dummy name (`Nelson Eiró`), role, About blurb, 3
    projects, 2 blog stubs, CV sections. No new copy, no real personal data.
  - **Never push or merge to `main`.** Branch → commit → PR. Landing is a human action.
  - **No Claude session links or session trailers** in commit messages or the PR body.
  - Node toolchain only (`npm`). No Python; `python-conventions` and the Python `test-automator`
    gates are **N/A** this phase.
  - `/variants/**` stays untouched and must not be broken by the scaffold.
- Assumptions (noted, non-blocking):
  1. **npm** as the package manager (zero-config, matches the Actions `setup-node` cache default).
  2. Astro 5.x, `output: 'static'`, **no UI framework integration** — the design is typography-only.
  3. **Hand-written CSS ported from `variants/astro-modern/style.css`**, not Tailwind. The
     stylesheet is 17 lines; a build-time CSS framework is unjustified overhead here.
  4. Blog posts stay **inline in `blog.astro`** for now (they are 2 dummy stubs). Astro content
     collections are deferred to the first real post — noted as a follow-up, not built now.
  5. Deployed as a **project site** at `/personal-webpage/`. Account is `neiro-data`, confirmed by
     the human — no rename, no custom domain.

## Structure

Scaffold **at the repo root** — not in `/app` or `/site`.

```
/astro.config.mjs           # site + base for GitHub Pages
/package.json               # dev / build / preview scripts
/tsconfig.json              # from astro's strict preset
/.gitignore                 # node_modules, dist, .astro
/.github/workflows/deploy.yml
/src/
  layouts/BaseLayout.astro  # <head>, .wrap, header+nav, footer
  components/Nav.astro      # base-aware active-link nav
  pages/index.astro         # Home/About
  pages/cv.astro
  pages/projects.astro
  pages/blog.astro
  styles/global.css         # ported from variants/astro-modern/style.css
/public/                    # favicon etc.
/deprecated/variants/       # moved from /variants/, untouched content
/README.md                  # rewritten
/plan-*.md                  # kept
```

**Why root, not a subdir:** this repo hosts exactly one project. Root is the idiomatic Astro
layout, keeps `npm run dev` working from the repo root the user already launches Claude from, and
avoids a `working-directory:` on every Actions step. `/deprecated/variants/` does not collide:
Astro only consumes `src/`, `public/`, and the root config files, so a stray top-level directory is
inert.

**Why move `/variants/` to `/deprecated/variants/` (not delete, not leave in place):** the human
asked to keep it available but out of the way now that the decision is made and content is ported.
It costs nothing (not built, not deployed). `deprecated/` signals it's historical reference, not
part of the live project.

## Risks

- **GitHub Pages base path.** A project site serves from `/personal-webpage/`; hardcoded absolute
  links (`/cv`) will 404. Mitigation: every internal link goes through `import.meta.env.BASE_URL`
  (or Astro's `<a href={\`${base}cv\`}>`), and step 7 verifies links against `npm run preview`,
  which honours `base` — opening `dist/` directly does not.
- **Pages not enabled / wrong source.** The workflow fails or silently no-ops if Pages source is
  not set to "GitHub Actions" in repo settings. Mitigation: called out as a human prerequisite in
  the README and the PR body.
- **Silent content drift** during the HTML→Astro port. Mitigation: port page by page and diff the
  rendered text against the mockup; acceptance criterion 3 makes this explicit.
- **Scope creep** into content collections, MDX, dark mode, analytics, real content. Mitigation:
  out of scope by assumption 4; log them in the README as follow-ups.

## Plan

1. **Branch first:** `git checkout -b feat/astro-scaffold` from `main`. Confirm
   `git rev-parse --show-toplevel` is this repo before any command. `git mv variants
   deprecated/variants` as its own step (preserve history), commit separately before scaffolding.
2. Scaffold Astro at root: `npm create astro@latest . -- --template minimal --typescript strict
   --no-install --no-git` (empty-dir prompt must be answered to preserve `deprecated/`, `README.md`,
   `plan-*.md`), then `npm install`. Verify `git status` shows no deletions under `deprecated/`.
3. Configure `astro.config.mjs`: `site: 'https://neiro-data.github.io'`,
   `base: '/personal-webpage'`.
4. Port styles: `deprecated/variants/astro-modern/style.css` → `src/styles/global.css`, imported once in
   `BaseLayout.astro`. Keep the `--accent` custom property and existing class names
   (`.wrap`, `.top`, `.hero`, `.role`).
5. Build `BaseLayout.astro` + `Nav.astro` (title prop, active-link state, base-aware hrefs), then
   the four pages, pasting the mockup body content verbatim.
6. Add `.github/workflows/deploy.yml`: trigger `push: [main]` + `workflow_dispatch`; permissions
   `contents: read`, `pages: write`, `id-token: write`; `concurrency: pages`; jobs
   `withastro/action@v3` (or checkout → setup-node 20 w/ npm cache → `npm ci` → `npm run build` →
   `actions/upload-pages-artifact` with `dist/`) then `actions/deploy-pages@v4`.
7. **Verify:** `npm run build` exits 0; `npm run preview` serves all four pages at the `base`
   prefix with no 404s and no broken nav links; workflow YAML parses (`actions/workflow-parser`,
   `yq e . .github/workflows/deploy.yml`, or the GitHub Actions editor).
8. Rewrite `README.md`: what the site is, `npm run dev/build/preview`, the deploy story and the
   human prerequisite (Settings → Pages → Source: GitHub Actions), the `deprecated/variants/` note,
   and the open follow-ups (real content, content collections).
9. Commit in logical chunks, push the **branch**, open a PR. No trailers, no session links, no
   merge — the human lands it.

## Delegation

**Yes — delegate steps 2–6 to `frontend-developer`.** This is real toolchain work (npm scaffold,
Astro layouts/components/routing, CSS port, Actions YAML) rather than planning, and it is a single
coherent concern owned end to end by one specialist. Bounded brief: scope limited to repo root +
`src/**` + `.github/workflows/**`; inputs are `deprecated/variants/astro-modern/*.html` and
`style.css` (already moved there in step 1) plus this plan's Structure section; out of scope are
`/deprecated/**` edits, any new content, any push or merge to `main`. Expected output: a working
build, the file tree above, and a short note of deviations.

Steps 1, 7, 8, 9 stay with the orchestrator/human (git hygiene, verification, README, PR).

**Pipeline note:** No Python and no application logic, so `python-conventions` and `test-automator`
do not apply — verification is step 7 (build exits 0, preview renders, YAML valid). A short
`code-reviewer` pass over `astro.config.mjs` and `deploy.yml` is worthwhile (base-path and
permissions correctness are the two easy things to get wrong); a review of the `.astro` markup is
low value. `ui-designer` is not needed — the design is already fixed by the mockup.

## Acceptance criteria

- [ ] `npm install && npm run build` succeeds from a clean checkout; `dist/` contains 4 HTML pages.
- [ ] `npm run preview` serves Home/About, CV, Projects, Blog with working nav under the `base`
      prefix; no 404s, no console errors.
- [ ] Rendered text matches `deprecated/variants/astro-modern/*.html` verbatim — same name, role,
      About blurb, 3 projects, 2 blog stubs, CV sections. Nothing invented.
- [ ] `/deprecated/variants/**` content is byte-identical to the pre-move `/variants/**` and is not
      part of the build output.
- [ ] `.github/workflows/deploy.yml` is valid YAML, triggers on push to `main`, and uses the
      `upload-pages-artifact` → `deploy-pages` flow with the correct permissions.
- [ ] `README.md` documents dev/build/preview, deploy status, the Pages settings prerequisite, and
      the open follow-ups.
- [ ] Work is on a branch with an open PR; `main` has no direct commits; no session trailers
      anywhere in commits or the PR body.

## State summary

- **Decisions:** Astro at **repo root** (single-project repo, idiomatic, no `working-directory`
  churn); **npm**; hand-written CSS ported from the mockup (no Tailwind); no UI framework
  integration; blog posts inline, content collections deferred; `/variants/` **moved** to
  `/deprecated/variants/`; deploy as a **project site** with `site:
  'https://neiro-data.github.io'`, `base: '/personal-webpage'`; account `neiro-data`, no rename, no
  custom domain — all confirmed by the human.
- **Files:** `deprecated/variants/astro-modern/{index,cv,projects,blog}.html`, `style.css`,
  `HANDOFF.md` (sources, moved from `variants/` in step 1); `astro.config.mjs`, `package.json`,
  `src/**`, `.github/workflows/deploy.yml`, `README.md` (to create/update);
  `plan-personal-webpage.md` (prior phase).
- **Blockers:** none.
- **Open questions:** none outstanding — username, rename, domain, and `/variants/` handling all
  confirmed by the human.
- **Next actions:** branch + move `variants/` → `deprecated/variants/` (step 1) → delegate steps
  2–6 to `frontend-developer` → verify (7) → README (8) → PR (9). Human still needs to enable
  Settings → Pages → Source: GitHub Actions before the first deploy.
