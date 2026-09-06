# Hyperlink Typography — Usage Context

`alias.font.hyperlink.*` styles interactive, navigating text — inline links within body copy or standalone text links, distinct from button labels (`alias.font.label.*`) which trigger actions rather than navigate.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.hyperlink.default` | a hyperlink's resting state | static, non-interactive text |
| `alias.font.hyperlink.hover` | a hyperlink while hovered | a hyperlink's resting state — swap to `default` when the pointer leaves |

## Guidance

Only apply hyperlink typography to text that actually navigates (changes the URL/route) or triggers an equivalent "go somewhere" action. A clickable action that stays on the page (opens a modal, submits a form) is a button and should use `alias.font.label.*` plus `alias.color.state.*` for its interaction feedback, not hyperlink typography — mixing the two confuses the visual language between "this navigates" and "this performs an action here."

`hover` is a state variant, not a separate style choice — a hyperlink should always start in `default` and transition to `hover` only in response to the pointer, exactly like `alias.color.state.hover` is a transient overlay rather than a base style.

## Related

- `docs/context/typography/body.md` — the surrounding paragraph copy hyperlinks are typically embedded in
- `docs/context/typography/labels.md` — for action-triggering controls, not navigation
- `docs/context/color/state.md` — the same default/hover state pattern applied to color
