---
name: add-breakpoint
description: Add a new breakpoint tier (dimension, typescale, border, grid, layout) to the SCALES token system
disable-model-invocation: true
allowed-tools: Read, Edit
---

# Skill: add-breakpoint

Add a new breakpoint tier to the SCALES token system. Breakpoints define context-specific dimension, typescale, border, grid, and layout tokens.

## Before you start

Ask the user for:
- Breakpoint name (e.g. `sm`, `md`, `xl`)
- Max screen width for this breakpoint (e.g. `768px`)
- Grid columns (e.g. `4` for mobile, `8` for tablet)
- Whether to start from `breakpoint/lg` as a base and adjust, or define values from scratch

## Steps

1. **Read existing breakpoint for reference**
   Read `tokens/tokens.json`. Use the full `breakpoint/lg/*` structure as the template. It consists of 5 sections:
   - `breakpoint/lg/border`
   - `breakpoint/lg/dimension`
   - `breakpoint/lg/grid`
   - `breakpoint/lg/layout`
   - `breakpoint/lg/typescale`

2. **Create `breakpoint/[bp]/dimension`**
   Map `scaling/factors` steps to `size` and `space` tokens. The mapping does not need to be identical to `lg` — choose steps that make sense for the breakpoint's density.
   - Smaller breakpoints typically use smaller factor steps
   - All tokens must reference `{scale.[step]}` — never hardcode values

3. **Create `breakpoint/[bp]/border`**
   - `borderWidth.*` references `{scale.[step]}`
   - `radius.*` references `{brand.shape.[step]}`
   - Keep the same semantic keys: `xs`, `sm`, `md` for borderWidth; `none`, `sm`, `md`, `lg` for radius

4. **Create `breakpoint/[bp]/typescale`**
   Map brand font primitives to typographic roles. References must point to `{brand.font.[property].[step]}`.
   - Smaller breakpoints typically use smaller font size steps
   - All categories must be present: `display`, `headline`, `label`, `body`, `hyperlink`, `code`
   - All properties must be present: `fontSize`, `fontWeight`, `lineHeight`, `letterSpacing`, `fontFamily`, `textDecoration`

5. **Create `breakpoint/[bp]/grid`**
   ```
   grid.cols            → number of columns (must be numeric JSON value, not string)
   grid.marginLeftRight → references {size.[step]}
   grid.gutter          → references {space.[step]}
   ```

6. **Create `breakpoint/[bp]/layout`**
   ```
   screen.maxWidth               → value with px unit (e.g. "768px"), $type: "sizing"
   screen.layout.paddingLeftRight → references {space.[step]}
   ```

7. **Validate**
   - No hardcoded values — all tokens reference either `{scale.*}` or `{brand.*}`
   - Every token has `$type`
   - `grid.cols` is a numeric value, not a string
   - `screen.maxWidth` includes `px` unit
   - All 5 sections are present

8. **Write to `tokens/tokens.json`**
   Add all 5 new sections. Do not modify any existing sections.

9. **Confirm and remind**
   Report all created sections and remind the user to:
   - Add the new breakpoint sections to their Figma Token Studio theme configuration
   - Update the `alias/*` sections if they should now reference the new breakpoint instead of or alongside `lg`
   - Consider whether the alias tier needs a breakpoint-switching strategy (e.g. CSS custom property overrides per breakpoint)
