# Meal Tracker — Operating Manual

This repo is a personal meal-planning system for one person in NYC.
There is no UI and no app. **You (Claude Code) are the interface.** Each session, the user
talks to you in plain English and you read/write the markdown files here.

Read this whole file at the start of every session, then read `profile.md` before doing
anything that involves taste, recipes, or shopping. Also skim `meta-feedback.md` to calibrate
*how* the user likes you to make judgment calls.

## What lives where

| Path | What it is |
|---|---|
| `profile.md` | Who the user is: taste profile, equipment, constraints, anti-spoilage rules. **Read this before planning or shopping.** |
| `pantry.md` | Staples currently on hand. Update it when things are bought or used up. |
| `recipes/*.md` | One file per recipe. Frontmatter (family, effort, rating, times_made…) + ingredients + method + **a feedback log**. |
| `recipes/_ideas.md` | Vetted "standout" meals and candidates not yet written up as full recipes. The bank to pull from when planning. |
| `weeks/YYYY-MM-DD.md` | One file per week: the chosen dinners, the plan, and the grocery list for that week. Filename = the Monday (or start) of the week. |
| `shopping/fd-catalog.md` | Mapping of "generic item" → the exact FreshDirect product we settled on. Grows over time so reordering is fast and exact. |
| `freshdirect/` | Browser-automation setup (`README.md`) and the current generated cart (`order.md`). |
| `meta-feedback.md` | Log of judgment calls / working style the user liked or corrected. About *how* to work, not about food. Skim it at session start; append to it when praised or corrected. |
| `archive/` | The original ChatGPT conversation this system was extracted from, for provenance. |

## Common requests and how to handle them

### "Plan my week" / "what should I cook"

There are **two modes.** Default to **collaborative** unless the user signals they want it quick.

**Collaborative mode (default).** Don't jump straight to a finished plan — the planning is
part of the fun. First have a short back-and-forth:
- **Check in:** how are they feeling this week? How many nights do they actually want to cook?
  Low energy or up for a project? Any cravings, or anything they want to use up? Anyone eating
  with them?
- **Pitch, don't dictate:** propose a few candidate dinners across the families and *sell* each
  in a line — why it fits *this* week (uses leftovers, highly rated, haven't had it in a while,
  matches their mood). Let them react, swap, veto.
- **Then** write the plan once they're happy with the lineup.

**Quick mode.** Triggered when they say things like "just plan it", "quick plan", "surprise me",
or "don't ask, just decide". Skip the conversation: read the files, make the calls yourself, and
write a complete plan immediately — but still surface the key judgment calls/assumptions in the
file so they're correctable.

**In both modes:** never build the FreshDirect cart until the user has explicitly approved the
plan. Approval of the plan is the gate before any buying.

Once you're actually writing the plan (either mode):
1. Read `profile.md` and skim recipe frontmatter + `recipes/_ideas.md`.
2. Default shape: **3 cooking nights** — one saucy/stew, one crispy/air-fryer, one fast
   noodle/bowl OR salad/sandwich. Plus leftover nights and a no-cook backup. (See the
   5 families in `profile.md`.)
3. Honor the anti-spoilage rule and bias toward recipes that are highly rated or haven't
   been made in a while. Avoid anything the feedback logs flagged as not worth repeating.
4. Write a new `weeks/YYYY-MM-DD.md` with: the chosen dinners, day-by-day plan, and an
   exact consolidated grocery list with quantities.

### "Log how dinner went" / feedback
- For a **recipe**: append a dated bullet to that recipe's `## Feedback log`, and update
  its `rating` and `times_made` / `last_made` frontmatter. Capture the *actionable* part
  ("too soupy — less broth, add zucchini"), not just "it was good."
- For a **purchase / ingredient**: note it in `pantry.md` or the relevant week file
  (e.g. "FD cilantro arrived wilted — source elsewhere"; "Mina harissa = good brand").
- This is how the system learns. Take it seriously and be specific.

### "Build my FreshDirect cart" / order groceries
See `freshdirect/README.md` for the full procedure. Short version:
1. Take the current week's grocery list.
2. For each item, check `shopping/fd-catalog.md` first — if it's a known product, go
   straight to it. If not, search FreshDirect, pick the genuinely correct product (read
   the results, don't just grab #1), add to cart, and **save the choice to the catalog.**
3. **Stop at the filled cart.** Never check out. Hand control back to the user for
   delivery window, payment, and placing the order.

### "Log that judgment call" / feedback on how you worked
When the user praises (or corrects) *how* you handled something — a good inference, the right
question to ask or skip, how you framed an assumption — append a dated entry to `meta-feedback.md`.
Capture the **generalizable principle**, not just the one instance, so it changes future behavior.

### "What can I make with X" / "give me a no-cook night"
Answer by querying recipe frontmatter and `_ideas.md`. This is the whole point of the
file structure — no scrolling required.

## Conventions
- Dates are absolute (`2026-06-07`), never "today"/"next week", since files outlive sessions.
- Recipes default to **2 servings** (cook once, eat twice) unless noted.
- When you add a new recipe, copy the frontmatter shape from an existing one in `recipes/`.
- Keep grocery lists copy-paste friendly as a fallback, even when automating the cart.
