---
name: genlayer-design
description: Use the GenLayer Design System when building GenLayer frontends, dashboards, explorer views, and hackathon demos. Points agents at the canonical DESIGN.md source for brand tokens, components, assets, and implementation constraints.
allowed-tools:
  - Bash
  - Read
  - WebFetch
---

# GenLayer Design System

Use this skill when creating or modifying GenLayer-facing UI: dashboards, explorer pages, validator/operator views, demo apps, landing pages, hackathon prototypes, or screenshots intended to represent GenLayer.

The canonical design reference is:

- Repository: [genlayer-foundation/genlayer-design](https://github.com/genlayer-foundation/genlayer-design)
- Agent entry point: [DESIGN.md](https://github.com/genlayer-foundation/genlayer-design/blob/main/DESIGN.md)

## Workflow

1. **Load the canonical reference first**
   - Read `DESIGN.md` from `genlayer-foundation/genlayer-design` before choosing colors, typography, spacing, component styling, or brand assets.
   - If the repo is available locally, prefer the local checkout. Otherwise fetch the GitHub copy.

2. **Use design tokens instead of inventing styles**
   - Reuse the documented color tokens, typography, spacing, radii, shadows, and component patterns.
   - Avoid one-off greens, gradients, button styles, cards, and dashboard chrome that only approximately match GenLayer.

3. **Choose the right artifact boundary**
   - Product/app repo: implement the UI and copy.
   - `genlayer-design`: source of truth for brand assets, tokens, reusable component references, and theme guidance.
   - Public docs or skills: explain how builders/agents should use the design system; do not duplicate the entire design source.

4. **Preserve accessibility and responsiveness**
   - Keep contrast, focus states, keyboard navigation, and small-screen behavior explicit.
   - Do not sacrifice readability for a brand effect.

5. **Validate before returning**
   - Confirm the UI points to or follows the current `DESIGN.md` guidance.
   - Run the app's normal lint/build/typecheck when available.
   - If producing a static mockup, inspect it visually before handing it off.

## Recommended Agent Prompt

```text
Use the GenLayer Design System. First read https://github.com/genlayer-foundation/genlayer-design/blob/main/DESIGN.md, then apply its tokens, components, brand assets, and accessibility guidance to this GenLayer UI. Do not invent new brand colors or component styles unless DESIGN.md explicitly leaves the area unspecified.
```

## Sharp Edges

- **Do not copy private/internal context into public UI.** Keep screenshots, examples, and placeholder data sanitized.
- **Do not hardcode secrets, wallet private keys, API keys, or real user data in examples.** Use placeholders.
- **Do not treat this skill as the design source of truth.** It routes agents to the canonical design repository; update that repository when brand rules change.
- **Do not apply GenLayer branding to non-GenLayer or partner-owned products without confirming the product boundary.**

## Quick Check

Before finalizing a UI change, answer:

- Did I read the current `DESIGN.md`?
- Are colors, fonts, spacing, cards, buttons, and states derived from documented tokens or components?
- Are responsive behavior and accessibility states covered?
- Did I run the relevant lint/build/typecheck or visually inspect the result?
