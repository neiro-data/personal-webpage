# Handoff — astrofy variant

**Approximates:** [Astrofy](https://github.com/manuelernestog/astrofy), an Astro theme with a
card/sidebar personal-site layout (avatar, rounded cards, soft accent palette).

## What this is
A static HTML/CSS mockup only — no Astro, no build step, no components. Fidelity is "close enough
to judge layout and vibe," not a working port.

## Stubs / not real
- All nav links are real (4 pages exist) but there's no active-route highlighting logic — it's
  hardcoded per file via the `active` class.
- Avatar is a CSS gradient placeholder, not an image.
- Blog "Read more" links go to `#`.
- Dummy content (name, role, projects, blog, CV) is shared verbatim across all 4 variants — see
  root README.

## To preview
Open `index.html` directly in a browser, or from repo root:
```
python3 -m http.server -d variants/astrofy 8000
```

## Migration effort if chosen
Real Astrofy is an Astro + Tailwind + DaisyUI project. Migrating means: scaffolding an actual Astro
project (`npm create astro@latest`), pulling in the upstream theme or rebuilding its components,
and porting content into its content collections. Rough effort: medium — most work is learning
Astro's content-collection conventions, not the visual design (already close here).
