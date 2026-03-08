# SCALES

**A design token boilerplate for your design system.**

SCALES gives you a production-ready, structured token set to build on — so you don't have to start from scratch. It is designed for design teams working with Figma and Token Studio, and is built around an X-tier architecture concept by Marco-Christian Krenn.

---

## What's inside

- A multi-brand token architecture with two example brands (brandA, brandB)
- Light and dark mode support out of the box
- A global dimension scale as the foundation for all size and spacing values
- A full typescale with responsive-ready breakpoint structure
- W3C DTCG-compliant token format — compatible with tools like Zeroheight, Style Dictionary, and others
- Written for and managed with [Tokens Studio for Figma](https://tokens.studio/)

---

## Architecture

SCALES is built on an X-tier model. Each tier has a clear responsibility:

```
scaling/factors    → global dimension scale (brand-independent)
brand/[brandX]/*   → brand-specific primitives (color, font, shape)
breakpoint/[bp]/*  → context tokens (dimension, typescale, border, grid, layout)
mode/dark|light    → light and dark mode color mappings
alias/*            → PUBLIC API — the only tier consumed by products
```

Only the `alias/` tier is released and consumed by products. All other tiers exist to keep the system scalable, maintainable, and brand-swappable.

For a full breakdown see [ARCHITECTURE.md](./ARCHITECTURE.md) and [CONVENTIONS.md](./CONVENTIONS.md).

---

## Getting started

1. Open the `tokens.json` file in [Tokens Studio for Figma](https://tokens.studio/)
2. Explore the token structure and connect it to your Figma library
3. Swap out `brand/brandA/*` with your own brand colors, fonts, and shapes
4. Use the `alias/*` tokens in your components — these are your stable public API

---

## Working with AI agents

SCALES ships with agent-readable documentation and executable skill files:

- [`ARCHITECTURE.md`](./docs/ARCHITECTURE.md) — tier model, reference chains, token structure
- [`CONVENTIONS.md`](./docs/CONVENTIONS.md) — naming, value formats, structural rules
- [`AGENT-SETUP.md`](./docs/AGENT-SETUP.md) — how to set up an agent-assisted workflow
- [`CLAUDE.md`](./CLAUDE.md) — instructions for Claude Code and compatible agents

Any agent with access to these files has enough context to extend the token system correctly.

The `skills/` folder contains step-by-step task guides that any agent or tool can execute — they are plain markdown, not tied to a specific tool. Point your agent at the relevant file and it has everything it needs to complete the task correctly.

| Skill | Purpose |
|-------|---------|
| [`skills/validate.md`](./skills/validate.md) | Validate `tokens/tokens.json` against all conventions |
| [`skills/add-brand.md`](./skills/add-brand.md) | Add a new brand to the system |
| [`skills/add-color.md`](./skills/add-color.md) | Add a new palette color to an existing brand |
| [`skills/add-breakpoint.md`](./skills/add-breakpoint.md) | Add a new breakpoint tier |

If you use **Claude Code**, these skills are also available as slash commands: `/validate`, `/add-brand`, `/add-color`, `/add-breakpoint`.

---

## Notes

- This is a starter set — no Style Dictionary configuration or build pipeline is included
- The `$themes` and `$metadata` sections in `tokens.json` are Figma/Token Studio configuration and should not be edited manually
- Feedback and contributions are welcome — open an issue if you spot anything

---

## Feedback

If you have any feedback or notice any issues, I would be grateful to hear from you.
