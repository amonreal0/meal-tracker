# 🥘 Meal Tracker

A personal meal-planning system for one person — with **no app and no UI**. Instead of a
website, the "interface" is [Claude Code](https://claude.com/claude-code): you open a session,
talk in plain English, and Claude reads and writes the markdown files in this repo to plan
your week, track recipes, log feedback, and even fill your grocery cart.

It started as a single long ChatGPT conversation about what to cook (preserved in `archive/`),
which kept getting lost in scroll. This repo turns that into a structured, durable system that
learns your tastes over time.

## How it works

```
You ──talk──▶ Claude Code ──reads/writes──▶ markdown files in this repo
```

Every session, Claude reads `CLAUDE.md` (the operating manual) to learn how the system works,
then helps with whatever you ask:

- **"Plan my week"** — Claude checks in on how you're feeling, pitches dinners across your
  5 dinner "families," then writes a plan + an exact grocery list.
- **"Log how dinner went"** — feedback gets appended to that recipe's log, and its rating
  updates. This is how the system learns.
- **"Build my FreshDirect cart"** — Claude drives a real browser to fill your cart, then
  stops before checkout for you to review and pay.
- **"What can I make with X?" / "give me a no-cook night"** — answered by querying the recipes.

## Repository structure

| Path | What it is |
|---|---|
| `CLAUDE.md` | Operating manual — how a Claude session should use this repo. |
| `profile.md` | Taste profile, equipment, constraints, anti-spoilage rules. |
| `pantry.md` | Staples currently on hand. |
| `recipes/` | One file per recipe: frontmatter + ingredients + method + a feedback log. |
| `recipes/_ideas.md` | Vetted "standout" meals and candidates to pull from when planning. |
| `weeks/` | One file per week: chosen dinners, day-by-day plan, and grocery list. |
| `shopping/fd-catalog.md` | Mapping of generic item → the exact FreshDirect product chosen. |
| `freshdirect/` | Browser-automation setup and the current generated cart. |
| `meta-feedback.md` | Notes on *how* the user likes Claude to work (style, judgment calls). |
| `archive/` | The original ChatGPT conversation, for provenance. |

## Setup

1. Install [Claude Code](https://claude.com/claude-code) and open this folder in a session.
2. For grocery automation, you'll need [Node.js](https://nodejs.org) (for the Playwright
   browser MCP, configured in `.mcp.json`). Approve the `playwright` server when prompted,
   then sign into FreshDirect once in the browser window — see `freshdirect/README.md`.

## Privacy / git notes

- `.gitignore` excludes `freshdirect/browser-profile/` (holds login cookies — **never
  committed**) and `.playwright-mcp/` (transient automation dumps).
- This is a personal repo: it contains one person's food preferences and meal history, not
  secrets — but the browser profile would be sensitive, hence the gitignore.

## Conventions

- Dates are absolute (`2026-06-14`), since files outlive sessions.
- Recipes default to **2 servings** (cook once, eat twice).
- Grocery lists stay copy-paste friendly even when the cart is automated.
