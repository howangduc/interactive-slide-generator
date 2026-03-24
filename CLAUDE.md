# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Savyu-Slide is a workspace for creating browser-based presentation slide decks. Each slide deck is a standalone React + Vite app living in its own subfolder under `Slides/`.

## Project Structure

```
Savyu-Slide/
├── Slides/              # All slide deck projects live here
│   ├── my-deck-1/       # Each deck is a standalone React+Vite app
│   ├── my-deck-2/
│   └── ...
├── .agents/skills/slide-deck/   # Slide deck skill (SKILL.md + slide-guidelines.md)
├── .claude/skills/              # Symlinked skills
└── CLAUDE.md
```

## Creating a New Slide Deck

Use `/new-slides` to start a new project. This navigates into `Slides/` and scaffolds a new deck.

Each deck uses this tech stack:
- **Build:** Vite
- **Framework:** React 18+ with TypeScript
- **Animation:** Framer Motion (`framer-motion` — **NOT** `motion/react`, which doesn't exist in v12+)
- **Styling:** Tailwind CSS v4
- **Charts:** Recharts (when needed)
- **Icons:** Lucide React (when needed)

## Build & Dev Commands (per deck)

```bash
cd Slides/<deck-name>
npm install
npm run dev          # Start dev server
npx tsc --noEmit     # Type check
npx vite build       # Production build
```

## Key Architecture Conventions

### Slide Container
- Fixed **1280x720px** container scaled via CSS `transform: scale()` to fit viewport
- All content authored at 1280x720, uniformly scaled (like reveal.js)
- `SlideLayout` component handles scaling + centering

### Tailwind + Scaling Gotcha
Because of transform scaling, Tailwind's rem-based spacing appears smaller on screen. For elements with visible backgrounds (cards, chips, buttons), use **inline `style={{}}` with px values** instead of Tailwind padding classes.

### Typography
- All font sizes **must use `clamp(min, preferred, max)`** — never fixed px/rem
- Max 2 font families per deck, loaded from Google Fonts or Fontshare
- Never center-align body paragraphs

### Content Density
- Max 60% of slide area should contain content
- Every slide must fit within 1280x720 — no overflow, no scrolling
- If content overflows, split into multiple slides

### Visual Rules
- No text wrapped in background cards — text sits directly on slide background
- No nested backgrounds (box inside box)
- Borders must be subtle: `border-white/10`, `border-muted/20`
- Backgrounds should have depth (layered gradients), not flat solid colors

### Navigation
- Keyboard: Right/Space/Enter = next, Left = previous
- Click: right half = next, left half = previous
- Progress bar at bottom + slide counter in bottom-right

### Animation
- Framer Motion with `AnimatePresence mode="wait"` for transitions
- Default duration: 0.4–0.6s, easing: `[0.25, 0.1, 0.25, 1]`
- Stagger children by 0.08–0.12s
- Always support `prefers-reduced-motion`

## Content Structure (Training Decks)

Follow the learning cycle from `slide-guidelines.md`:
**Problem → Discussion → Concept → Example → Takeaway**

Target ratio: 60-70% visual slides, 10-15% charts/diagrams, 15-20% text.

## Workflow

1. Ask user for mood and content topic before coding any slides
2. Suggest 2-3 style presets based on mood (see SKILL.md for preset table)
3. Scaffold app with chosen preset's theme + shared components (SectionDivider, CodeBlock)
4. Create `CONTENT.md` in project root — user's content editing surface
5. Start dev server in background for live preview
6. For 10+ slides: use **parallel Agent calls** (3-4 agents building slide batches simultaneously)
7. Wire up `slides/index.ts` and verify build
8. **Visualization pass**: review slides for text-heavy content, suggest visual upgrades (charts, gauges, diagrams, progressive reveal, CountUp animations)
9. Always keep the app in a runnable state — no broken imports

## Visualization-First Principle

Always prefer visuals over text:
- Tables with numbers → Recharts charts
- Percentages → SVG ring gauges
- Comparisons → before/after bars or auto-flipping cards
- Processes → step-by-step progressive reveal
- Statistics → CountUp hero numbers
- Code → TypewriterCode reveal
- Decisions → visual spectrum diagrams

## Quality Checks Before Delivering

- `npm run dev` starts without errors
- `npx tsc --noEmit` passes
- `npx vite build` succeeds
- No placeholder text, no content overflow
- All font sizes use `clamp()`, all backgrounds have depth
