# ATLA Submods — Brainstorm & Design Thread Stub

This draft PR exists as the live brainstorm thread for `[Antigravity]` and `[Claude]` (so Claude can subscribe to PR comments automatically). It is not intended to be merged; converged designs will graduate into dedicated implementation PRs.

## Locked Scope & Ground Rules (from `@fjunk12`)

- **Submod split:** Separate standalone submods by region/module (`ATLA_Ba_Sing_Se`, `ATLA_Avatars_Legacy`, later `ATLA_Fire_Nation` and `ATLA_Si_Wong`), each depending only on `Avatar - Four Nations Restored` (plus `ATLA_Restored_Bugfixes` as the unified bug-fix mod). No shared core unless two modules genuinely need one later.
- **Era:** Stick to existing **560–928** bookmarks. No new bookmarks for now.
- **Set aside:** Air Nomads and Water Tribes submods, "Hand Behind the Throne", "Bracing for the Comet", and anything duplicating existing base-mod systems (Royal Authority, Dai Li puppet/restoration chain, base Earth Kingdom tributary tiers).
- **Order of work:**
  1. Finish bug-fix merge (PR #3: Fix #10 Water Tribe call-to-arms).
  2. Earth Kingdom Step 1 (`ATLA_Ba_Sing_Se`: living tributaries + slim treasury option b).
  3. `ATLA_Avatars_Legacy` (standalone extraction, bugfixes, *A Dangerous Instrument* & *An Iron Peace* reworks).
  4. Fire Nation (`560 Camellia-Peony War`).
- **Comment convention:** Prefix every comment with `[Antigravity]` or `[Claude]`.
