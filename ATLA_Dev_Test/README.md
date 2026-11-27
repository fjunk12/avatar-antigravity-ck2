# ATLA Dev Test (testing only)

A test-only submod for `ATLA_Ba_Sing_Se` and `ATLA_Avatars_Legacy`. **Not part of the release:** keep it out of the `mods` branch and don't enable it in a real game.

Install it like the other submods, together with the main mod, `ATLA_Ba_Sing_Se` and `ATLA_Avatars_Legacy` (it calls their scripted effects). It overrides no file and uses the prefix `atxd_`.

Open **Dev Test Menu** in the Intrigue tab (players only):

| Button | Who | What it does |
|---|---|---|
| Test: Status | anyone | Royal Authority, unity law tier, treasury, last year's income, tributaries and how many are out of reach, puppet or restored, active burdens |
| Test: Strong Earth King | Earth King | Restored, non-puppet king under the States law. It sets `earthking_in_power` as the base restoration does, so the base `earthking.1` doesn't give the puppet trait back. It fires the base law event `earthking.61`, which makes Earth realms tributaries. A day later: Royal Authority 65, treasury +250 |
| Test: Toggle Puppet | Earth King | Switches between puppet (the Grand Secretariat spends and answers pleas) and restored |
| Test: Cycle Royal Authority | anyone | 20 → 45 → 70 → 20 (the three plea bands) |
| Test: Treasury +200 | anyone | Adds 200 to the treasury (cap 1,000) |
| Test: Run Ba Sing Se Year | any ruler | Runs the yearly update now: income, works, Secretariat, reach, breakaways, AI pleas. Result in game.log |
| Test: Check the Reach | Earth King | Traces the reach and writes every Earth tributary to game.log as `connected` or `OUT OF REACH` |
| Test: Receive a Plea | Earth King | A random eligible Earth realm pleads now (no war needed). Under a puppet, the Secretariat answers |
| Test: Roll an Avatar Burden | anyone | Gives the world one of the five burdens (culture-based burdens use your culture) |
| Test: Run Legacy Year | any ruler | Runs the yearly Avatar's Legacy pulse now |

**Suggested test run** (any bookmark, playing the Earth King):
1. Strong Earth King, then wait a day and check Status.
2. Check the Reach, and compare game.log with the map.
3. Receive a Plea three times, with Cycle Royal Authority in between, to see all three bands.
4. Toggle Puppet, then Receive a Plea (the Secretariat answers), and Run Ba Sing Se Year a few times to watch the Secretariat save for the Granaries, then skim.
