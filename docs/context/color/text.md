# Text Color — Usage Context

`alias.color.text.*` covers general-purpose typographic color — the default reading colors used across body copy, labels, and headings that aren't otherwise covered by a more specific `onX` token (see Related).

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.text.default` | the default color for body copy and most typography on a light/default surface | backgrounds or borders |
| `alias.color.text.inverted` | text placed on a dark or inverted surface (e.g. a dark-mode-style panel embedded in a light UI) | text on the default light background |
| `alias.color.text.subtle` | de-emphasized, secondary copy (captions, helper text, metadata) | primary body text, or anything that needs to be the reading focus |

## Guidance

This group is for **general** text, not text sitting on a colored/branded/state surface — if your text sits on top of `primary.brand`, `intent.successHighEmphasis`, `background.highEmphasis`, or a `state.*` overlay, use that group's matching `onX` token instead (e.g. `alias.color.primary.onBrand`), because those are contrast-checked specifically against their paired background. Reach for `alias.color.text.*` only on the neutral `background.*` surfaces.

`subtle` is a hierarchy tool, not a low-contrast-for-its-own-sake choice — use it deliberately to push secondary information behind primary content, not as a substitute for `default` when you just want a "slightly different gray."

## Related

- `docs/context/color/background.md` — the neutral surfaces this text color is designed for
- `docs/context/color/interaction.md`, `docs/context/color/intent.md`, `docs/context/color/state.md` — each has its own `onX` text color for its own background
