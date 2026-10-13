---
name: ux-writer-ui-copy
description: >-
  Write and refine UI microcopy for screens, components, errors, and onboarding.
  Use when Figma frames need final or draft user-facing text.
---

# UI copy

## When to use

- High- or mid-fi screens exist in Figma
- Engineering needs string inventory
- Localization prep

## Process

1. Walk flows in Figma; assign **string IDs** (`flow.screen.element`).
2. Draft copy using voice guidelines; prioritize clarity over cleverness.
3. Pair with UI Designer on truncation, tooltips, and progressive disclosure.
4. Document **aria-label** suggestions where visible label is insufficient (flag a11y).

## Patterns

- **Primary button:** verb + object (“Save changes”)
- **Errors:** problem + action (“Connection lost. Retry or work offline.”)
- **Empty states:** benefit + CTA (“No projects yet. Create one to collaborate.”)

## Output

Rows in `templates/copy-deck.md`.
