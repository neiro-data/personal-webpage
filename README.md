# personal-webpage

Repo for a personal site. **Design decision is still open** — currently comparing four static
mockups before committing to a real framework build.

## Comparing the design variants

Four low-fidelity, static HTML/CSS mockups live in `/variants/`, one per candidate design
direction, all rendering the same placeholder content (name/role, About, 3 fake projects, 2 fake
blog posts, stub CV). No build step, no Node/Ruby/Go toolchain — just HTML and CSS.

Open the comparison hub:

```
open variants/index.html
```

or serve the whole repo and browse:

```
python3 -m http.server
# then visit http://localhost:8000/variants/
```

| Variant | Look | Approximates |
| --- | --- | --- |
| [`astrofy`](variants/astrofy/index.html) | Card/sidebar, avatar, rounded cards, light & airy | [Astrofy](https://github.com/manuelernestog/astrofy) (Astro) |
| [`astro-modern`](variants/astro-modern/index.html) | Full-width minimal, large type, single accent | Minimal Astro portfolio themes |
| [`jekyll-minimal`](variants/jekyll-minimal/index.html) | Classic blog/document feel, serif, understated | [Minima](https://github.com/jekyll/minima) (Jekyll) |
| [`hugo-terminal`](variants/hugo-terminal/index.html) | Dark, monospace, terminal-prompt accents | [hugo-theme-terminal](https://github.com/panr/hugo-theme-terminal) (Hugo) |

Each variant folder has a `HANDOFF.md` covering what's stubbed, how to preview it standalone, and
the estimated migration effort if it's the one picked.

## Status

- **This phase:** static mockups only, for a look-and-feel decision. No GitHub Pages, no Actions,
  no deploy config yet.
- **Next phase (after a variant is picked):** scaffold the real framework (Astro/Jekyll/Hugo),
  port the placeholder content to real content, wire up GitHub Pages.

See `plan-personal-webpage.md` for the full plan and `plan-first-commit.md` for the original
brainstorm.
