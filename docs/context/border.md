# Border Width & Radius — Usage Context

`alias.borderWidth.*`, `alias.radius.*`, and the `alias.border.focusOutline` composite cover stroke thickness and corner rounding — structural border properties, as distinct from border *color* (see `docs/context/color/border.md`).

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.borderWidth.xs` | the thinnest border stroke (hairline dividers) | spacing or sizing values |
| `alias.borderWidth.sm` | a small, standard border stroke | spacing or sizing values |
| `alias.borderWidth.md` | a medium border stroke, used by the default `alias.border.focusOutline` | spacing or sizing values |
| `alias.radius.none` | square corners | spacing or sizing values |
| `alias.radius.sm` | subtly rounded corners (inputs, small controls) | spacing or sizing values |
| `alias.radius.md` | standard rounded corners (cards, buttons) | spacing or sizing values |
| `alias.radius.lg` | prominently rounded corners (modals, large surfaces, pill-like shapes) | spacing or sizing values |
| `alias.border.focusOutline` | the composite (color + width + style) default focus ring | decorative or static borders — reserved for focus-visible states |

## Guidance

Border width and radius are visually similar to spacing values (both are small `px` numbers) but semantically unrelated — never borrow a border token to create a gap, or a spacing token to size a border. Keeping them separate means a brand can change its "roundedness" or "border weight" globally without touching layout spacing at all (see `brand/[brandX]/shape` in `docs/ARCHITECTURE.md`).

Use `alias.border.focusOutline` as a complete unit rather than reassembling its parts — it already composes the correct color (`alias.color.border.focusOutline`), width, and style so that focus indication stays consistent across the whole product.

## Related

- `docs/context/color/border.md` — the color half of border styling
- `docs/context/dimension.md` — for actual spacing/sizing values
