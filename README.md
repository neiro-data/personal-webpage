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

Pages: Home/About, CV, Education and Certifications (split out of CV), Projects, Blog, Agents.
Home links out via GitHub/LinkedIn/mailto social icons (`src/components/SocialLinks.astro`), and
the site uses the Inter font throughout.

Blog posts live as markdown files in `src/content/blog/*.md`, parsed via an Astro content
collection (`src/content.config.ts`). `src/pages/blog/index.astro` lists posts (title, date,
summary); `src/pages/blog/[...slug].astro` renders each post's full content at its own route.

Projects page lists real public repos from GitHub, including individual subprojects under
`neiro-data/useful-tools` linked to their own subfolder.

## Design history

The `astro-modern` look was chosen after comparing four static HTML/CSS mockups
(astrofy, astro-modern, jekyll-minimal, hugo-terminal). Those mockups are kept for reference under
[`deprecated/variants/`](deprecated/variants/index.html) — not built, not deployed, safe to delete
once no longer needed. See `plan-personal-webpage.md` (mockup phase) and
`plan-astro-scaffold.md` (this phase) for the full history and decisions.
