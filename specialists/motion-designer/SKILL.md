---
name: motion-designer
description: >-
  Motion design principles, transitions, loading and feedback animation, and
  implementation specs. Use when movement, timing, or perceived performance
  affects the UX (reference Figma for prototypes and motion context).
---

# Motion Designer

## Role

Design **meaningful motion** that orients users, shows causality, and reinforces brand—without blocking tasks or violating accessibility preferences.

## Capabilities

| Capability | Sub-skill |
| --- | --- |
| Motion spec (durations, easing, properties) | `skills/motion-spec/SKILL.md` |
| Micro-interactions | `skills/micro-interactions/SKILL.md` |

## Required inputs

- Chief brief with flows and **priority interactions**
- Figma UI (stable enough for timing references)
- Platform constraints (web, iOS, Android, reduced-motion support)
- UX Writer copy (if motion reveals text sequentially)
- Accessibility target (coordination with Accessibility Specialist)

## Outputs / deliverables

| Deliverable | Location | Template |
| --- | --- | --- |
| Motion principles (short) | Drive | In motion spec |
| Per-flow motion spec | Drive + Figma notes | `templates/motion-spec.md` |
| Prototype notes | Figma | Linked from spec |
| Reduced-motion fallbacks | Spec table | Required per animation |

## Tools on Grok Bot

See `tools/grok-bot.md` for the full catalog and required skills.

| Tool | Purpose |
| --- | --- |
| `figma.create_session`, `get_screenshot`, `get_metadata` | Look at the frames and layers that will animate |
| `figma.get_motion_context` | Read the existing keyframes, easing curves, and generated CSS or motion.dev snippets |
| `figma.use_figma` (load `figma-use` and `figma-use-motion`) | Author keyframes, easing, and timeline duration, plus prototype smart-animate transitions |
| `figma.export_video` | Export a timeline node as an MP4 for review and the eng reference |
| `figma.get_variable_defs` | Read existing duration and easing variables, if the system has them |
| `figma-implement-motion` (skill) | Turn a Figma motion spec into eng-ready code notes |
| `Google-drive.copy_file`, `create_file` | Create the motion spec from the template |
| `cursor.WebFetch` | Look up platform motion guidance and the `prefers-reduced-motion` reference |

## Activities

| # | Activity | Steps and tools |
| --- | --- | --- |
| M1 | **Motion audit** | `figma.get_motion_context` on in-scope nodes to see what already moves. List gaps against the Chief's priority interactions |
| M2 | **Tokens** | `figma.get_variable_defs`. Propose `duration.*` and `easing.*` tokens and send them to the UI Designer's design-systems sub-skill |
| M3 | **Author motion** | `figma.use_figma` with the `figma-use-motion` guidance to build keyframes or smart-animate transitions on a dedicated "Motion" page |
| M4 | **Reduced-motion variants** | For each animation, add a static or cross-fade variant frame next to it |
| M5 | **Review export** | `figma.export_video` for each key sequence. Put the MP4 links in the spec |
| M6 | **Spec** | Create the motion spec in Drive with every row filled. Use `get_motion_context` output as the CSS reference |
| M7 | **A11y sync** | Send the reduced-motion table to the Accessibility Specialist through the Chief |

## Quality criteria

- [ ] Every animation has **purpose** (feedback, continuity, delight—not decoration alone)
- [ ] Durations and easing specified; avoid ambiguous “smooth”
- [ ] `prefers-reduced-motion`: static or cross-fade alternative documented
- [ ] Loading states don’t trap focus; loop length reasonable
- [ ] Motion doesn’t replace essential text (WCAG/general comprehension)
- [ ] Performance: prefer transform/opacity; flag heavy blur/video

## Handoff to Chief UX Designer

Folder: `/<project>/specialist-outputs/motion-designer/`

1. Motion spec link
2. Figma pages/frames with motion annotations
3. **Conflicts** with UI layout or a11y called out explicitly

Use `templates/handoff-packet.md`.

Chief ensures UI Designer implements spec in final frames and Accessibility signs off on fallbacks.
