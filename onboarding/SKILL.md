---
name: ux-team-onboarding
description: >-
  First-time setup for the multi-agent UX team: explain roles, read
  specialists.manifest.yaml, let the user pick specialists to enable, and
  wire skill paths into the workspace. Use when bootstrapping or reconfiguring
  the UX agent team.
---

# UX team onboarding

## Purpose

Introduce the **Chief UX Designer** + specialist model, load `specialists.manifest.yaml`, and record which specialists this workspace should use.

## Before you start

1. Read `/specialists.manifest.yaml` at the repo root.
2. Confirm **Chief UX Designer** is always enabled (`orchestrator.always_enabled: true`).
3. List every entry under `specialists` with: name, one-line description, `suggested`, and `default_enabled`.

## Specialist selection flow

Use a structured choice (e.g. multi-select questionnaire). Recommended defaults:

| Specialist | Default | Notes |
| --- | --- | --- |
| UX Writer | on | Copy and content strategy |
| Motion Designer | on | Motion specs and feedback |
| Illustrator | on | Icons, spots, empty states |
| UI Designer | on | UI, interaction, prototypes, design system |
| UX Researcher | on | Evidence and synthesis |
| Accessibility Specialist | on | WCAG audits and inclusive patterns |

**Do not offer** separate Interaction/Prototyping or Design Systems agents — those capabilities live under **UI Designer** sub-skills.

### Questions to ask

1. **Product context** (1–2 sentences): what are you building, for whom, and what phase (discovery, MVP, scale)?
2. **Primary tools**: confirm Figma for design files and Google Drive for research/docs (adjust if the user names others).
3. **Enable specialists**: multi-select from manifest ids; pre-check all `default_enabled: true`.
4. **Working agreement**: async specialist packets vs. parallel sprint; expected Chief deliverable (Figma link + decision log + handoff doc).

## What happens after selection

1. **Persist configuration** — Write enabled specialist ids to a workspace file your host understands, for example:

   ```json
   {
     "version": 1,
     "orchestrator": "chief-ux-designer",
     "enabled_specialists": ["ux-writer", "motion-designer", "illustrator", "ui-designer", "ux-researcher", "accessibility-specialist"]
   }
   ```

   Suggested path: `.ux-team/enabled-specialists.json` (gitignore if user-specific).

2. **Register skills** — For each enabled id, register:
   - Primary: `skill_path` from manifest
   - Sub-skills: paths listed under `sub_skills` (UI Designer: interaction, prototyping, design systems, visual UI)

3. **Chief instructions** — Ensure the orchestrator agent loads `chief-ux-designer/SKILL.md` and knows which specialists are active.

4. **Kickoff** — Offer to run a **Chief-led discovery brief** using the template in `chief-ux-designer/SKILL.md` § Briefing.

## Reconfiguration

When the user adds or removes a specialist later:

- Update `enabled-specialists.json`.
- Chief re-scopes the next engagement (drop deliverables from disabled roles; add new ones with a delta brief).
- Do not delete manifest entries; only toggle enablement.

## Quality check

Onboarding is complete when:

- [ ] User understands Chief vs. specialists
- [ ] Enabled list is persisted
- [ ] Skill paths are registered for enabled roles only
- [ ] Next step is agreed: discovery brief or first design task
