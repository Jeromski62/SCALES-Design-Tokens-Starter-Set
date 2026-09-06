# Interaction & Brand Color — Usage Context

`alias.color.primary.*` and `alias.color.secondary.*` carry the brand's interactive and identity colors. `primary` is the dominant interactive color (the one used most often); `secondary` supports it — use it to create hierarchy when two interactive elements appear together (e.g. a primary and a secondary button side by side).

## Tokens

| Token | Use for | Not for |
|---|---|---|
| `alias.color.primary.interaction` | background of the app's main interactive elements (primary buttons, active tabs, links-as-buttons) | static or decorative backgrounds that carry no interaction |
| `alias.color.primary.onInteraction` | text/icon color placed on top of `primary.interaction` | standalone text or icons that are not on that background |
| `alias.color.primary.brand` | background for primary brand-identity elements (logo lockups, hero accents) | interactive or state backgrounds — use `primary.interaction` instead |
| `alias.color.primary.onBrand` | text/icon color placed on top of `primary.brand` | any other background |
| `alias.color.secondary.interaction` | background of secondary interactive elements (secondary buttons, less prominent controls) | the app's primary/default interactive elements |
| `alias.color.secondary.onInteraction` | text/icon color placed on top of `secondary.interaction` | standalone text or icons that are not on that background |
| `alias.color.secondary.brand` | background for secondary brand-identity accents | interactive or state backgrounds |
| `alias.color.secondary.onBrand` | text/icon color placed on top of `secondary.brand` | any other background |

## Guidance

`interaction` vs. `brand` is the key distinction in this group: `interaction` colors respond to user action (a button you can press), `brand` colors express identity and typically sit on static surfaces (a hero section, a logo backdrop). Don't use a `brand` token where an `interaction` token belongs — a button styled with `primary.brand` loses the semantic link to "this is clickable" that tooling and future theme changes rely on.

`primary` vs. `secondary` is a hierarchy choice, not a palette choice: if a screen has two competing calls to action, the one you want the user to notice first gets `primary`, the other gets `secondary`. Never use both interchangeably on equivalent elements — that defeats the purpose of the hierarchy.

Example: a "Save" button uses `primary.interaction` for its background and `primary.onInteraction` for its label; a neighboring "Cancel" button uses `secondary.interaction`/`secondary.onInteraction`.

## Related

- `docs/context/color/state.md` — hover/press/disabled overlays that sit on top of these backgrounds
- `docs/context/color/intent.md` — for feedback colors (success/warning/etc.), not brand/interaction colors
