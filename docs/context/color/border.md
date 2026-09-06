# Border Color — Usage Context

`alias.color.border.*` covers stroke/outline colors — for dividing or outlining surfaces, never for filling them.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.border.subtle` | low-contrast dividers (e.g. a hairline between list rows) | focus indication, or as a fill/background |
| `alias.color.border.medium` | standard component outlines (input fields, cards) | focus indication, or as a fill/background |
| `alias.color.border.heavy` | high-contrast outlines that need to stand out (e.g. an error-adjacent outline) | focus indication, or as a fill/background |
| `alias.color.border.focusOutline` | the default keyboard-focus indicator | decorative or static borders — reserve it exclusively for focus-visible states |

## Guidance

`subtle` → `medium` → `heavy` is a contrast ladder, chosen by how much the border needs to separate itself from its surroundings — not by component type. The same input field might use `medium` normally and `heavy` when flagged invalid.

`focusOutline` is semantically distinct from the other three: it exists purely to satisfy keyboard/accessibility focus visibility and should never double as a decorative border on a resting element. Prefer the composite `alias.border.focusOutline` token (see `docs/context/border.md`) over assembling focus rings manually from this color plus a hand-picked width.

## Related

- `docs/context/border.md` — border width, radius, and the full focus-outline composite token
- `docs/context/color/background.md` — the surfaces these borders outline
