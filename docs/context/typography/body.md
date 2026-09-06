# Body Typography — Usage Context

`alias.font.body.*` is for paragraph/content copy — text the user reads for its own sake, as opposed to UI chrome (`alias.font.label.*`) or headings (`alias.font.headline.*`/`display.*`).

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.body.short` | single-line body text (e.g. a one-line description, a table cell) | multi-line paragraphs, or UI labels |
| `alias.font.body.long` | multi-line paragraph copy (article text, longer descriptions) | single-line body text, or UI labels |
| `alias.font.body.small` | small or secondary body copy (footnotes, dense data tables, metadata) | primary paragraph text, or UI labels |

## Guidance

Choose `short` vs. `long` the same way as `alias.font.label.*` — by whether the content is expected to wrap, not by how much text there happens to be today. `small` is a separate, size-based step for genuinely secondary reading content; don't reach for it just to fit more text into a tight layout — that's a layout problem, not a typography one.

Never substitute a headline or label style for body copy just because it "looks about the right size" — body styles carry line-heights tuned for comfortable multi-word reading that heading and label styles don't.

## Related

- `docs/context/typography/headlines.md` — for section titles that introduce body copy
- `docs/context/typography/labels.md` — for UI chrome, not readable content
- `docs/context/typography/hyperlinks.md` — for interactive text within body copy
