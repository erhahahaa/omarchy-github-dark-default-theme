# GitHub Dark Default for Omarchy

[GitHub's dark default theme](https://github.com/primer/github-vscode-theme) for [Omarchy](https://omarchy.org) 4 (Quattro). Colors, terminal ANSI values, and syntax highlighting come from GitHub's [Primer](https://github.com/primer/primitives) design system, so the desktop matches GitHub in the browser and in the editor.

![GitHub Dark Default running in Omarchy](preview.png)

<details>
<summary>Lock screen preview</summary>

![GitHub Dark Default lock screen](preview-unlock.png)

</details>

## Install

```bash
omarchy theme install https://github.com/erhahahaa/omarchy-github-dark-default.git
```

The repo name resolves to the theme name `github-dark-default`, and Omarchy applies it after cloning. To switch back to it later:

```bash
omarchy theme set github-dark-default
```

### Manual install (keeps the exact terminal and editor configs)

```bash
git clone https://github.com/erhahahaa/omarchy-github-dark-default.git /tmp/github-dark-default
mkdir -p ~/.config/omarchy/themes/github-dark-default
cp -r /tmp/github-dark-default/. ~/.config/omarchy/themes/github-dark-default/
rm -rf ~/.config/omarchy/themes/github-dark-default/.git
omarchy theme set github-dark-default
```

Removing `.git` is intentional. Omarchy treats a theme directory containing `.git` as a URL install and refuses to stage the files listed below, so the manual copy is the only way to keep them.

> **URL install vs manual copy**
>
> Omarchy never takes `alacritty.toml`, `foot.ini`, `ghostty.conf`, `kitty.conf`, `neovim.lua`, or `vscode.json` from a git-installed theme, since each can name a program to run or an extension to install. It regenerates them from `colors.toml` instead.
>
> The generated terminals use Omarchy's palette mapping (ANSI black is the background); the files in this repo use GitHub's exact ANSI endpoints (`#484f58` … `#b1bac4`), a `#2f81f7` cursor, the real `github-nvim-theme`, and the official GitHub VS Code extension. Manually copy the theme if you want those.

## What gets themed

| App                                                                                 | Source                                   | Notes                                                                    |
| ----------------------------------------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------ |
| Omarchy shell: bar, menus, launcher, notifications, OSD, polkit prompt, lock screen | generated                                | from `colors.toml`                                                       |
| Hyprland window borders                                                             | generated                                | blue → purple active gradient, Primer `#30363d` inactive                 |
| Alacritty, Kitty, Ghostty, Foot                                                     | shipped, or generated from `colors.toml` | exact GitHub ANSI palette and cursor                                     |
| Neovim                                                                              | shipped, or generated                    | `projekt0n/github-nvim-theme` with `github_dark_default`                 |
| VS Code                                                                             | shipped, or generated                    | `GitHub.github-vscode-theme`                                             |
| Helix                                                                               | `helix.toml`                             | GitHub syntax colors: red keywords, purple functions, light-blue strings |
| Obsidian                                                                            | `obsidian.css`                           | Primer surfaces, borders, links, and code colors                         |
| btop, Chromium/GTK, gum prompts, fcitx5                                             | generated                                | `mode = "dark"`                                                          |
| Keyboard backlight                                                                  | generated                                | follows `accent`                                                         |
| Icons                                                                               | `icons.theme`                            | `Yaru-blue`                                                              |

## Palette

| Role               | Hex       |
| ------------------ | --------- |
| background         | `#0d1117` |
| dark background    | `#010409` |
| darker background  | `#000000` |
| lighter background | `#161b22` |
| foreground         | `#e6edf3` |
| dark foreground    | `#7d8590` |
| light foreground   | `#f0f6fc` |
| bright foreground  | `#ffffff` |
| accent             | `#4493f8` |
| selection          | `#1e4273` |
| muted              | `#6e7681` |

Named colors: red `#ff7b72`, green `#3fb950`, yellow `#d29922`, orange `#f0883e`, blue `#58a6ff`, magenta `#bc8cff`, cyan `#39c5cf`, brown `#9e6a03`.

The terminals use GitHub's own 16-color ANSI set:

| Normal   | Hex       | Bright    | Hex       |
| -------- | --------- | --------- | --------- |
| `color0` | `#484f58` | `color8`  | `#6e7681` |
| `color1` | `#ff7b72` | `color9`  | `#ffa198` |
| `color2` | `#3fb950` | `color10` | `#56d364` |
| `color3` | `#d29922` | `color11` | `#e3b341` |
| `color4` | `#58a6ff` | `color12` | `#79c0ff` |
| `color5` | `#bc8cff` | `color13` | `#d2a8ff` |
| `color6` | `#39c5cf` | `color14` | `#56d4dd` |
| `color7` | `#b1bac4` | `color15` | `#f0f6fc` |

## Backgrounds

Six dark Japan-night wallpapers ship with the theme:

- `japan-night-1.jpg`
- `japan-night-2.jpg`
- `japan-night-3.jpg`
- `japan-night-4.jpg`
- `japan-night-moon-dim.jpg`
- `japan-night-street-dim.jpg`

Cycle them with:

```bash
omarchy theme bg next
```

Add your own in `~/.config/omarchy/backgrounds/github-dark-default/`.

## Files

| Path                                                       | Purpose                                                                                         |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `colors.toml`                                              | Quattro palette: semantic roles, Hyprland borders, and the explicit `color0`–`color15` ANSI set |
| `alacritty.toml`, `foot.ini`, `ghostty.conf`, `kitty.conf` | Exact GitHub ANSI colors for each terminal                                                      |
| `neovim.lua`                                               | Loads `projekt0n/github-nvim-theme` and selects `github_dark_default`                           |
| `vscode.json`                                              | Installs `GitHub.github-vscode-theme`                                                           |
| `helix.toml`                                               | Helix syntax theme                                                                              |
| `obsidian.css`                                             | Obsidian theme                                                                                  |
| `icons.theme`                                              | `Yaru-blue` icon set                                                                            |
| `backgrounds/`                                             | Six wallpapers                                                                                  |
| `preview.png`                                              | Theme switcher preview                                                                          |
| `preview-unlock.png`                                       | Preview used by Style → Unlock                                                                  |
| `unlock.png`                                               | Plymouth boot logo used by Style → Unlock                                                       |
| `LICENSE`                                                  | MIT                                                                                             |

Files are intentionally not generated ahead of time when Omarchy can generate them (btop, Chromium, keyboard backlight, shell sections, and so on). A checked-in copy would freeze that file and stop future Omarchy or palette changes from reaching it.

## Compatibility

Built against Omarchy 4 (Quattro). `colors.toml` also carries the pre-Quattro keys, so the palette remains usable on Omarchy 3.

## Credits

- Palette and syntax colors: [GitHub Primer](https://github.com/primer/primitives) and [github-vscode-theme](https://github.com/primer/github-vscode-theme) (MIT).
- Neovim colors: [github-nvim-theme](https://github.com/projekt0n/github-nvim-theme) (MIT).
- Icons: `Yaru-blue`.
- GitHub and the GitHub logo are trademarks of GitHub, Inc. This is an unofficial theme.

## License

MIT. See [LICENSE](LICENSE).
