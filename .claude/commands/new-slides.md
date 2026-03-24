You are starting a new slide deck project. Follow these steps:

1. Ask the user for a **project name** (folder name for this deck) if not provided as argument: $ARGUMENTS
2. Ask the user for the presentation **mood** and **content/topic**
3. Create the project folder inside `Slides/` (e.g., `Slides/<project-name>/`)
4. Invoke the `/slide-deck` skill to scaffold and build the presentation

The `Slides/` folder is at the root of this workspace. All new slide deck projects MUST be created inside it.

## Workflow After Folder Creation

1. **Suggest 2-3 style presets** based on the user's mood — let them choose
2. **Scaffold the app** — Vite + React + Tailwind + Framer Motion + theme + shared components
3. **Create `CONTENT.md`** — a structured markdown template in the project root for the user to paste slide content into. Use `## Slide N: Title` headings as a guide. This is the user's content editing surface.
4. **Start dev server** (`npx vite --host`) in background so the user can preview immediately
5. **Build slides from content** — once the user pastes content into `CONTENT.md`, build all slides:
   - For decks with **10+ slides**, use **parallel Agent tool calls** to build batches simultaneously (e.g., 3-4 agents building 5-8 slides each)
   - For smaller decks, build sequentially in batches of 5-10
6. **Wire up `slides/index.ts`** with all slide imports and verify build (`tsc --noEmit` + `vite build`)
7. **Review & enhance** — after first pass, review for slides that are too text-heavy and suggest visualization upgrades (charts, gauges, diagrams, progressive reveal)

## Content-to-Slide Mapping

When the user provides content (via CONTENT.md or chat), analyze each slide and choose the best visual approach:

| Content Type | Visual Approach |
|---|---|
| Statistics / numbers | CountUp animation with hero stat display |
| Comparisons (good/bad, before/after) | Animated flip or side-by-side with bars |
| Processes / flows | Step-by-step progressive reveal (auto-advance) |
| Tables with 2-3 columns | Keep as styled table |
| Tables comparing quantities | Recharts bar/area chart |
| Percentages / scores | SVG ring gauges with animated fill |
| Code examples | TypewriterCode with blinking cursor |
| Hierarchies / taxonomies | Category grid with icon badges |
| Decision frameworks | Visual spectrum or flow diagram |
| Section transitions | SectionDivider component (phase, title, timeline) |

Always prefer visualization over raw text. A chart > a table. A gauge > a number. A diagram > a bullet list.
