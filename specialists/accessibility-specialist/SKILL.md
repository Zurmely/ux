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

## Tools on Grok Bot

See `tools/grok-bot.md` for the full catalog and required skills.

| Tool | Purpose |
| --- | --- |
| `figma.create_session`, `get_metadata` | List the frames, layer order, and names. Layer order is a proxy for reading and focus order |
| `figma.get_design_context` (load `figma-design-to-code`) | Inspect a node's structure, semantics hints, and dimensions (touch targets) |
| `figma.get_variable_defs` | Get the exact hex values of text and fill tokens for contrast math |
| `Google-slides.check_contrast` | Compute WCAG AA ratios for up to 40 hex pairs per call, with the nearest passing color for failures. Pure calculation, so it works for any UI |
| `figma.get_screenshot` | Capture visual evidence for each finding |
| `figma.use_figma` (load `figma-use`) | Add a11y annotations (focus order, roles, labels) in an annotation layer. Don't change design layers |
| `figma.generate_figma_design` | Capture the live product into Figma to audit what actually shipped |
| `figma.get_motion_context` | Check animation durations, loops, and flashing against the reduced-motion and seizure criteria |
| `cursor.WebFetch` | Read the WCAG 2.2 Understanding docs and ARIA Authoring Practices for each cited criterion |
| `Github.search_code`, `get_file_contents` | Check the implemented semantics (ARIA, labels) when the code is available |
| `Github.issue_write` | File remediation tickets, one per blocker, linked to the audit ID (on request) |
| `Google-drive.copy_file`, `create_file` | Create the audit report from the template |

## Activities

| # | Activity | Steps and tools |
| --- | --- | --- |
| A1 | **Scope** | Confirm the WCAG level with the Chief. `figma.get_metadata` on the in-scope flows. For shipped product, also run `generate_figma_design` on the live URL |
| A2 | **Contrast pass** | `figma.get_variable_defs` to collect every text and background pair, then batch them through `Google-slides.check_contrast` (mark large text). Log failures with the suggested passing color |
| A3 | **Structure pass** | `figma.get_design_context` per frame: heading hierarchy, labels on inputs and icon buttons, touch targets of at least 24×24 CSS px (WCAG 2.2 AA) |
| A4 | **Keyboard and focus** | Infer tab order from the layer order. Check that every interactive state has a visible focus style. Record traps |
| A5 | **Motion pass** | `figma.get_motion_context`. Check that reduced-motion variants exist and nothing flashes more than three times a second |
| A6 | **Annotate** | `figma.use_figma` adds focus order numbers and role or label notes on a dedicated annotation layer |
| A7 | **Report** | Fill in the audit report with screenshots from `figma.get_screenshot` and criteria cited from `cursor.WebFetch` |
| A8 | **Tickets** | With approval, `Github.issue_write` for each blocker or major issue |

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
