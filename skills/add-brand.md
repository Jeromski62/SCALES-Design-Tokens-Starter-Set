# Skill: add-brand

Add a new brand to the SCALES token system. A brand consists of three sections: color, font, and shape.

## Before you start

Ask the user for:
- Brand name (used as the section key, e.g. `brandC`)
- Primary color (hex) — the main brand color
- Secondary color (hex) — the supporting brand color
- Font family for display and content (can be the same)
- Border radius style preference: sharp (sm=2px), balanced (sm=4px), or rounded (sm=8px)

## Steps

1. **Read existing brand for reference**
   Read `tokens/tokens.json`. Use `brand/brandA/color`, `brand/brandA/font`, and `brand/brandA/shape` as the structural template.

2. **Create `brand/[brandName]/color`**
   - Duplicate the full `brand/brandA/color` structure
   - Replace palette hex values with the new brand's colors
   - The palette must include all 8 color groups: `green`, `mint`, `blue`, `violet`, `red`, `orange`, `yellow`, `neutral`
   - Each group must include all steps: `50`, `100`, `200`, `300`, `400`, `500`, `600`, `700`, `800`, `900` (neutral also needs `950`)
   - Map `brand.color.role.main.primary.*` to the primary color palette
   - Map `brand.color.role.main.secondary.*` to the secondary color palette
   - Keep intent colors (`success`, `warning`, `critical`, `info`) mapped to the appropriate semantic palette colors (green, yellow, red, blue)
   - All hex values must be UPPERCASE

3. **Create `brand/[brandName]/font`**
   - Duplicate `brand/brandA/font` structure exactly
   - Update `brand.font.family.display` and `brand.font.family.content` with the new font family
   - Keep `brand.font.family.code` as `Geist Mono` unless the user specifies otherwise
   - All other font primitive values (size, weight, lineHeight, letterSpacing) remain unchanged

4. **Create `brand/[brandName]/shape`**
   - Duplicate `brand/brandA/shape` structure
   - Adjust `brand.shape.sm`, `brand.shape.md`, `brand.shape.lg` based on the chosen radius style
   - `brand.shape.none` must always be `0px`

5. **Validate the new sections**
   - All hex colors are UPPERCASE
   - No compound tokens
   - Every token has `$type`
   - All `$description` values are lowercase
   - The full `brand.color.role.*` structure is present — mode tokens depend on it

6. **Write to `tokens/tokens.json`**
   Add the three new sections to the JSON. Do not modify any existing sections.

7. **Confirm**
   Report what was created and remind the user to add the new brand to their Figma Token Studio theme configuration so it can be activated alongside the existing breakpoint, mode, and alias sections.
