# Handoff — hugo-terminal variant

**Approximates:** [Hugo](https://gohugo.io/) terminal/portfolio themes such as
[hugo-theme-terminal](https://github.com/panr/hugo-theme-terminal) — dark background, monospace
type, terminal-prompt accents (`$`, `>`), high contrast, panel-style content blocks.

## What this is
Static HTML/CSS mockup only — no Hugo, no build step, no `hugo.toml`, no Go binary.

## Stubs / not real
- Nav items are styled like terminal commands (`./cv`, `./projects`) but are plain real links
  between the 4 pages.
- Blog "read more >>" links go to `#`.
- No actual terminal interactivity (no typing animation, no keyboard nav) — visual reference only.
- Dummy content shared verbatim across all 4 variants — see root README.

## To preview
Open `index.html` directly, or:
```
python3 -m http.server -d variants/hugo-terminal 8000
```

## Migration effort if chosen
Real build: Hugo (single static binary, no package manager needed) + the terminal theme as a git
submodule or copied into `themes/`, content as Markdown in `content/`. Rough effort: low — Hugo's
toolchain is the lightest of the four (no Node/Ruby/npm), and the upstream theme already looks
close to this mockup.
