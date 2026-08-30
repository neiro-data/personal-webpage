# Handoff — jekyll-minimal variant

**Approximates:** classic Jekyll blog themes in the [Minima](https://github.com/jekyll/minima)
family — serif body text, narrow measure, understated underline-on-hover links, document feel.

## What this is
Static HTML/CSS mockup only — no Jekyll, no Liquid templates, no `_config.yml`, no Ruby/Bundler.

## Stubs / not real
- Nav links between the 4 pages are real; no Jekyll collections/front-matter behind them.
- Blog post links go to `#` (in real Jekyll these would be generated post pages).
- No RSS/Atom feed, no pagination — out of scope for a look-and-feel mockup.
- Dummy content shared verbatim across all 4 variants — see root README.

## To preview
Open `index.html` directly, or:
```
python3 -m http.server -d variants/jekyll-minimal 8000
```

## Migration effort if chosen
Real build: Jekyll + Minima (or a fork), needs Ruby + Bundler toolchain, `_posts/` collection for
blog, `_config.yml`, GitHub Pages' native Jekyll support (no custom Action needed). Rough effort:
low for the theme itself (Minima is close to this mockup already) but adds a Ruby toolchain
dependency the other three options don't have.
