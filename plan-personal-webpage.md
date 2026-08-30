# Plan — Four demo design variants for the personal site

## Brief

Before committing to a single template, scaffold **four side-by-side static demo pages** in this
repo — one per design direction from `plan-first-commit.md` (Astrofy-style, Modern Astro, Jekyll
minimal, Hugo terminal/portfolio). Each is a **low-effort static HTML/CSS mockup**, not a real
framework build: enough to judge the look and the page structure (Home/About, CV, Projects, Blog),
nothing more. The user picks one afterward; only then do we scaffold the real framework and wire
GitHub Pages.

## Goals & constraints

- Deliverable: repo skeleton + 4 comparable demo pages + 1 handoff note per variant + top-level README.
- Hard constraints:
  - **No GitHub Pages / Actions / deploy config in this phase.**
  - No Node/Ruby/Go toolchains, no `npm install`, no build step. Plain HTML + CSS only.
  - Each variant must be viewable by opening a file in a browser (double-click or `python3 -m http.server`).
  - All four render the **same dummy content** so the comparison is about design, not copy.
- Assumptions (noted, not blocking):
  1. Static HTML mockups are acceptable fidelity for a look-and-feel decision (explicitly requested).
  2. Tailwind-ish variants are approximated with hand-written CSS or a CDN link, not a build pipeline.
  3. Dummy content = placeholder name/role, 3 fake projects, 2 fake blog entries, stub CV sections.
  4. Nav links between the 4 pages within a variant may be stubbed (`#`) except where trivially real.

## Structure

```
/README.md                  # how to view + compare all four
/plan-first-commit.md       # original brainstorm (kept)
/plan-personal-webpage.md   # this file
/variants/
  index.html                # comparison hub: 4 cards linking to each variant
  astrofy/        index.html  cv.html  projects.html  blog.html  style.css  HANDOFF.md
  astro-modern/   (same file set)
  jekyll-minimal/ (same file set)
  hugo-terminal/  (same file set)
```

Rationale: one directory per variant keeps CSS namespaced and lets any variant be deleted wholesale
once the choice is made. `/variants/index.html` is the entry point for comparison. Nothing sits at
repo root that would later collide with a real Astro/Jekyll/Hugo scaffold.

## Design intent per variant

| Variant | Look |
| --- | --- |
| `astrofy` | Card/sidebar layout, avatar, rounded cards, DaisyUI-ish palette, light+airy |
| `astro-modern` | Full-width minimal, large type, generous whitespace, single accent color |
| `jekyll-minimal` | Classic document/blog feel, serif body, narrow measure, understated links |
| `hugo-terminal` | Dark, monospace, terminal-prompt accents, high contrast |

## Risks

- **Mockup ≠ real template.** Fidelity gap could mislead the pick. Mitigation: each `HANDOFF.md`
  states plainly that this approximates the upstream template and links the real repo/theme.
- **Scope creep into a real build.** Mitigation: no package manifests committed in this phase.
- **Divergent dummy content across variants** would bias the comparison. Mitigation: write the content
  block once, reuse verbatim in all four.

## Plan

1. Create `/variants/` and the four subdirectories.
2. Draft the shared dummy content block (About blurb, 3 projects, 2 blog stubs, CV sections).
3. Build variant 1 (`astrofy`): 4 pages + `style.css`. Establish the page-structure template.
4. Replicate pages 2–4 (`astro-modern`, `jekyll-minimal`, `hugo-terminal`) — same markup skeleton and
   content, distinct CSS and layout treatment.
5. Write `HANDOFF.md` per variant: what's stubbed, what needs real content, how to run/preview, and
   which upstream template/theme it approximates + migration effort.
6. Write `/variants/index.html` (comparison hub) and the top-level `README.md`.
7. Verify: open the hub, confirm all 4 load standalone, no broken internal links, no 404 assets.

Delegation: none warranted — single coherent front-end mockup task, tightly coupled shared content.
Optionally `ui-designer` for step 4 if the four styles come out visually too similar; not planned by
default.

**Pipeline note:** no Python and no application logic, so `python-conventions` and `test-automator`
are not meaningfully applicable. Verification here is HTML validity + manual visual check (step 7).
A light `code-reviewer` pass is optional and low value for static mockups.

## Acceptance criteria

- [ ] `/variants/index.html` opens locally and links to all four variants.
- [ ] Each variant has Home/About, CV, Projects, Blog pages that render standalone with no build step.
- [ ] The four are visually clearly distinct; content is identical across them.
- [ ] Each variant has a `HANDOFF.md` covering stubs, TODO content, preview instructions, upstream ref.
- [ ] Root `README.md` explains how to view and compare, and states the decision is still open.
- [ ] No GitHub Pages workflow, `CNAME`, or deploy config anywhere in the repo.

## State summary

- **Decisions:** static HTML/CSS mockups (not real framework scaffolds); `/variants/<name>/` layout;
  deploy deferred to the follow-up phase after the user picks.
- **Files:** `plan-first-commit.md` (source spec), `plan-personal-webpage.md` (this plan),
  `/variants/**` (to create), `README.md` (to create).
- **Blockers:** none.
- **Open questions (non-blocking):** real name/handle/social URLs for the dummy content — placeholders
  used until provided; whether the final repo will be renamed `<username>.github.io`.
- **Next actions:** execute steps 1–7; then a follow-up session scaffolds the chosen framework and
  wires GitHub Pages.
