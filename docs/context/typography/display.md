# Display Typography — Usage Context

`alias.font.display.*` is the top of the type scale — reserved for the single largest, most attention-grabbing headline on a page (hero sections, landing pages, splash moments).

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.font.display.1` | the single most prominent headline on a page | body copy, or a second simultaneous headline of equal prominence |
| `alias.font.display.2` | a secondary hero-level headline (e.g. subtitle under a `display.1`, or the hero on a less prominent page) | body copy, or standard section headlines |

## Guidance

Display styles should appear **at most once or twice per page** — if you find yourself reaching for `display.1` on more than one element in the same view, one of them almost certainly belongs to `alias.font.headline.*` instead (see `docs/context/typography/headlines.md`). Display type is a moment, not a section-heading pattern.

Never use display styles for body copy, form labels, or UI chrome — their line-height and letter-spacing are tuned for a handful of large words, not for reading paragraphs.

## Related

- `docs/context/typography/headlines.md` — the next step down for repeatable section titles
