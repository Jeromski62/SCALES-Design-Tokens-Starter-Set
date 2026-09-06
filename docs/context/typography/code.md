# Code Typography — Usage Context

`alias.font.code.*` provides the system's monospace style, for representing literal code or code-like values.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.code.small` | inline code snippets or small code blocks (variable names, short commands, config values) | prose, or UI labels — anything that isn't literally code or a code-like value |

## Guidance

Reserve monospace styling for genuine code-like content — file paths, variable names, commands, API values. Don't use it for emphasis or "technical feel" on regular prose; that undermines the signal that monospace is meant to carry (this text can be copy-pasted literally / is syntactically significant).

There is currently only one step in this category (`small`) — if a future need arises for a larger code-block style (e.g. a dedicated multi-line code block distinct from inline code), add it here following the same naming pattern (`alias.font.code.[variant]`) rather than repurposing `small` for a different size.

## Related

- `docs/context/typography/body.md` — for prose that happens to mention code, but isn't itself code
