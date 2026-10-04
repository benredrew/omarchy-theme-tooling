# Theme README format

Every theme repository's `README.md` follows this format, so all of them read
alike on GitHub and on themes.omarchy.org. `agent-theme-package validate`
checks the required parts. Copy the template below and replace each `<...>`.

## Rules

- **Sections, in this order, with these exact headings:** the `#` title, then
  `## Install`, `## Backgrounds`, `## Previews`, `## Photo`, `## License`. No
  other `##` sections; put anything else in one of these.
- **Title** is the display name (`Tiny Is Huge`), matching the registry entry.
- **Summary** is one paragraph straight under the title: light or dark, what
  the inspiration is, and which roles the main colors play. No marketing.
- **Hero image** follows the summary: `preview.png`, the same image Omarchy's
  theme switcher shows.
- **Install** gives the repository URL form, which always works, then
  `omarchy theme set <slug>`. Once the theme is listed in the registry, add
  the shorter `omarchy theme install <slug>` above the URL form.
- **Backgrounds** names every level in order with its letter, says which
  `agent-theme-levels` method produced them, names the intended level, and says
  Omarchy starts on the first one and `omarchy theme bg next` cycles.
- **Previews** is the two-column table of `previews/filter-intensity.png`
  (width 520) and `previews/palette.png` (width 320).
- **Photo** credits the photographer and the source, says what was changed,
  and states the rights basis: the author's own photo, or the license or
  written permission it is used under. A third-party photo without
  permission is not published at all (see `agent-theme-publishing.md`).
- **License** names the license that `LICENSE` contains and what it covers.
  Choosing a license is the author's decision; never pick one for them.

## Template

````markdown
# <Theme Name>

<One paragraph: light or dark theme; the inspiration; the roles of the main
colors (surfaces, text, focus, information).>

![<Theme Name> wallpaper, <intended level name>](preview.png)

## Install

```bash
omarchy theme install https://github.com/<owner>/omarchy-<slug>-theme.git
```

Then choose **<Theme Name>** from Omarchy's theme picker, or run:

```bash
omarchy theme set <slug>
```

## Backgrounds

<N> ordered treatments of the same photo, made with `agent-theme-levels
--method <method>`: **A Crisp**, **B Light**, ... <one sentence on what the
method does>. <Letter> is the intended look. Omarchy starts on A; switch with
`omarchy theme bg next`.

## Previews

| Wallpaper treatment levels | Palette |
| --- | --- |
| <img src="previews/filter-intensity.png" alt="Crisp through strongest wallpaper levels in diagonal, bordered regions" width="520"> | <img src="previews/palette.png" alt="<Theme Name> role-based color palette" width="320"> |

## Photo

<Photo title or description> by <photographer, linked>. <Source and what was
changed: crop, palette, treatment.> <Rights basis.>

## License

<License name, linked>. <What it covers, e.g. "the theme files and
wallpapers".>
````
