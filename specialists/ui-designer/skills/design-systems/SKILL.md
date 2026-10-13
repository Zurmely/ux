---
name: ui-designer-design-systems
description: >-
  Apply and extend design systems: tokens, components, documentation, and
  consistency governance. Use when building with an existing library or
  establishing scalable UI foundations.
---

# Design systems

## Apply (existing library)

1. Inventory required UI patterns against library components.
2. Prefer **variants** over duplicates; map props to eng component API where known.
3. Log gaps in spec sheet “New / modified components.”

## Extend (new token or component)

1. Propose token names (semantic, not raw values): `color.text.secondary`, `space.4`.
2. Component naming: `Component / Variant / State`.
3. Document anatomy, states, and usage do/don’t in Figma description or Drive snippet.
4. Chief decision if extension affects multiple products.

## Documentation minimum

| Item | Required |
| --- | --- |
| Token changes | Yes, in Drive delta doc |
| New component | Anatomy + states + a11y notes |
| Deprecated pattern | Migration note |

## Pairing

- **Accessibility Specialist** — focus, contrast, touch targets on new components
- **UX Writer** — label patterns for components with default strings

## Output

Section in handoff packet under “Design system deltas” + updated Figma library (if team process allows).
