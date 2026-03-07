# Token Architecture

This system follows a multi-tier architecture. Only the `alias/` tier is released and consumed by products. All other tiers exist to keep the system scalable, maintainable, and brand-swappable.

## Tier Overview

```
scaling/factors        → global dimension scale (brand-independent primitives)
brand/[brandX]/*       → brand-specific primitives (color palette, font, shape)
breakpoint/[bp]/*      → context-specific tokens (dimension, typescale, border, grid, layout)
mode/dark | mode/light → light/dark mode color mappings
alias/*                → PUBLIC API — the only released tier
```

Each tier references only the tier(s) below it. Never skip tiers or reference upward.

---

## Tier 1 — scaling/factors

Global, brand-independent dimension scale. All size and spacing values in the system originate here.

**Token path:** `scale.[step]`

**Steps:**
| Token | Value |
|-------|-------|
| `scale.none` | 0px |
| `scale.7xs` | 1px |
| `scale.6xs` | 2px |
| `scale.5xs` | 4px |
| `scale.4xs` | 8px |
| `scale.3xs` | 12px |
| `scale.2xs` | 16px |
| `scale.xs` | 20px |
| `scale.sm` | 24px |
| `scale.md` | 32px |
| `scale.lg` | 44px |
| `scale.xl` | 48px |
| `scale.2xl` | 52px |
| `scale.3xl` | 60px |
| `scale.4xl` | 64px |
| `scale.5xl` | 72px |
| `scale.6xl` | 80px |

---

## Tier 2 — brand/[brandX]

Brand-specific primitives. Fully swappable per brand. All brands must implement the same internal structure.

Each brand consists of three sections:

### brand/[brandX]/color

**Palette** — raw hex color values.

```
brand.color.palette.[colorName].[step]
```

Color names: `green`, `mint`, `blue`, `violet`, `red`, `orange`, `yellow`, `neutral`
Steps: `50`, `100`, `200`, `300`, `400`, `500`, `600`, `700`, `800`, `900` (neutral also has `950`)

**Role** — semantic color roles mapped from palette. This is brand-specific because different brands may assign different palette colors to the same role.

```
brand.color.role.main.[primary|secondary].[weight]
brand.color.role.intent.[success|warning|critical|info].[weight]
brand.color.role.neutral.[weight]
```

Role weights for `main` and `intent`: `lightest`, `light`, `medium`, `strong`, `bold`, `dark`
Role weights for `neutral`: `lightest`, `lighter`, `light`, `medium`, `strong`, `bold`, `dark`, `darkest`

### brand/[brandX]/font

Brand-specific font primitives.

```
brand.font.family.[display|content|code]
brand.font.weight.[black|bold|semiBold|default]
brand.font.size.[3xs|2xs|xs|sm|md|ml|lg|xl|2xl|3xl]
brand.font.lineHeight.[3xs|2xs|xs|sm|md|ml|lg|xl|2xl|3xl]
brand.font.letterSpacing.[xs|sm|md|lg]
brand.font.paragraphSpacing.[sm]
brand.font.textCase.[upper]
brand.font.textDecoration.[none|underline]
```

### brand/[brandX]/shape

Brand-specific border radius values.

```
brand.shape.[none|sm|md|lg]
```

---

## Tier 3 — breakpoint/[breakpoint]

Context-specific tokens scoped to a breakpoint. Currently only `lg` is implemented. Additional breakpoints (e.g. `sm`, `md`) follow the same structure.

### breakpoint/[bp]/dimension

Maps `scaling/factors` steps to semantic size and space tokens.

```
size.[none|3xs|2xs|xs|sm|md|lg|xl|2xl|3xl]   → $type: sizing
space.[none|3xs|2xs|xs|sm|md|lg|xl|2xl|3xl]  → $type: spacing
```

### breakpoint/[bp]/border

```
borderWidth.[xs|sm|md]    → $type: borderWidth
radius.[none|sm|md|lg]    → $type: borderRadius
```

### breakpoint/[bp]/typescale

Maps brand font primitives to semantic typographic roles. References `brand.font.*` tokens.

```
typescale.fontSize.[category].[variant]
typescale.fontWeight.[category].[variant]
typescale.lineHeight.[category].[variant]
typescale.letterSpacing.[category].[variant]
typescale.fontFamily.[category].[variant]
typescale.textDecoration.[category].[variant]
```

Categories: `display` (1–2), `headline` (1–5), `label` (short/long), `body` (short/long/small), `hyperlink` (default/hover), `code` (small)

### breakpoint/[bp]/grid

```
grid.cols          → $type: number
grid.marginLeftRight → $type: sizing
grid.gutter        → $type: spacing
```

### breakpoint/[bp]/layout

```
screen.maxWidth               → $type: sizing
screen.layout.paddingLeftRight → $type: spacing
```

---

## Tier 4 — mode/dark & mode/light

Maps brand color roles to semantic mode-specific tokens. References `brand.color.role.*`.

Both modes expose the same token structure:

```
mode.primary.[interaction|onInteraction|brand|onBrand]
mode.secondary.[interaction|onInteraction|brand|onBrand]
mode.intent.[infoHighEmphasis|infoLowEmphasis|onInfo|successHighEmphasis|...]
mode.background.[body|highEmphasis|mediumEmphasis|lowEmphasis]
mode.text.[default|inverted|subtle]
mode.state.[disable|onDisable|hover|press|select|onSelect|selectInverted|onSelectInverted]
mode.border.[subtle|medium|heavy|focusOutline]
```

**Important:** `highEmphasis` and `lowEmphasis` values are intentionally swapped between light and dark mode to ensure correct contrast on each background.

---

## Tier 5 — alias/* (PUBLIC API)

The only tier released to consuming products. Passes through mode and breakpoint tokens without transformation.

```
alias.color.*       → references mode.*
alias.size.*        → references size.* (breakpoint)
alias.space.*       → references space.* (breakpoint)
alias.font.*        → references typescale.* (breakpoint) — composite typography tokens
alias.borderWidth.* → references borderWidth.* (breakpoint)
alias.radius.*      → references radius.* (breakpoint)
alias.border.*      → composite border tokens
alias.grid.*        → references grid.* (breakpoint)
alias.screen.*      → references screen.* (breakpoint)
```

---

## Reference Chain Summary

```
Color:      palette → role → mode → alias.color
Dimension:  scale → size/space (breakpoint) → alias.size / alias.space
Typography: brand.font → typescale (breakpoint) → alias.font
Border:     scale + brand.shape → borderWidth/radius (breakpoint) → alias.border
```

---

## Adding a New Brand

1. Duplicate `brand/brandA/*` as `brand/[newBrand]/*`
2. Replace palette hex values
3. Remap `brand.color.role.*` to the new palette
4. Update font family values in `brand.font.family.*`
5. Adjust shape values in `brand.shape.*`
6. In Figma Token Studio: create a new theme that activates the new brand sections alongside the existing breakpoint, mode, and alias sections

**Contract:** All brands must expose the full `brand.color.role.*` structure. The mode tier depends on it.
