# Dimension — Component vs. Page Level Usage Context

`alias.size.*`, `alias.space.*`, `alias.grid.*`, and `alias.screen.*` all come from the same underlying scale (`scaling/factors`, see `docs/ARCHITECTURE.md`), which makes it tempting to treat them as interchangeable. They aren't: the meaningful decision here isn't which step of the scale to pick (that's just magnitude), it's **which of the four groups applies**, because each is scoped to a different layer of the UI.

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.size.[3xs–3xl, none]` | component-level sizing — icon/control/element dimensions | page grid or layout margins |
| `alias.space.[3xs–3xl, none]` | component-level spacing — gaps between elements inside a component | page grid gutters or layout margins |
| `alias.grid.cols` | number of columns in the page grid | component-internal layouts |
| `alias.grid.marginLeftRight` | page-level grid margin | component-internal spacing |
| `alias.grid.gutter` | gap between page grid columns | component-internal spacing |
| `alias.screen.maxWidth` | maximum content width for the page/breakpoint | component-internal sizing |
| `alias.screen.layout.paddingLeftRight` | horizontal page wrapper padding | component-internal spacing |

## Guidance

Ask "what am I sizing?" before picking a group:

- **Inside a component** (icon size, button padding, gap between a label and its icon) → `alias.size.*` / `alias.space.*`.
- **The page's structural grid** (how many columns, the gutter between them, the grid's outer margin) → `alias.grid.*`.
- **The page's overall content width and outer wrapper** → `alias.screen.*`.

A common anti-pattern this system is designed to prevent: using `alias.space.3xl` to fake a page margin, or `alias.grid.marginLeftRight` to pad the inside of a card. Both will *work* numerically (they're all just `px` values under the hood), but they break the moment someone needs to change page-layout margins independently from component spacing (or vice versa) — which is precisely the flexibility this separation exists to protect, since both scales originate from the same `scaling/factors` tier but are exposed through different breakpoint contexts (`breakpoint/[bp]/dimension` vs. `breakpoint/[bp]/grid` vs. `breakpoint/[bp]/layout`).

Within `alias.size.*`/`alias.space.*`, the T-shirt steps (`3xs`…`3xl`) are pure magnitude — there's no fixed rule like "`md` is always for buttons." Pick the step by how large the gap/element should look relative to its neighbors, not by convention.

## Related

- `docs/context/border.md` — border width/radius, visually similar but semantically separate from spacing
