# Savyu-Slide

Create beautiful, interactive slide decks that run in the browser. Powered by AI coding agents.

Unlike traditional slide tools (PowerPoint, Google Slides), Savyu-Slide generates **fully interactive presentations** — animated transitions, live charts, progressive reveals, typewriter effects, and more. Every deck is a lightweight web app you can share as a link or host anywhere.

## How It Works

1. You describe your presentation topic and mood
2. The AI agent builds an interactive slide deck for you
3. You get a live preview in your browser — edit content, request changes
4. Export as a static website and share with anyone

No design skills required. No drag-and-drop. Just describe what you want.

## Getting Started

### Requirements

- [Node.js](https://nodejs.org/) v18 or newer
- An AI coding agent CLI (e.g., Claude Code, Codex, Cursor, etc.)

### Setup

```bash
git clone https://github.com/howangduc/interactive-slide-generator.git
cd Savyu-Slide
```

That's it. No install needed at the root level.

### Create Your First Deck

Open the project with your AI coding agent, then run:

```
/new-slides
```

You'll be guided through:

1. **Name** your deck (e.g., `quarterly-review`, `product-launch`)
2. **Pick a mood** — professional, techy, playful, calm, bold, etc.
3. **Choose a visual style** from 11 built-in presets
4. **Provide your content** — paste a markdown outline or describe your slides in chat

The agent builds the entire deck, starts a live preview, and you iterate from there.

### Preview Your Deck

```bash
cd Slides/<your-deck-name>
npm install
npm run dev
```

Open **http://localhost:5173** in your browser.

**Navigate slides:** Arrow keys, Space, Enter, or click left/right halves of the screen.

## Visual Style Presets

Choose a preset when creating a deck. Each defines the full color palette, fonts, and signature design elements.

| Preset | Mood | Look |
|--------|------|------|
| **Bold Signal** | Confident | Dark, orange accent, grid layout |
| **Electric Studio** | Professional | Dark, electric blue, two-panel split |
| **Creative Voltage** | Energized | Dark, blue + neon yellow |
| **Dark Botanical** | Elegant | Dark, warm accents, serif type |
| **Neon Cyber** | Techy | Dark navy, cyan + magenta glow |
| **Terminal Green** | Hacker | Dark, green terminal aesthetic |
| **Notebook Tabs** | Organized | Light, paper card, colored tabs |
| **Pastel Geometry** | Friendly | Light, soft pastels, rounded cards |
| **Vintage Editorial** | Inspired | Light cream, geometric shapes |
| **Swiss Modern** | Minimal | White + black, red accent, grid |
| **Paper & Ink** | Editorial | Cream, crimson, serif type |

## What Makes These Slides Different

Every slide deck is a **live web app**, not a static PDF. Out of the box you get:

- **Animated transitions** between slides (fade, slide, scale)
- **Staggered content reveals** — bullets and cards animate in sequence
- **Counting-up statistics** — numbers animate from 0 to their value
- **Typewriter code blocks** — code appears character by character
- **Animated SVG gauges** — circular progress rings for percentages
- **Auto-flipping comparisons** — good/bad examples toggle automatically
- **Interactive charts** — bar charts, area charts styled to your theme
- **Progressive reveal flows** — step-by-step diagrams that auto-advance
- **Before/after bars** — animated comparison visualizations
- **Keyboard + click navigation** with progress bar

All responsive. All animated. All running at 60fps.

## Editing Your Slides

Each deck contains a `CONTENT.md` file — your content editing surface:

```markdown
## Slide 1: Title
**Title:** My Presentation
**Subtitle:** The story so far

## Slide 2: The Problem
- Users are dropping off at checkout
- Mobile conversion is 40% lower than desktop
- Average session time decreased 15% this quarter
```

Edit the markdown, then tell the agent what to update. Or just describe changes in chat:

> "Make slide 3 a bar chart instead of a table"
> "Add a section divider before slide 8"
> "The stats on slide 2 should count up with animation"

## Sharing Your Deck

### Option 1: Share the live dev link

Run `npm run dev -- --host` and share your local network URL for live demos.

### Option 2: Deploy as a static website

```bash
cd Slides/<your-deck-name>
npx vite build
```

This creates a `dist/` folder. Upload it to any static host:

**Vercel:**
```bash
npx vercel --prod
```

**Netlify:**
```bash
npx netlify deploy --prod --dir=dist
```

**GitHub Pages:**
```bash
npx vite build --base=/<repo-name>/
# Push dist/ contents to gh-pages branch
```

**Any web server:**
Just copy the `dist/` folder. It's plain HTML/CSS/JS — works everywhere.

Recipients open the link in any browser. No installs, no apps, no accounts needed.

### Option 3: Export to PDF

Open the deck in your browser and use your browser's **Print to PDF** (Ctrl+P / Cmd+P). Set paper to Landscape for best results.

## Tech Stack

Each generated deck uses:

| Layer | Technology |
|-------|-----------|
| Build | Vite |
| Framework | React 18+ with TypeScript |
| Animation | Framer Motion |
| Styling | Tailwind CSS v4 |
| Charts | Recharts |
| Icons | Lucide React |

## Project Structure

```
Savyu-Slide/
├── .agents/skills/slide-deck/   # Slide-building skill + design guidelines
├── .claude/commands/            # /new-slides command definition
├── CLAUDE.md                    # Project conventions for the AI agent
└── README.md
```

When you create a deck, it goes into a `Slides/` folder (gitignored — your decks are yours).

## Contributing

Feel free to add new style presets, improve the animation patterns, or enhance the slide-building skill. The core logic lives in:

- `.agents/skills/slide-deck/SKILL.md` — main build instructions + animation catalog
- `.agents/skills/slide-deck/slide-guidelines.md` — content structure guidelines
- `.claude/commands/new-slides.md` — the `/new-slides` command workflow

## License

MIT
