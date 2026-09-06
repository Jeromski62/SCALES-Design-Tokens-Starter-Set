# Background Color — Usage Context

`alias.color.background.*` provides neutral surface colors with no semantic meaning attached — they establish visual layering (page vs. card vs. modal) via emphasis, not via brand or intent.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.background.body` | the page/app background, the lowest layer everything else sits on | component surfaces, or as a text color |
| `alias.color.background.highEmphasis` | surfaces that need to stand out most from the body (e.g. a modal, a popover) | medium/low emphasis surfaces |
| `alias.color.background.mediumEmphasis` | standard component surfaces (cards, panels) | high or low emphasis surfaces |
| `alias.color.background.lowEmphasis` | surfaces that should recede (a disabled section, a nested sub-panel) | high or medium emphasis surfaces |

## Guidance

Think of these four tokens as a stacking order, not a fixed 1:1 mapping to specific components: which token a given card uses depends on what it's stacked against. A card on the page body is `mediumEmphasis`; a modal floating above that same card is `highEmphasis` so it visually separates from what's behind it.

Never use a background token as a text or border color — text needs `alias.color.text.*` and borders need `alias.color.border.*`, both tuned for contrast against these backgrounds, not to double as fills themselves.

## Related

- `docs/context/color/text.md` — text colors tuned to sit on these backgrounds
- `docs/context/color/border.md` — border colors tuned to sit on these backgrounds
