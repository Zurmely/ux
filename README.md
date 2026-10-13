# UX Agent Skills

A **library of agent skills** for a multi-agent UX team. A **Chief UX Designer** orchestrates specialist agents; each specialist owns a slice of the experience and returns structured outputs the Chief reconciles into a final deliverable.

Design work is expected in **Figma**; research, briefs, and decision logs in **Google Drive** (or equivalent). Skills are **tool-agnostic** beyond those conventions.

## Concept

```text
                    ┌─────────────────────────┐
                    │   Chief UX Designer     │
                    │  brief · reconcile ·    │
                    │  decide · handoff       │
                    └───────────┬─────────────┘
          ┌─────────────────────┼─────────────────────┐
          ▼                     ▼                     ▼
   UX Researcher           UI Designer          UX Writer
   Accessibility           Motion Designer      Illustrator
```

1. **Brief** — Chief scopes the problem and assigns parallel workstreams.
2. **Produce** — Enabled specialists execute using their `SKILL.md` (and sub-skills).
3. **Reconcile** — Chief resolves conflicts, fills gaps, and records decisions.
4. **Hand off** — Final Figma structure, specs, copy doc, motion notes, a11y checklist, and links in Drive.

## Specialists

| ID | Role | Scope |
| --- | --- | --- |
| `chief-ux-designer` | Chief UX Designer | Always on — orchestration |
| `ux-writer` | UX Writer | Voice, UI copy, content strategy |
| `motion-designer` | Motion Designer | Motion principles and specs |
| `illustrator` | Illustrator | Icons, spots, visual narrative |
| `ui-designer` | UI Designer | Visual UI, **interaction design**, **prototyping**, **design systems** |
| `ux-researcher` | UX Researcher | Plans, studies, synthesis |
| `accessibility-specialist` | Accessibility Specialist | Audits, inclusive patterns, acceptance criteria |

There are **no separate** Interaction/Prototyping or Design Systems agents; those capabilities are **sub-skills of UI Designer**.

## Repository structure

```text
.
├── README.md
├── specialists.manifest.yaml    # Registry + default enablement
├── onboarding/
│   └── SKILL.md                 # First-time specialist selection
├── chief-ux-designer/
│   └── SKILL.md
└── specialists/
    ├── ux-writer/
    ├── motion-designer/
    ├── illustrator/
    ├── ui-designer/             # + interaction, prototyping, design-systems
    ├── ux-researcher/
    └── accessibility-specialist/
```

Each specialist folder contains:

- **`SKILL.md`** — YAML frontmatter (`name`, `description`) plus role, I/O, quality bar, handoff to Chief
- **`skills/`** — Optional sub-skills for distinct capabilities
- **`templates/`** — Checklists and deliverable scaffolds where useful

## Getting started

1. Clone this repo into your agent workspace (or install skills from it).
2. Run the **onboarding** skill: `onboarding/SKILL.md`.
3. Read `specialists.manifest.yaml` and persist your enabled specialist ids (see onboarding § What happens after selection).
4. Configure your **Chief UX Designer** agent with `chief-ux-designer/SKILL.md`.
5. Register each enabled specialist’s primary skill and listed sub-skills.

## Adding a new specialist

1. **Create a folder** under `specialists/<id>/` with kebab-case `id`.
2. **Author `SKILL.md`** using the same sections as existing specialists:
   - Role and when to invoke
   - Capabilities (link sub-skills)
   - Required inputs
   - Outputs / deliverables (point to `templates/`)
   - Quality criteria
   - Handoff to Chief UX Designer
3. **Add sub-skills** under `specialists/<id>/skills/<capability>/SKILL.md` for distinct jobs.
4. **Register** in `specialists.manifest.yaml`:
   - `id`, `name`, `description`, `suggested`, `default_enabled`, `skill_path`, `sub_skills`
5. **Update this README** specialist table.
6. **Extend Chief skill** — Add the role to briefing templates and reconciliation rules in `chief-ux-designer/SKILL.md` if the new role affects conflict patterns.

## License

Add a license file when you publish; skills are intended to be copied and adapted in your own agent setups.
