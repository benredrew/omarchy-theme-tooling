# Omarchy theme package workflow

Use this workflow when a user asks an agent to make, publish, update, or list a
custom Omarchy theme. It is deliberately separate from a theme repository:
theme repos hold only installable theme assets and visible previews; shared
agent tooling lives under `~/.local/bin` and `~/.agents`.

## Build and review

1. Keep the working theme under `~/.config/omarchy/themes/<slug>/` and its
   wallpaper levels under `~/.config/omarchy/backgrounds/<slug>/`.
2. Order same-framing filter levels with sortable filenames, for example
   `A-crisp.png` through `D-strong.png`.
3. Use `agent-theme-preview` to make the deterministic wallpaper and palette
   boards, plus the root `preview.png` picker tile. Make it with:

   ```bash
   agent-theme-preview picker --title "THEME NAME" --subtitle "Artist · dark" \
     colors.toml backgrounds/A-crisp.png preview.png
   ```

   Use `--top-offset` or a caller-chosen `--closeup` crop where the composition
   needs it. Submit review boards through `agent-gallery`, with a tile only for
   a palette-only set.
4. Never apply a new palette before the user has reviewed it, unless they
   explicitly ask to apply it.

## Wallpaper treatment levels

Use `agent-theme-levels --colors colors.toml <source-image> <output-directory>`
to create a non-destructive spectrum of same-framing wallpaper copies: A–D by
default, or any count with `--levels N` (evenly spaced along the same scale;
the default 4 are its reference points, listed below). It never changes the
source and refuses to reuse a non-empty output directory.
Never use AI re-generation for a filtered version of a licensed photograph;
the levels must come from this repeatable raster pipeline.

Choose the treatment with `--method`. Methods are separate looks, not
strengths; each maps the same A–D strength scale, and more may be added:

| Method | Look |
| --- | --- |
| `low-res-speckle` (default) | Hard-edged pixels that each keep the local average color, fewer colors with half-strength dithering, light monochrome grain and slightly lifted blacks. Its strongest level uses only the theme's own colors (pass `--colors`). |
| `low-res-painting` | Edge-preserving flattening into painted shapes at lower resolution, a few flat undithered colors, lifted pastel light with a warm `selection`-color wash, soft glow and gentle grain: a lo-fi-beats illustration look. |

| File | Intent |
| --- | --- |
| `A-crisp.png` | Faithful clean baseline. |
| `B-light.png` | First reference strength of the method. |
| `C-medium.png` | Clearly stylized while preserving the focal silhouette. |
| `D-strong.png` | The method's maximum that remains legible. |

Every method preserves crop, orientation, and resolution. When the user asks
for a look by name ("lo-fi", "vintage"), show the methods' boards side by side
rather than assuming one: what reads as that look is the user's call.

After rendering, use `agent-theme-preview wallpaper` on the levels and submit
the resulting board to Agent Gallery as a floating review set. Every level of
the gradient ships in the theme's `backgrounds/` as a wallpaper option; that is
the point of the spectrum. The level the user picks by its letter is the
default wallpaper, the one the theme opens on.

## Package

Create a public repository named `omarchy-<name>-theme`. It contains only:

- `colors.toml`, `icons.theme`, root `preview.png`, and optional lock assets;
- `backgrounds/` with the ordered wallpaper levels;
- `previews/filter-intensity.png` and `previews/palette.png`, embedded in the
  README so GitHub visitors can see the options;
- `README.md` in the standard format of `docs/theme-readme.md` (installed as
  `~/.agents/OMARCHY-THEME-README.md`): fixed sections Install, Backgrounds,
  Previews, Photo, License, with photographer credit and rights basis;
- `LICENSE` holding the license the author chose. Ask; never choose it for them.

Do not put scripts, renderer copies, package-manager files, or agent workflow
documents in the theme repository.

Before committing, run:

```bash
agent-theme-package validate --title "THEME NAME" /path/to/omarchy-name-theme
```

It rejects tooling directories, checks the README format and that a `LICENSE`
exists, rejects `colors.toml` keys Omarchy never reads (judged against the
installed Omarchy's templates), and verifies that both committed preview PNGs regenerate pixel-for-pixel
from `colors.toml` and the ordered background files.

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
