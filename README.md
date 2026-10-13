# UX Agent Skills

A **library of agent skills** for a multi-agent UX team. A **Chief UX Designer** orchestrates specialist agents; each specialist owns a slice of the experience and returns structured outputs the Chief reconciles into a final deliverable.

Design work happens in **Figma**. Research, briefs, and decision logs live in **Google Drive**. The skills target **Grok Bot**: every specialist lists the exact Grok Bot tools it uses and maps them to concrete activities (see `tools/grok-bot.md`). On another host, swap in equivalent tools.

## Tools by specialist (Grok Bot)

| Specialist | Core tools |
| --- | --- |
| Chief UX Designer | `cursor.Task` (dispatch specialists), `TodoWrite`, Drive, Notion, Figma index, Slides review deck, GitHub handoff issues, `cursor-subscriptions` |
| UX Writer | Figma read + `use_figma` text edits, Drive copy deck, Notion glossary, X vocabulary search, GitHub string files |
| Motion Designer | `get_motion_context`, `use_figma` with `figma-use-motion`, `export_video`, Drive spec |
| Illustrator | `search_design_system`, `use_figma` vectors, `generate_image` / Weave (paid), shaders, `upload_assets` / `download_assets` |
| UI Designer | `create_session`, `search_design_system`, `use_figma`, `generate_figma_design`, `generate_diagram`, Code Connect, GitHub component reads |
| UX Researcher | Drive, Notion meeting notes, Gmail feedback threads, GitHub issues, X social listening, WebSearch, FigJam affinity and journey maps, Slides readout |
| Accessibility Specialist | `get_variable_defs` + `Google-slides.check_contrast`, `get_design_context`, `get_motion_context`, annotations via `use_figma`, WebFetch for WCAG, GitHub remediation issues |

Outward actions (sending email, sharing files, filing issues, paid generation) always need the user's approval.

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
├── specialists.manifest.yaml    # Registry, defaults, tools, activities
├── tools/
│   └── grok-bot.md              # Grok Bot tool catalog, prerequisites, safety rules
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
3. Read `specialists.manifest.yaml`, run the **tool readiness check** against your Grok Bot connections, and save the enabled specialist ids (see the onboarding skill).
4. Configure your **Chief UX Designer** agent with `chief-ux-designer/SKILL.md`.
5. Register each enabled specialist’s primary skill and listed sub-skills.

## Adding a new specialist

1. **Create a folder** under `specialists/<id>/` with kebab-case `id`.
2. **Author `SKILL.md`** using the same sections as existing specialists:
   - Role and when to invoke
   - Capabilities (link sub-skills)
   - Required inputs
   - Outputs / deliverables (point to `templates/`)
   - **Tools on Grok Bot**: only tools listed in `tools/grok-bot.md`, with the required skills
   - **Activities**: numbered steps, each naming the tools it calls
   - Quality criteria
   - Handoff to Chief UX Designer
3. **Add sub-skills** under `specialists/<id>/skills/<capability>/SKILL.md` for distinct jobs.
4. **Register** in `specialists.manifest.yaml`:
   - `id`, `name`, `description`, `default_enabled`, `skill_path`, `sub_skills`
   - `tools.required`, `tools.optional`, `tools.key`, `required_skills`, `activities`
   - `paid_tools` / `approval_required` where they apply
   - If the role needs a tool that isn't in the catalog, add it to `tools/grok-bot.md` first
5. **Update this README** specialist table.
6. **Extend Chief skill** — Add the role to briefing templates and reconciliation rules in `chief-ux-designer/SKILL.md` if the new role affects conflict patterns.

## License

Add a license file when you publish; skills are intended to be copied and adapted in your own agent setups.
