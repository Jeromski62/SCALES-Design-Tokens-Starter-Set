# Claude Instructions — SCALES

SCALES is a design token boilerplate. This repository contains an X-tier token system based on a concept by Marco-Christian Krenn. Read ARCHITECTURE.md and CONVENTIONS.md before making any changes.

## What this repo is

SCALES is a design token boilerplate built around a brand-swappable, breakpoint-aware, mode-adaptive X-tier token architecture. The system is managed in Figma via Token Studio and exported as `tokens.json`.

## The only file that matters

`tokens.json` — all tokens live here. The `$themes` and `$metadata` sections are Figma/Token Studio configuration. Do not edit them manually.

## Rules

### Never touch
- `$themes` — Figma Token Studio configuration (IDs, theme compositions)
- `$metadata` — Token Studio metadata
- The internal structure of `alias/*` without also updating the corresponding `mode/*` or `breakpoint/*` tokens it references

### Always follow
- Tier reference direction: `scaling/factors` → `brand` → `breakpoint` → `mode` → `alias`
- Token types from CONVENTIONS.md — never invent new `$type` values
- Hex colors in UPPERCASE
- `$description` values in lowercase with no trailing spaces
- No compound tokens (a node cannot have both `$value` and non-`$` children)
- Every token must have `$type`

### When adding a new brand
- Duplicate `brand/brandA/*` structure completely
- Both `brand/[x]/color`, `brand/[x]/font`, and `brand/[x]/shape` must be present
- The full `brand.color.role.*` structure is required — the mode tier depends on it
- See ARCHITECTURE.md → "Adding a New Brand"

### When editing colors
- Changes to `brand.color.palette.*` do not automatically propagate — check `brand.color.role.*` references
- Changes to `brand.color.role.*` may affect mode tokens — verify `mode/dark` and `mode/light`
- `highEmphasis` and `lowEmphasis` are intentionally swapped between light and dark mode

### When editing dimensions
- All values in `scaling/factors` affect the entire system — change with care
- `breakpoint/lg/dimension` maps factors to size/space — not all factor steps are used (intentional non-linear scale)

## Validation checklist

Before committing changes, verify:

1. No broken references — every `{token.path}` resolves to a defined token
2. No compound tokens
3. Every token has `$type`
4. All hex colors are UPPERCASE
5. No `$description` values start with a capital letter or end with a space
6. `mode/dark` and `mode/light` define the same set of tokens
7. Both `brand/brandA` and `brand/brandB` (and any additional brands) have identical internal structure

## Architecture reference

```
scaling/factors    → global dimension scale
brand/[brandX]/*   → brand-specific primitives (color, font, shape)
breakpoint/lg/*    → context tokens (dimension, typescale, border, grid, layout)
mode/dark|light    → color mappings per mode
alias/*            → PUBLIC API — only this tier is consumed by products
```

Full documentation: ARCHITECTURE.md | CONVENTIONS.md

## Skills

Executable skill files are located in `skills/`. Each skill guides an agent through a specific task:

| File | Purpose |
|------|---------|
| `skills/validate.md` | Validate `tokens/tokens.json` against all conventions |
| `skills/add-brand.md` | Add a new brand to the system |
| `skills/add-color.md` | Add a new palette color to an existing brand |
| `skills/add-breakpoint.md` | Add a new breakpoint tier |

To invoke a skill, read the corresponding file and follow its steps.
