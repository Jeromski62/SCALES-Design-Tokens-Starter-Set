---
name: add-color
description: Add a new palette color to an existing brand in the SCALES token system
disable-model-invocation: true
allowed-tools: Read, Edit
---

# Skill: add-color

Add a new color to the palette of an existing brand.

## Before you start

Ask the user for:
- Brand name (e.g. `brandA`)
- Color name (e.g. `teal`, `pink`, `lime`)
- Hex values for all required steps, or a single base color to generate a scale from

## Steps

1. **Read existing brand palette**
   Read `tokens/tokens.json`. Look at `brand/[brandName]/color.brand.color.palette` to understand the existing structure.

2. **Validate input**
   - Color name must be a single lowercase word, no spaces or special characters
   - All hex values must be valid 6-digit hex codes
   - Steps required: `50`, `100`, `200`, `300`, `400`, `500`, `600`, `700`, `800`, `900`
   - If the user provides only a base color, ask them to confirm the full scale before proceeding — do not generate values automatically

3. **Add to palette**
   Add the new color group under `brand/[brandName]/color → brand.color.palette.[colorName]`:
   ```
   50  → lightest tint
   100
   200
   300
   400
   500 → base / mid-point
   600
   700
   800
   900 → darkest shade
   ```
   All hex values must be UPPERCASE. Each step must have `$type: "color"`.

4. **Check if role mapping is needed**
   Ask the user: should this color be used for a semantic role (e.g. as a new intent color)?
   - If yes: add the appropriate mapping to `brand.color.role.*` and update `mode/dark` and `mode/light` accordingly
   - If no: the color lives in the palette only and is not yet referenced anywhere — that is fine

5. **Validate**
   Run a quick check:
   - All new hex values are UPPERCASE
   - All steps are present (50–900)
   - Every token has `$type: "color"`
   - No existing tokens were modified

6. **Write to `tokens/tokens.json`**
   Add only the new color group. Do not modify any other part of the file.

7. **Confirm**
   Report the new token paths created (e.g. `brand.color.palette.teal.50` through `brand.color.palette.teal.900`).
