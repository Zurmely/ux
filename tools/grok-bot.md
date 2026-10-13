# Grok Bot tool catalog for the UX team

This is the tool surface the UX agents can use when running on **Grok Bot**. Each specialist's `SKILL.md` has a **Tools** section that picks from this list, and an **Activities** section that says which tool to call at each step.

Tools are written as `Namespace.tool_name`. The namespace is the MCP server or built-in toolset that hosts the tool.

## Connection status

Check what's connected before you plan any work. Use the host's tool discovery (for example `GetDynamicTools`).

| Namespace | Status on Grok Bot | Used by |
| --- | --- | --- |
| `figma` | Ready (Figma MCP) | All design specialists |
| `Google-drive` | Ready | All, since Drive is where docs live |
| `Google-slides` | Ready | Chief, Researcher, Accessibility (`check_contrast`) |
| `Notion` | Ready | Chief, Researcher, Writer |
| `Gmail` | Ready | Chief, Researcher |
| `Github` | Ready | Chief, UI Designer, Accessibility |
| `X` | Ready (public reads are built in) | Researcher, Writer |
| `cursor` (built-in) | Ready | All (`WebSearch`, `WebFetch`, `Task`, `TodoWrite`, `GenerateImage`) |
| `cursor-subscriptions` | Ready | Chief |
| `Slack` | **Needs auth.** Authenticate it in the Cursor desktop app before use | Chief (optional) |
| `Cloudflare-*` | Not relevant to UX work | None |

If a namespace a specialist relies on is missing or not authenticated, the specialist should **say so in its handoff packet** and fall back to Drive or a markdown deliverable. It must not invent tool output.

## Mandatory skill prerequisites

Some tools fail in confusing ways unless you load their skill first. These rules aren't optional.

| Before calling | Load skill |
| --- | --- |
| `figma.use_figma` | `figma-use` (plus `figma-use-figjam` on FigJam boards, `figma-use-slides` in Figma Slides, `figma-use-motion` for animation) |
| `figma.get_design_context` | `figma-design-to-code` |
| `figma.create_new_file` | `figma-create-new-file` |
| `figma.generate_diagram` | `figma-generate-diagram` |
| `figma.create_shader` / `update_shader` | `figma-shaders` |
| `figma.create_generative_plugin` / `update_generative_plugin` | `figma-generative-plugins` |
| Translating a page or layout into Figma | `figma-generate-design` |
| Building a library, tokens, or variables from code | `figma-generate-library` |
| Code Connect mapping | `figma-code-connect` |
| Implementing Figma motion in code | `figma-implement-motion` |
| Any `X.*` tool | `x-api-mcp-guide` |

**Figma session rule:** once you know the file key, call `figma.create_session` before any other Figma file tool, including read-only ones. Pass the returned `sessionId` on every later Figma call for the task.

## Tool reference by job

### Figma: read

| Tool | Use it to |
| --- | --- |
| `figma.get_design_context` | Get the primary read of a node: reference code, a screenshot, and metadata |
| `figma.get_screenshot` | Capture a visual of a node, FigJam board, or Slides page |
| `figma.get_metadata` | Get a structural XML overview (layer names, hierarchy) |
| `figma.get_variable_defs` | Get the tokens and variables bound to a node (colors, type, spacing) |
| `figma.get_motion_context` | Get keyframes, easing, and generated CSS or motion.dev snippets |
| `figma.get_figjam` | Read FigJam boards (affinity maps, journeys) |
| `figma.get_libraries` | List subscribed and available libraries |
| `figma.search_design_system` | Find components, variables, and styles to reuse |
| `figma.download_assets` | Export renders, source images, and SVGs of a node |
| `figma.list_file_shaders` | List the shader effects and fills used in a file |
| `figma.whoami` | Get the user's plans, which you need as `planKey` for paid generation |

### Figma: write

| Tool | Use it to |
| --- | --- |
| `figma.create_new_file` | Create a blank Design, FigJam, or Slides file |
| `figma.use_figma` | Make any edit through the Plugin API: frames, components, variables, text, prototype reactions, annotations |
| `figma.generate_figma_design` | Capture a live web page by URL into a file, for audits or redesign baselines |
| `figma.html_to_figma` | Convert static HTML into plain layers (no design-system bindings) |
| `figma.generate_diagram` | Generate a Mermaid flowchart, sequence, state, or Gantt chart in FigJam |
| `figma.upload_assets` | Upload images or SVGs into a file |
| `figma.export_video` | Export a timeline node as an MP4 |
| `figma.generate_image` | Generate a raster image. **Paid**: uses Figma AI credits and needs `planKey` |
| `figma.weave_find_model` / `weave_run_model` / `weave_get_model_run_output` | Run a named Weave AI model on images or video |
| `figma.weave_list_tools` / `weave_run_tool` / `weave_get_tool_run_output` | Run a published Weave workflow |
| `figma.create_shader` / `update_shader` / `list_shaders` / `get_shader` | Author shader effects and fills |
| `figma.get_code_connect_map` / `get_code_connect_suggestions` / `send_code_connect_mappings` / `add_code_connect_map` | Map components to code |
| `figma.get_context_for_code_connect` / `list_file_components_for_code_connect` | Get component props, variants, and the published-component graph |

### Docs, research, and communication

| Tool | Use it to |
| --- | --- |
| `Google-drive.search_files` / `list_recent_files` | Find briefs, research, and brand docs |
| `Google-drive.read_file_content` | Read a doc, optionally with its comments |
| `Google-drive.create_file` | Create a deliverable (copy deck, spec, report) |
| `Google-drive.update_file` | Rename, move, or edit file metadata |
| `Google-drive.copy_file` | Start a doc from a template |
| `Google-drive.share_file` / `get_file_permissions` | Share deliverables (only on request) |
| `Google-drive.download_file_content` | Export a doc or sheet |
| `Google-slides.create_presentation` / `compose_slide` / `add_slide` / `insert_*` / `get_slide_thumbnail` | Build readouts and design reviews |
| `Google-slides.check_contrast` | Compute WCAG contrast for hex pairs, with the nearest passing color if a pair fails. This is a pure calculation, so it works for any UI colors, not only slides |
| `Notion.notion-search` / `notion-fetch` | Find workspace context and specs |
| `Notion.notion-query-meeting-notes` | Pull interview and stakeholder meeting notes |
| `Notion.notion-create-pages` / `notion-update-page` / `notion-create-database` | Publish decision logs, research repos, and glossaries |
| `Notion.notion-create-comment` / `notion-get-comments` | Run review threads on specs |
| `Gmail.search_threads` / `get_thread` | Mine feedback and support threads |
| `Gmail.create_draft` | Draft recruiting or stakeholder emails. **Draft only.** Send only after the user approves |
| `Github.search_issues` / `list_issues` / `issue_read` | Mine bug and feedback themes |
| `Github.issue_write` / `sub_issue_write` | File remediation or handoff tickets (on request) |
| `Github.get_file_contents` / `search_code` | Read implemented UI, tokens, and copy strings |

### Web and social

| Tool | Use it to |
| --- | --- |
| `cursor.WebSearch` | Do competitive research, look up standards, find patterns |
| `cursor.WebFetch` | Read a specific URL (WCAG understanding docs, competitor pages) |
| `X.search_posts_all` / `get_posts_counts_recent` | Do social listening on user language and pain points, and measure volume |
| `X.search_news` / `get_news` / `get_trends_by_woeid` | Read market and trend context |
| `X.search_users` / `get_users_posts` | Find and read public accounts (competitors, communities) |

Public X reads are **built into Grok Bot**. They don't need an X connection and don't spend the user's credits. Account-level X tools (timeline, bookmarks, Chat) need the user's X connection. **Posting to X isn't supported.**

### Orchestration (Chief only)

| Tool | Use it to |
| --- | --- |
| `cursor.Task` | Launch a specialist as a subagent with its brief. Run independent specialists in parallel |
| `cursor.TodoWrite` | Track the engagement plan and each specialist's status |
| `cursor-subscriptions.subscribe_timer` | Schedule a check-in or follow-up |
| `cursor-subscriptions.subscribe_github_pr` | Wait for an eng PR that implements the handoff |
| `cursor-subscriptions.subscribe_slack_thread` / `subscribe_slack_channel` | Wait for stakeholder feedback (needs Slack auth) |

### Image generation

| Tool | When |
| --- | --- |
| `figma.generate_image` | Use for illustration concepts that land in Figma. **Paid.** Confirm `planKey` and get user consent first |
| `cursor.GenerateImage` | Use **only when the user explicitly asks for an image**. Never use it for decoration |
| `figma.weave_run_model` | Use for a specific named model or image-to-image work |

## Safety rules for every agent

1. **Read before you write.** Inspect the Figma file or Drive folder before editing it.
2. **Get approval before any outward action.** Sending email, sharing files, filing GitHub issues, and spending paid credits (Figma AI, Weave, X account tools) all need explicit user approval.
3. **Don't fabricate.** If a tool is unavailable, record "not run, tool unavailable" in the handoff packet.
4. **Link, don't paste.** Handoff packets reference Figma node URLs and Drive file links.
5. **Protect PII.** Research notes from Gmail, Notion, or X go into restricted Drive files. Summaries carry no personal identifiers.
