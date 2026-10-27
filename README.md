# Palette AXI Neon

<!-- readme-axi type=card -->

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://hacs.xyz/docs/faq/custom_repositories)
[![GitHub release](https://img.shields.io/github/v/release/ngoviet/palette-axi-neon)](https://github.com/ngoviet/palette-axi-neon/releases)
[![HACS validation](https://github.com/ngoviet/palette-axi-neon/actions/workflows/validate.yml/badge.svg)](https://github.com/ngoviet/palette-axi-neon/actions/workflows/validate.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**English** · [Tiếng Việt](README.vi.md)

A dark neon theme for Home Assistant: night-blue surfaces, neon accents, and text that stays readable
everywhere, including the text fields and pickers that many dark themes leave light.

> 🇻🇳 Built and maintained by one person in Việt Nam — if it saves you time, please
> [support the project](#support-the-project).

![Palette AXI Neon colour palette](https://raw.githubusercontent.com/ngoviet/palette-axi-neon/main/images/palette.png)

## Features

- **Night blue, not black.** The page background is a deep blue (OKLCH L 0.18), cards sit one step lighter, and a
  soft glow lifts the top-left corner. Borders and greys share the background hue, so nothing looks dead grey.
- **Accents on one lightness band.** Every accent (L 0.70–0.84) has about the same visual weight, so none
  shouts louder than the others. One meaning per colour: green = good, amber = attention, red = error,
  blue = info, cyan = primary.
- **Measured contrast.** Primary text is 14.99:1 on cards and secondary text 8.66:1 (WCAG AAA). Every status
  colour is at least 6.5:1.
- **Readable text fields.** The theme declares dark mode explicitly, so search boxes, pickers and form fields
  use dark fills (see [Why the `modes` block matters](#why-the-modes-block-matters)).
- **Mushroom-friendly.** HA's named colours (`red-color`, `amber-color`, `teal-color`, …) are remapped to the
  same palette, so Mushroom chips and `icon_color` match the theme.

## Installation

### HACS (recommended)

1. Open **HACS** in Home Assistant.
2. Open the menu (⋮, top right) → **Custom repositories**.
3. Add `https://github.com/ngoviet/palette-axi-neon` and choose the **Theme** type.
4. Search for **Palette AXI Neon**, open it and select **Download**.
5. Reload themes: **Developer tools → Actions → `frontend.reload_themes`**, or restart Home Assistant.

### Manual

1. Make sure `configuration.yaml` loads themes from a folder:

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
   ```

2. Copy [`themes/palette_axi_neon.yaml`](themes/palette_axi_neon.yaml) into `/config/themes/`.
3. Call the `frontend.reload_themes` action (or restart Home Assistant).

## Usage

- **Whole interface (per user):** open your **Profile** → **Theme** and pick `palette-axi-neon`.
- **A single dashboard or view:** set `theme: palette-axi-neon` on the view in the raw configuration editor.
- **As the default for everyone:** call `frontend.set_theme` with `name: palette-axi-neon`.

## Why the `modes` block matters

The theme ends with a `modes: dark:` block. Do not remove it.

When a theme has no `modes` key, the Home Assistant frontend forces **light mode** for it. Text fields, the
theme picker and other form controls then use the light default fill (`#f5f5f5`), while their text inherits the
theme's light `primary-text-color`. The result is light text on a light field, almost invisible.

A theme that declares `dark` without `light` makes the frontend force **dark mode** instead. Every value the theme
does not set falls back to Home Assistant's dark defaults, and the block also tunes the input colours to the
palette:

```yaml
  modes:
    dark:
      input-fill-color: "#142443"
      input-ink-color: "#e6edf7"
      input-label-ink-color: "#a2b7d7"
      # …
```

The same trick fixes any custom dark theme with unreadable text fields.

## Palette

| Role | Variable | Colour | Contrast on card |
|------|----------|--------|------------------|
| Page background | `primary-background-color` | `#0a1122` | — |
| Card | `card-background-color` | `#0e182e` | — |
| Sidebar / header | `sidebar-background-color` | `#060a14` | — |
| Text field | `input-fill-color` | `#142443` | text 13.07:1 |
| Border / divider | `divider-color` | `#1e2b4a` | — |
| Primary text | `primary-text-color` | `#e6edf7` | 14.99:1 |
| Secondary text | `secondary-text-color` | `#a2b7d7` | 8.66:1 |
| Disabled text | `disabled-text-color` | `#6b7fa3` | 4.37:1 |
| Primary / accent | `primary-color` | `#22d3ee` | 9.77:1 |
| Success | `success-color` | `#22c55e` | 7.75:1 |
| Warning | `warning-color` / `amber-color` | `#f59e0b` / `#fbbf24` | — / 10.58:1 |
| Error | `error-color` | `#ff716a` | 6.58:1 |
| Info | `info-color` | `#6ca4ff` | 7.06:1 |
| Purple | `purple-color` | `#a78bfa` | 6.49:1 |
| Orange | `orange-color` | `#fb923c` | 7.81:1 |
| Pink | `pink-color` | `#f472b6` | 6.67:1 |

Text on the cyan primary button (`text-primary-color` `#0a1122`) reaches 10.41:1. Contrast figures are WCAG 2
ratios measured with [palette-axi](#credits).

### Extra variables for your own cards

The theme also defines `--nv-*` variables (`nv-cyan`, `nv-blue`, `nv-green`, `nv-amber`, `nv-red`, `nv-purple`,
`nv-orange`, `nv-pink`, `nv-metric`, `nv-surface`) for custom cards and `card-mod` styles. Always give a
fallback so the card still works on other themes:

```css
color: var(--nv-blue, #448aff);
```

## Compatibility

- Tested on Home Assistant **2026.10**.
- Dark only: there is no light variant, and the theme stays dark even when your profile is set to light or auto.

## Credits

Palette generated and checked with **palette-axi** (OKLCH, `generate --preset neon-dark`), a small CLI that
audits UI colours: tinted neutrals, accents on one lightness band, APCA and WCAG contrast, sRGB gamut.

<!-- support:start -->
## Support the project

<p align="center">
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/banner.svg" width="720" alt="Built and maintained by one person in Việt Nam">
</p>

<p align="center">
  <a href="https://buymeacoffee.com/ngoviet"><img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/btn-coffee.svg" height="56" alt="Buy me a coffee"></a>
  &nbsp;
  <a href="https://github.com/sponsors/ngoviet"><img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/btn-sponsors.svg" height="56" alt="GitHub Sponsors"></a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/vietqr-card.svg" width="300" alt="VietQR — MB Bank — NGO DUC VIET — 911051212">
  &nbsp;
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/crypto-card.svg" width="300" alt="Crypto — BNB Smart Chain (BEP20) — 0xcbf0402b232cb24b4d998f09a4884f87b5f74750">
</p>

<p align="center"><b>Crypto wallet, BNB Smart Chain (BEP20) only:</b><br><code>0xcbf0402b232cb24b4d998f09a4884f87b5f74750</code></p>

<p align="center"><sub>🇻🇳 VietQR: scan with any Vietnamese banking app, transfer note <code>Ung ho palette-axi-neon</code>. Thank you for keeping this project alive!</sub></p>
<!-- support:end -->

## License

[MIT](LICENSE) © Ngô Đức Việt.
