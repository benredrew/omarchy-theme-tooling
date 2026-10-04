# Omarchy theme package workflow

Use this workflow when a user asks an agent to make, publish, update, or list a
custom Omarchy theme. It is deliberately separate from a theme repository:
theme repos hold only installable theme assets and visible previews; shared
agent tooling lives under `~/.local/bin` and `~/.agents`.

## Build and review

1. Keep the working theme under `~/.config/omarchy/themes/<slug>/` and its
   wallpaper levels under `~/.config/omarchy/backgrounds/<slug>/`.
2. Order same-framing filter levels with sortable filenames, for example
   `A-crisp.png` through `D-ultra-lofi.png`.
3. Use `agent-theme-preview` to make the deterministic wallpaper and palette
   boards. Submit them through `agent-gallery`, with a tile only for a
   palette-only set.
4. Never apply a new palette before the user has reviewed it, unless they
   explicitly ask to apply it.

## Lo-fi wallpaper spectrum

Use `agent-theme-lofi --colors colors.toml <source-image> <output-directory>`
to create a non-destructive spectrum of same-framing wallpaper copies: A–D by
default, or any count with `--levels N` (evenly spaced along the same scale;
the default 4 are its reference points, listed below). It never changes the
source and refuses to reuse a non-empty output directory.
Never use AI re-generation for a filtered version of a licensed photograph;
the levels must come from this repeatable raster pipeline.

| File | Intent |
| --- | --- |
| `A-crisp.png` | Faithful clean baseline. |
| `B-lofi.png` | Gentle softening, lower saturation/local contrast, and restrained tonal compression. |
| `C-heavy-lofi.png` | Clearly stylized, muted, and softer while preserving the focal silhouette. |
| `D-ultra-lofi.png` | Dreamy maximum treatment that remains legible rather than becoming a color wash. |

The command increases the same controls monotonically across the spectrum:
micro-detail reduction, highlight/shadow compression, muted theme-led color,
and a restrained accent tint. It preserves crop, orientation, and resolution.
After rendering, use `agent-theme-preview wallpaper` on the levels and submit
the resulting board to Agent Gallery as a floating review set. Apply or package
only the level the user selects by its letter.

## Package

Create a public repository named `omarchy-<name>-theme`. It contains only:

- `colors.toml`, `icons.theme`, root `preview.png`, and optional lock assets;
- `backgrounds/` with the ordered wallpaper levels;
- `previews/filter-intensity.png` and `previews/palette.png`, embedded in the
  README so GitHub visitors can see the options;
- a concise README and, whenever required, clear photographer attribution.

Do not put scripts, renderer copies, package-manager files, or agent workflow
documents in the theme repository.

Before committing, run:

```bash
agent-theme-package validate --title "THEME NAME" /path/to/omarchy-name-theme
```

It rejects tooling directories and verifies that both committed preview PNGs
regenerate byte-for-byte from `colors.toml` and the ordered background files.

## Publication

1. Check every wallpaper's license or permission. Attribution alone is not
   permission to redistribute a photo or its derivative.
2. Create/push the public GitHub repo only with user authorization. Set useful
   discovery topics (`omarchy-theme` plus visual descriptors).
3. Submit to the official registry only when its permission attestation is
   true. Never bypass or falsely complete it.
4. Do not post announcements unless the user asks.

Use explicit `git add <paths>` commands, preserve the human's configured Git
author identity, and credit agents with a co-author trailer where appropriate.
