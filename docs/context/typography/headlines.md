# Headline Typography — Usage Context

`alias.font.headline.*` provides a 5-step hierarchy for section and subsection titles — the repeatable heading pattern used throughout a product, as opposed to the one-off hero moments covered by `alias.font.display.*`.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.headline.1` | top-level section titles (page title, major section headers) | hero/display moments, or body copy |
| `alias.font.headline.2` | major subsection titles | top-level section titles, or body copy |
| `alias.font.headline.3` | minor subsection titles | major section titles, or body copy |
| `alias.font.headline.4` | component-level titles (card titles, panel headers) | page- or section-level titles |
| `alias.font.headline.5` | the smallest headline step, for compact component titles (e.g. a list-group header) | section titles, or body copy |

## Guidance

Treat `headline.1`–`5` as a strict nesting order that mirrors document structure (like HTML `h1`–`h5`): a `headline.3` should not appear as a direct child of a `headline.1` if a `headline.2` exists in the same hierarchy — skipping levels breaks the visual (and often semantic/accessibility) hierarchy. Pick the level by the heading's *depth in the page's outline*, not by how large you want the text to look — if you need bigger text without implying a deeper/shallower heading level, that's a sign you actually want `alias.font.display.*` or a component-specific override, not a headline mismatch.

Never use a headline style for a UI label (button text, form label) or paragraph copy — use `alias.font.label.*` or `alias.font.body.*` respectively.

## Related

- `docs/context/typography/display.md` — one level up, for hero-scale moments
- `docs/context/typography/body.md` — for paragraph copy that follows a headline
- `docs/context/typography/labels.md` — for UI chrome text, not content headings
