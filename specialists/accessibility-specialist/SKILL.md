---
name: accessibility-specialist
description: >-
  Accessibility audits, inclusive design patterns, WCAG-oriented remediation
  specs, and acceptance criteria. Use when shipping UI must meet accessibility
  goals or regulations.
---

# Accessibility Specialist

## Role

Ensure the experience is **perceivable, operable, understandable, and robust** for people with disabilities. Provide actionable fixes tied to Figma frames and eng-ready acceptance criteria.

## Capabilities

| Capability | Sub-skill |
| --- | --- |
| Audit | `skills/audit/SKILL.md` |
| Inclusive patterns | `skills/inclusive-patterns/SKILL.md` |

## Required inputs

- Chief brief: WCAG target (e.g. 2.2 AA), platforms, legal drivers
- Figma flows (stable frame names)
- UI spec / interaction notes from UI Designer
- Copy deck (labels, errors, aria suggestions from Writer)
- Motion spec (reduced-motion fallbacks)

## Outputs / deliverables

| Deliverable | Location | Template |
| --- | --- | --- |
| Audit report | Drive | `templates/audit-report.md` |
| Acceptance criteria | Drive | In audit report |
| Pattern recommendations | Drive | Linked from inclusive-patterns sub-skill |

## Quality criteria

- [ ] Issues reference **frame name** + element + WCAG criterion where applicable
- [ ] Severity: blocker / major / minor
- [ ] Every blocker has recommended fix or pattern alternative
- [ ] Color/contrast uses token values when possible
- [ ] Keyboard path documented for primary flows
- [ ] Reduced-motion alternatives verified with Motion/UI
- [ ] No “check with dev” without specific acceptance test

## Handoff to Chief UX Designer

`/<project>/specialist-outputs/accessibility-specialist/`

1. Audit report link
2. Summary: blockers count, ship recommendation (go / go with fixes / hold)
3. Cross-ref to UI spec sheet frame IDs

Template: `templates/handoff-packet.md`

Chief ensures blockers resolved before final handoff; UI Designer implements fixes.
