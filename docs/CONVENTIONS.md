# Token Conventions

## Naming

### Scale / Size Identifiers

Use T-shirt sizing with extended small range:

```
none, 7xs, 6xs, 5xs, 4xs, 3xs, 2xs, xs, sm, md, ml, lg, xl, 2xl, 3xl, 4xl, 5xl, 6xl
```

`ml` (medium-large) is used only in typography (font size and line height) where a step between `md` and `lg` is needed.

### Semantic Weight Identifiers

Used for color roles (not palette steps):

```
lightest → lighter → light → medium → strong → bold → dark → darkest
```

### Typographic Variants

```
display:   1, 2
headline:  1, 2, 3, 4, 5
label:     short, long
body:      short, long, small
hyperlink: default, hover
code:      small
```

### Casing

- Token keys: `camelCase`
- Section names (top-level keys): `kebab-case` with `/` as tier separator (e.g. `brand/brandA/color`)
- All `$description` values: lowercase, no trailing spaces

---

## Values

### Colors

- Hex values: always **UPPERCASE** (e.g. `#F7FBEB`)
- Format: 6-digit hex only (no shorthand `#FFF`, no `rgba`)
- References use `{token.path}` syntax

### Dimensions

- All dimension, sizing, and spacing values include a unit (e.g. `4px`, `1440px`)
- Exception: `$type: "number"` tokens use unitless numeric values (e.g. `12`)

### Font Weights

- Stored as strings (e.g. `"700"`) — this is correct per DTCG spec
- Named weights are not used; numeric values only

### Border Radius / Shape

- Always include unit (e.g. `0px`, `4px`)
- `0` must be written as `0px`

---

## Token Types (`$type`)

Use DTCG-compliant type names:

| Category | `$type` |
|----------|---------|
| Colors | `color` |
| Spacing | `spacing` |
| Sizing | `sizing` |
| Border width | `borderWidth` |
| Border radius | `borderRadius` |
| Border (composite) | `border` |
| Typography (composite) | `typography` |
| Font family | `fontFamilies` |
| Font size | `fontSizes` |
| Font weight | `fontWeights` |
| Line height | `lineHeights` |
| Letter spacing | `letterSpacing` |
| Paragraph spacing | `paragraphSpacing` |
| Text case | `textCase` |
| Text decoration | `textDecoration` |
| Number | `number` |
| Dimension | `dimension` |

Every token must have a `$type`. No exceptions.

---

## Descriptions (`$description`)

- Always lowercase
- No trailing spaces
- No punctuation at the end
- Be specific about the token's purpose, not its value
- Use: `"background color for disabled elements"` not `"neutral.400"`

---

## Structure Rules

### No compound tokens

A token node must be either a **leaf** (has `$value`) or a **group** (has children) — never both.

```json
// ✅ correct — leaf
"brand": { "$value": "...", "$type": "color" }

// ✅ correct — group
"brand": {
  "default": { "$value": "...", "$type": "color" },
  "onBrand": { "$value": "...", "$type": "color" }
}

// ❌ wrong — compound
"brand": {
  "$value": "...",
  "$type": "color",
  "onBrand": { "$value": "...", "$type": "color" }
}
```

### Reference direction

Tokens must only reference tokens from the same tier or a lower tier. Never reference upward or sideways across tiers.

```
alias → mode ✅
alias → brand ❌ (skips a tier)
mode → alias ❌ (references upward)
```

### Composite tokens

Composite tokens (e.g. `$type: "typography"` or `$type: "border"`) must reference other tokens via `{path}`, never hardcode values inline.

---

## Extending the System

### Adding a color to the palette

Add the new color to `brand/[brandX]/color` under `brand.color.palette.[colorName]`. Include all steps (50–900). Do not reference it in `role` until there is a defined semantic purpose.

### Adding a role color

Add to `brand.color.role.*` and reference it from `mode/dark` and `mode/light`. Ensure both modes define the token — missing a mode will cause broken references.

### Adding a typescale variant

Add to `breakpoint/[bp]/typescale` first, then expose through `alias/font`. Do not reference `brand.font.*` directly from `alias/`.

### Adding a new breakpoint

Duplicate the full `breakpoint/lg/*` structure as `breakpoint/[newBp]/*`. Adjust values as needed. Update the alias tier to reference the correct breakpoint context via Figma Token Studio themes.
