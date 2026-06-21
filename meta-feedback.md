# Meta-feedback — how the user likes Claude to work

This is **not about food.** It's a log of judgment calls (and working style) the user
appreciated, so future sessions can calibrate *how* to operate, not just *what* to cook.

Skim this at the start of a session. When the user praises a call you made — or corrects
one — add a dated entry. Capture the **generalizable principle**, not just the one instance,
so it actually changes future behavior.

Format:
```
- YYYY-MM-DD — <the call you made>. **Principle:** <the rule to generalize>.
```

## Log

- 2026-06-07 — Inferred recipe ratings (noodles 5, others 4) from a qualitative comment
  ("all really good but noodles were my favorite") instead of asking him to assign numbers.
  **Principle:** Translate qualitative feedback into the structured fields the system needs;
  don't make the user do bookkeeping. State the inference so it's correctable.

- 2026-06-07 — Filled in cook dates (Mon/Wed/Fri of the week) from the existing plan rather
  than stopping to ask which days he cooked.
  **Principle:** When a detail is reasonably implied by existing files, fill it from there and
  move on; reserve questions for things that genuinely can't be inferred.

- 2026-06-07 — On "used up pretty much everything," distinguished perishables (used) from
  durable jars/oils/dry goods (carried over) rather than blindly marking all staples gone —
  and flagged each assumption for quick correction.
  **Principle:** Apply real-world common sense to ambiguous statements (a bottle of soy sauce
  isn't emptied in a week), and surface the assumptions explicitly so they're cheap to fix.
  Proactive-but-transparent beats either asking everything or silently guessing.

- 2026-06-14 — **Correction.** Filled the FreshDirect cart in one shot, then showed him what
  was bought. He'd rather see the **proposed buy list before the cart fills** (and it belongs in
  `order.md`). Also auto-bought broccoli/jalapeños/garlic he already had.
  **Principle:** For steps that spend money or are tedious to undo, propose-then-execute: show
  the concrete list for a quick yes before acting, don't act-then-report. Same spirit as plan
  approval gating the buy. And cross-check `pantry.md` before adding staples — durable items
  (garlic, jarred peppers, oils) are probably already on hand; default to *not* rebuying them.

- 2026-06-13 — **Correction.** When asked to "plan next week," jumped straight to a finished
  plan. He'd have preferred a collaborative lead-in: check how he's feeling that week and *sell*
  him on the dinner options before committing. Led to adding two planning modes in CLAUDE.md.
  **Principle:** Planning is a moment to engage, not just produce. Default to collaborating —
  check in on mood/energy/cravings and pitch options with a why — and reserve "just produce it"
  for when he explicitly asks for speed. Distinguish work that's *transactional* (logging,
  pantry math — be efficient) from work that's *a decision he enjoys making* (what to eat —
  bring him into it). Approval still gates the buying step in both modes.
