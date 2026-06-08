# FreshDirect ordering

The "smart" approach: **Claude drives a real browser live** using the Playwright MCP server.
There is no fixed script — Claude reads each page, decides what to do, and acts step by step,
so it can judge which search result is the *right* product. Checkout always stays manual.

## One-time setup
1. **Node.js** must be installed (provides `npx`). Check with `node --version`.
2. The Playwright MCP server is configured in the repo's `.mcp.json` and uses a **persistent
   browser profile** at `freshdirect/browser-profile/` so your FreshDirect login survives
   between sessions. (That folder is gitignored — it holds login cookies, never commit it.)
3. Approve the `playwright` MCP server when Claude Code prompts on first use.
4. **Log in once:** the first time, a browser window opens; sign into FreshDirect manually.
   The session cookie persists in the profile for future runs.

## Procedure (what Claude does when you say "build my FreshDirect cart")
1. Read the current week file's grocery list (`weeks/<latest>.md`).
2. For each item:
   - Check `shopping/fd-catalog.md`. If it's a **known product**, navigate straight to it.
   - If **unknown**, search FreshDirect, read the results, and pick the genuinely correct
     product (right thing, sane size for one person) — not just the first hit. When unsure
     between options, ask the user.
   - Add to cart. For any new product, **record it in `shopping/fd-catalog.md`.**
3. Write the resulting cart to `freshdirect/order.md` (items, products, est. quantities).
4. **STOP at the filled cart.** Do not check out. Hand back to the user for delivery window,
   payment, and placing the order.

## Delivery notes (from FreshDirect)
- Delivers locally; same-day/next-day windows.
- **You must be present by default** unless you enable *Unattended Delivery* (then they leave
  it at the door/lobby). For meat/dairy/frozen/seafood, pick a window you'll be home for.
- Alcohol always requires someone 21+ with ID; it can't be left unattended.
- Bags are free to keep. Trucks are refrigerated; frozen kept with dry ice; they don't use ice packs.

## Timing & promo notes (learned)
- **Order ~3+ days before the cooking week starts.** Delivery slots can be several days out —
  the 2026-06-14 order was placed for a Monday start but the earliest slot was Wednesday 6/17,
  which pushed cooking to Wed/Thu. When planning, factor in the lead time.
- **"$50 off / NEW50"-type promos are first-order only.** Don't plan a cart around hitting the
  $99 minimum on later orders — it won't apply.

## Caveats / when it breaks
- **Login expiry / captcha:** if FreshDirect logs you out or shows a captcha, just complete it
  in the open window, then tell Claude to continue.
- **Site changes:** FreshDirect can change their layout; since Claude drives live (not a fixed
  script) it adapts, but occasionally a step needs a second try.
- **Product matching:** the catalog makes this better every week. Early orders need more of
  your input on which product is right.
