# Intent Color — Usage Context

`alias.color.intent.*` communicates system feedback — information, success, warning, and critical states. These colors are reserved for meaning, not decoration: a user should be able to learn "orange-ish = warning" once and rely on it holding everywhere in the product.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.intent.infoHighEmphasis` | prominent informational surfaces (banners, badges that must stand out) | low-emphasis informational hints, or anything decorative |
| `alias.color.intent.infoLowEmphasis` | subtle informational surfaces (inline hints, quiet tags) | high-emphasis alerts or critical states |
| `alias.color.intent.onInfo` | text/icon color on either info background | any other background |
| `alias.color.intent.successHighEmphasis` | prominent success surfaces (confirmation banners) | subtle success hints |
| `alias.color.intent.successLowEmphasis` | subtle success surfaces (a quiet "saved" tag) | prominent confirmations or critical states |
| `alias.color.intent.onSuccess` | text/icon color on either success background | any other background |
| `alias.color.intent.warningHighEmphasis` | prominent warning surfaces | subtle warning hints |
| `alias.color.intent.warningLowEmphasis` | subtle warning surfaces | prominent warnings or critical states |
| `alias.color.intent.onWarning` | text/icon color on either warning background | any other background |
| `alias.color.intent.criticalHighEmphasis` | prominent error/destructive surfaces | subtle critical hints or informational states |
| `alias.color.intent.criticalLowEmphasis` | subtle critical surfaces | prominent errors |
| `alias.color.intent.onCritical` | text/icon color on either critical background | any other background |

## Guidance

Pick the **category** (info/success/warning/critical) by meaning, never by how the color happens to look — a warm palette brand might have a "warning" color that doesn't read as orange, but it must still only be used for warnings.

Pick **highEmphasis vs. lowEmphasis** by how much attention the message needs, not by visual preference: a full-page error banner is `criticalHighEmphasis`; a quiet inline validation note next to a form field is `criticalLowEmphasis`. Don't swap them for aesthetic reasons — high/low emphasis pairs are tuned for correct contrast against their matching `onX` token, and mixing tiers can produce insufficient contrast.

Never repurpose an intent color for branding or navigation — if it's not communicating a system state, it doesn't belong in this group (see `docs/context/color/interaction.md`).

## Related

- `docs/context/color/interaction.md` — for brand/interactive colors, not system feedback
- `docs/context/color/background.md` — for neutral surfaces with no semantic meaning
