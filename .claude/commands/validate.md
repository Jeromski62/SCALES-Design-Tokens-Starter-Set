---
name: validate
description: Validate tokens/tokens.json against all SCALES conventions — broken references, compound tokens, missing types, hex casing, mode parity, brand structure parity
disable-model-invocation: true
allowed-tools: Read, Grep
---

# Skill: validate

Validate `tokens/tokens.json` against all SCALES conventions. Run every check and report results clearly.

## Steps

1. Load `tokens/tokens.json`

2. **Broken references** — collect all `{token.path}` references from `$value` fields. Collect all defined token paths. Report any reference that does not resolve to a defined token.

3. **Compound tokens** — find any token node that has both a `$value` and non-`$` children. A node must be either a leaf or a group, never both.

4. **Missing `$type`** — every token with a `$value` must also have a `$type`. Report any that do not.

5. **Hex color casing** — all hex color values must be UPPERCASE (e.g. `#F7FBEB`). Report any lowercase hex values and their exact token path.

6. **Sizing without unit** — any token with `$type: "sizing"` or `$type: "spacing"` or `$type: "dimension"` must have a value with a unit (e.g. `4px`). Report bare numbers.

7. **`$description` quality**
   - Must start with a lowercase letter
   - Must not end with a space
   - Report all violations with token path and current value

8. **Mode parity** — `mode/dark` and `mode/light` must define the exact same set of token paths. Report any token present in one but missing in the other.

9. **Brand structure parity** — all brands under `brand/` must expose the same internal structure. Compare `brand/brandA/color`, `brand/brandA/font`, `brand/brandA/shape` against every other brand and report structural differences.

10. **`$type: "number"` values** — must be numeric JSON values, not strings. E.g. `12` not `"12"`.

## Output

Report each check with a clear pass ✅ or fail ❌ status. For failures, list every affected token path and the specific issue. At the end, summarize total issues found.
