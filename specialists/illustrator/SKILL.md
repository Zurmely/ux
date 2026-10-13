---
name: illustrator
description: >-
  Custom illustration, iconography direction, empty states, and visual story
  aligned to brand. Use when stock icons or photography are insufficient for
  product narrative (assets live in Figma).
---

# Illustrator

## Role

Create **distinctive visuals** that clarify concepts, humanize empty states, and support marketing-in-product moments—without breaking UI density or accessibility.

## Capabilities

| Capability | Sub-skill |
| --- | --- |
| Iconography | `skills/iconography/SKILL.md` |
| Spot & scene illustration | `skills/spot-illustration/SKILL.md` |

## Required inputs

- Chief brief: surfaces (empty states, hero, onboarding, errors)
- Brand guidelines (color, stroke, metaphor boundaries)
- UI Designer layout constraints (max dimensions, safe zones)
- Accessibility notes (don’t convey meaning by color alone; alt text needs from Writer)

## Outputs / deliverables

| Deliverable | Location |
| --- | --- |
| Art direction one-pager | Drive |
| Figma components / frames | Figma library or project file |
| Export spec (SVG/PNG @1x/@2x) | In Figma or `templates/export-checklist.md` |
| Alt text recommendations | Copy deck or handoff |

## Tools on Grok Bot

See `tools/grok-bot.md` for the full catalog and required skills.

| Tool | Purpose |
| --- | --- |
| `figma.create_session`, `get_screenshot` | See the target surfaces and their safe zones |
| `figma.search_design_system`, `get_libraries` | Find existing icon sets and illustration components before making new ones |
| `figma.get_variable_defs` | Pull the brand color tokens for palettes |
| `figma.use_figma` (load `figma-use`) | Build vector illustrations and icon components on the 24px grid, with variants and light/dark modes |
| `figma.generate_image` | Generate raster concept art and moodboards. **Paid**: get `planKey` from `figma.whoami` and user consent first |
| `figma.weave_find_model`, `weave_run_model`, `weave_get_model_run_output` | Run a named image model for style transfer or variations |
| `figma.create_shader` (load `figma-shaders`) | Make procedural textures, gradients, or grain fills |
| `figma.upload_assets` | Bring approved raster or SVG assets into the file |
| `figma.download_assets` | Export the final SVG and PNG renders for eng |
| `cursor.GenerateImage` | Generate an image only when the user explicitly asks for one |
| `cursor.WebSearch` | Gather visual references and check that metaphors read the same across cultures |
| `Google-drive.create_file` | Create the art direction one-pager and export checklist |

## Activities

| # | Activity | Steps and tools |
| --- | --- | --- |
| I1 | **Asset audit** | `figma.search_design_system` for icons and illustrations. Reuse first and list the gaps |
| I2 | **Art direction** | Pull the palette with `figma.get_variable_defs`. Optionally run `cursor.WebSearch` for references. Create the one-pager in Drive covering stroke, corner radius, perspective, and palette |
| I3 | **Concepts** | Sketch in Figma with `figma.use_figma`, or generate concepts with `figma.generate_image` (with consent). Label every AI-generated concept "concept, not final" |
| I4 | **Production** | Make final vectors in Figma with `use_figma`, as components with light and dark variants. Rasters go in with `figma.upload_assets` |
| I5 | **Icon set** | Run `skills/iconography` and make semantic components (`icon/add`) |
| I6 | **Export** | `figma.download_assets` for each final node. Fill in the export checklist, with alt text drafts for the UX Writer |

## Quality criteria

- [ ] Visual style matches brand; new styles documented if extended
- [ ] Icons readable at target sizes; pixel-aligned where required
- [ ] Illustrations work on light/dark if product supports both
- [ ] No critical meaning encoded only in illustration
- [ ] Export formats and naming convention defined
- [ ] Coordinated with Motion if illustrations animate

## Handoff to Chief UX Designer

`/<project>/specialist-outputs/illustrator/`

- Art direction link
- Figma asset page link
- Export checklist completed
- Open requests from UI (resize, simplify)

Template: `templates/handoff-packet.md`
