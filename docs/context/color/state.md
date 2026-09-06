# State Color — Usage Context

`alias.color.state.*` covers transient interaction feedback — colors that appear only while a user is actively interacting with an element (hovering, pressing, selecting) or while an element is disabled. Every token in this group describes a temporary condition, never a resting/default appearance.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.state.disable` | background of a disabled control | interactive or hover backgrounds |
| `alias.color.state.onDisable` | text/icon color on a disabled background | any other background |
| `alias.color.state.hover` | overlay applied while the pointer is over an element | a default/static background |
| `alias.color.state.press` | overlay applied while an element is actively pressed/clicked | a default/static background |
| `alias.color.state.select` | background of a selected element (e.g. an active list item) | hover or press overlays |
| `alias.color.state.onSelect` | text/icon color on a selected background | any other background |
| `alias.color.state.selectInverted` | selected-state background on a dark/inverted surface | selected state on a default light surface |
| `alias.color.state.onSelectInverted` | text/icon color on `selectInverted` | selected state on a default light surface |

## Guidance

`hover` and `press` are overlays (semi-transparent, meant to be composited on top of an existing background — see the `$extensions.studio.tokens.modify` alpha values on these two tokens), not standalone fills. Don't use them as a component's base/resting background color; they only make sense layered on top of `primary.interaction`, `background.*`, etc.

`disable` and `select` are full backgrounds, not overlays — but they're still conditional states: a component should switch to `disable` only while genuinely non-interactive, and to `select` only while genuinely the active/chosen item, never as a permanent style choice.

Use the `Inverted` variants only when the surrounding surface is itself dark/inverted (see `docs/context/color/text.md` for the same default/inverted split) — mixing a non-inverted select color onto an inverted surface will fail contrast.

## Related

- `docs/context/color/interaction.md` — the base interactive backgrounds these states overlay
- `docs/context/color/background.md` — the base surfaces `disable`/`select` backgrounds replace
