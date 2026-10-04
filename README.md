# Omarchy Theme Tooling

Shared, deterministic tooling for creating and publishing clean Omarchy theme
packages. This repository intentionally contains the workflow layer only—no
theme assets or wallpapers.

## Included commands

- `agent-theme-preview` renders a role-based palette card and a diagonal
  wallpaper filter-intensity board from a `colors.toml` plus ordered,
  same-framing images. Identical inputs produce byte-identical PNGs.
- `agent-theme-package validate` verifies that a theme repository contains only
  package assets and that its committed preview boards reproduce exactly.

## Install on an agent workstation

```bash
install -Dm755 bin/agent-theme-preview ~/.local/bin/agent-theme-preview
install -Dm755 bin/agent-theme-package ~/.local/bin/agent-theme-package
install -Dm644 docs/agent-theme-publishing.md ~/.agents/OMARCHY-THEME-PUBLISHING.md
```

The publishing guide documents the image-rights check, GitHub publication,
registry attestation, and the separation between a reusable tool repository and
a theme-only repository.

## Typical flow

```bash
# Generate standard review artifacts.
agent-theme-preview wallpaper --gap 26 colors.toml previews/filter-intensity.png \
  backgrounds/A-crisp.png backgrounds/B-lofi.png \
  backgrounds/C-heavy-lofi.png backgrounds/D-ultra-lofi.png
agent-theme-preview palette --title "THEME NAME" colors.toml previews/palette.png

# Confirm the theme package is clean and reproducible before publishing.
agent-theme-package validate --title "THEME NAME" /path/to/omarchy-theme-name-theme
```

Use the shared Agent Gallery to submit review boards. Palette-only sets tile;
wallpaper and mixed sets float.
