# Handoff — astro-modern variant

**Approximates:** a modern minimal Astro portfolio theme (e.g. the style of themes like
[AstroPaper](https://github.com/satnaing/astro-paper) or [Astroship](https://astroship.web3templates.com/)
stripped to single-column, large-type, single-accent layouts) — full-width, generous whitespace,
top nav instead of a sidebar.

## What this is
Static HTML/CSS mockup only — no Astro, no build step. Single accent color (`--accent`) is the
only thing distinguishing sections visually; typography and spacing do the rest of the work.

## Stubs / not real
- Top nav is real links between the 4 pages; no mobile hamburger/collapse behavior.
- Blog "Read more" links go to `#`.
- No image usage in this variant — deliberately typography-only per the design intent.
- Dummy content shared verbatim across all 4 variants — see root README.

## To preview
Open `index.html` directly, or:
```
python3 -m http.server -d variants/astro-modern 8000
```

## Migration effort if chosen
Real build: Astro + minimal CSS or Tailwind, MDX or content collections for blog posts. Rough
effort: low-medium — this is the simplest layout of the four, mostly typography and spacing
tokens to port, no complex component library.
