# personal-webpage

Personal site, built with [Astro](https://astro.build) in the `astro-modern` style, deployed to
GitHub Pages.

## Development

```
npm install
npm run dev       # http://localhost:4321/personal-webpage/
```

## Build & preview

```
npm run build      # outputs to dist/
npm run preview    # serves dist/ under the /personal-webpage base, matching prod
```

## Deploy

Deploys automatically via `.github/workflows/deploy.yml` on every push to `main` (checkout → npm
ci → build → upload-pages-artifact → deploy-pages). Live at
**https://neiro-data.github.io/personal-webpage/**.

**One-time human prerequisite:** in the repo's Settings → Pages, set Source to **GitHub Actions**
before the first push to `main` — otherwise the workflow has nothing to deploy to.

## Content

Pages (Home/About, CV, Projects, Blog) currently hold **placeholder content** — a stand-in name,
role, About blurb, 3 fake projects, 2 fake blog stubs, and stub CV sections — carried over from the
design-comparison phase. Replacing it with real content is the next step, not done in this phase.

Blog posts are inline in `src/pages/blog.astro` for now; moving to Astro content collections is a
follow-up once there's real post content to manage.

## Design history

The `astro-modern` look was chosen after comparing four static HTML/CSS mockups
(astrofy, astro-modern, jekyll-minimal, hugo-terminal). Those mockups are kept for reference under
[`deprecated/variants/`](deprecated/variants/index.html) — not built, not deployed, safe to delete
once no longer needed. See `plan-personal-webpage.md` (mockup phase) and
`plan-astro-scaffold.md` (this phase) for the full history and decisions.
