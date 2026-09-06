# Label Typography — Usage Context

`alias.font.label.*` is for UI chrome text — the short, functional text on interactive controls (buttons, tabs, form field labels, tags), as opposed to content the user reads for information.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.label.short` | single-line UI labels (button text, tab labels, tags) | labels that wrap onto multiple lines, or paragraph copy |
| `alias.font.label.long` | UI labels that may wrap onto multiple lines (e.g. a checkbox label with a longer sentence) | single-line labels, or paragraph copy |

## Guidance

The `short`/`long` split is about **line-wrapping behavior**, not visual size — pick `long` whenever the label's content is allowed to wrap in your layout (its line-height is tuned for multi-line legibility), and `short` when the control enforces a single line (e.g. `text-overflow: ellipsis`).

Labels are functional/interactive text, not content — if the text is something the user reads for its own sake (an article, a description, an explanation), it belongs in `alias.font.body.*` instead, even if it's visually small.

## Related

- `docs/context/typography/body.md` — for content the user reads, not UI chrome
- `docs/context/typography/hyperlinks.md` — for interactive text that navigates, rather than labels a control
