# Working with Agents

SCALES is designed to work alongside AI agents. This guide explains how to set up an agent-assisted workflow, either with or without Figma or Tokens Studio.

Agents do not replace Figma or Tokens Studio. Agents work on the JSON level and help you extend, validate, and maintain the token structure and speed up your work.

---

## What agents can do with SCALES

- Validate the token file against all conventions (`skills/validate.md`)
- Add a new brand guided by a structured process (`skills/add-brand.md`)
- Add a new palette color to an existing brand (`skills/add-color.md`)
- Add a new breakpoint tier (`skills/add-breakpoint.md`)
- Answer questions about the architecture and conventions
- Review the token file for inconsistencies, broken references, or naming issues

---

## Prerequisites

- An AI agent that can read and write files in your repository
  - Recommended: [Claude Code](https://claude.ai/code), Cursor, or GitHub Copilot Workspace
- `tokens/tokens.json` accessible in the repo
- The agent has access to `CLAUDE.md`, `docs/ARCHITECTURE.md`, `docs/CONVENTIONS.md`, and the `skills/` folder

No additional tooling or build pipeline is required to get started.

---

## Recommended workflow

### Option A — Agent + Tokens Studio (recommended)

Use Tokens Studio as your Figma-sync layer and agents for structural work on the JSON.

```
Figma  ←→  Tokens Studio  ←→  tokens/tokens.json  ←→  Agent
```

1. Make structural changes (new brand, new color, new breakpoint) via agent using the skills
2. Run `/validate` to confirm the result is clean
3. Pull the updated `tokens.json` into Tokens Studio
4. Sync to Figma

This keeps Tokens Studio as the source of truth for Figma while letting agents handle the heavy lifting on the JSON side.

### Option B — Agent only (no Figma)

If you are working in a code-only environment without Figma:

1. Point your agent at `tokens/tokens.json`
2. Use the skills in `skills/` as task guides
3. Run `/validate` after every change
4. Feed the output tokens into your build pipeline (e.g. Style Dictionary)

---

## How to give an agent context

Point your agent to these files before starting any task:

```
CLAUDE.md                  ← start here
docs/ARCHITECTURE.md       ← tier model and structure
docs/CONVENTIONS.md        ← naming, types, formatting rules
skills/[relevant-skill].md ← the task to execute
```

Most agents (Claude Code, Cursor) will pick up `CLAUDE.md` automatically if it is in the project root.

---

## Running a skill

Skills are step-by-step task guides written in plain markdown. Any agent that can read files can follow them.

Example with Claude Code:
```
read skills/add-brand.md and follow the steps
```

Example with Cursor or Copilot:
```
follow the instructions in skills/add-brand.md
```

The agent will ask clarifying questions (brand name, colors, font) before making any changes to `tokens/tokens.json`.

---

## Validation

Always run validation after making changes to `tokens/tokens.json`.

```
read skills/validate.md and run all checks against tokens/tokens.json
```

The validate skill checks for:
- Broken token references
- Compound tokens
- Missing `$type`
- Lowercase hex values
- Sizing tokens without units
- Description formatting issues
- Mode parity (dark/light)
- Brand structure parity

---

## Limitations

Agents are guides, not fully autonomous systems. Keep these in mind:

- **Color palette generation** — agents can fill in a palette structure but generating perceptually balanced color scales is unreliable. Always review generated color values visually before using them.
- **Tokens Studio sync** — agents write directly to `tokens.json`. After agent changes, always re-sync in Tokens Studio to keep Figma up to date.
- **No build pipeline included** — SCALES does not ship with Style Dictionary or any transformer config. If you need CSS variables or other outputs, that setup is up to you.
