---
name: accessibility-specialist-audit
description: >-
  Perform a structured accessibility audit of Figma flows against WCAG targets.
  Use before eng handoff or after major UI changes.
---

# Accessibility audit

## Process

1. Confirm scope and WCAG level with Chief.
2. Walk each flow: keyboard order, focus, labels, contrast, touch targets, errors.
3. Log findings in `templates/audit-report.md` with stable IDs.
4. Draft **acceptance criteria** QA can execute without interpretation.

## Tools

On Grok Bot, see activities A1–A8 in the parent `SKILL.md`. The core loop is:

1. `figma.get_variable_defs` to collect the hex values of text and fill tokens
2. `Google-slides.check_contrast` to check up to 40 pairs per call (set `large: true` for text at 24pt or more, or bold at 19pt or more)
3. `figma.get_design_context` for structure, labels, and target sizes
4. `cursor.WebFetch` on the WCAG Understanding page for each criterion you cite

Automated checks support manual review but don't replace it.

## Pairing

Review UI Designer interaction notes and Motion reduced-motion rows before sign-off.
