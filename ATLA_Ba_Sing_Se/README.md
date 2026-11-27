# ATLA Ba Sing Se

Earth Kingdom submod for **Avatar - Four Nations Restored** (`Rystic/ATLA-restored`). It depends only on the main mod and overrides no base file. Everything is prefixed `atxb_` (event namespace `atxb`), so it can run alongside `ATLA_Restored_Bugfixes` and `ATLA_Avatars_Legacy` (`atxl_`).

Install: copy `ATLA_Ba_Sing_Se.mod` and the `ATLA_Ba_Sing_Se/` folder into the CK2 `mod/` folder and enable it with the main mod. **Not yet tested in game.**

Design: agreed in fjunk12/avatar-antigravity-ck2#5 (Topic 1) and signed off by the owner.

## Living tributaries (v2)

The base mod already has four Earth Kingdom tributary types: outpost 10%, territory 12%, province 16% and state 20%. Each tributary adds to Royal Authority (`earthking.56`, capped at 50 while a puppet king has a regent). Tributaries come from the base mod: the unity-law events, the `pledge_to_earth_king` decision and story events. **This submod no longer makes AI realms pledge.** In lore the Earth King already counts the realms outside Ba Sing Se as his. What matters is whether the crown keeps them.

**The reach of Ba Sing Se.** Each year the crown traces which tributaries are connected to the capital:
1. It spreads out from the king's realm through bordering tributaries, up to 20 rings.
2. Island tributaries (`world_earth_islands`) count as connected while Ba Sing Se or a connected tributary holds a port.
3. Tributaries left over are **out of reach**. The overview and game.log show how many.

**Breakaways.** An AI tributary (duke or above) may break away. It uses the base decision's effect (`ATLAE.208`–`210`), and the base `earth_kingdom_reconquest` war is the crown's answer. Conditions:
- **Close to Ba Sing Se:** the crown is weak (puppet king, Royal Authority below 30, or at war below 50) **and** the tributary dislikes the king (opinion below 0).
- **Out of reach:** opinion below 25 is enough, whatever the crown's strength.
- **Odds:** 20% a year, 10% after A Single Law, and twice as likely for 10 years after the crown refused its plea. At most 2 a year.
- **Grace periods:** the first 3 years of a campaign, 5 years after a unity-law change, and 10 years after the crown answered its plea.

**Plea to Ba Sing Se.** An Earth realm (duke or above, not Way of Chin, not sandbenders, not at war with the Earth King himself) defending against a Fire Nation, Way of Chin or rebel attacker asks the crown for help. A realm can plead once every 5 years.
- **AI realms:** at most 2 pleas a year across the world.
- **Players:** use the **Plea to Ba Sing Se** decision, which doesn't count toward that cap.
- **Not a tributary deal:** a plea never makes anyone a tributary.

| Royal Authority | Gold | Host at their capital (no upkeep, disbands at peace) | Both |
|---|---|---|---|
| below 30 | 25 | 300 men (costs 30) | 55 |
| 30–59 | 40 | 600 men (costs 50) | 90 |
| 60+ | 60 | 1,000 men (costs 75) | 135 |

- **Paying:** costs come from the treasury, or from the king's own purse when the treasury can't cover them.
- **Helping:** Royal Authority +1 (+2 for both), the realm thinks better of the crown, and it won't break away for 10 years.
- **Refusing:** Royal Authority −1, −20 opinion, and twice the breakaway chance for 10 years.
- **Puppet king:** the **Grand Secretariat** answers. It turns the envoy away 3 times in 4, otherwise it sends a token host of 300. A player puppet only gets a memorandum.

## The treasury of Ba Sing Se

Tribute in CK2 goes to the Earth King's own purse. Each year a share of it moves into a crown treasury (`global_atxb_treasury`, at most 1,000):

- **Crown lands:** 10 gold, +10 at Royal Authority 30, +10 at 60.
- **Share of tribute:** per tributary, outpost 1, territory 2, province 3, state 4 gold (+25% after A Single Law).
  - Never more than 25% of the king's gold.
  - Never more than 80 a year together with the crown lands.
  - Nothing at all while the king has less than 25 gold.
- **Reporting:** every year a line starting `ATLA Ba Sing Se:` goes to game.log. The treasury overview shows the same figures.
- **Puppet king** (`trait = earthkingpuppet`): the king cannot spend the treasury. The **Grand Secretariat** does it: the holder of `d_dai_li`, or the chancellor before that title exists.
  - It first saves until the treasury covers the whole Royal Granaries (300), then builds them once, to keep the Lower Ring quiet.
  - It never builds the roads or the single law.
  - Once the Granaries stand, every year it takes a quarter of the treasury (at least 25, while the treasury has 50+) for itself.
  - A player puppet gets an "expenses of state" report.
- **Looting:** a foreign or Way of Chin ruler holding the Royal Palace takes the whole treasury.

For players, the works sit behind **Check Possible Works** in the Intrigue tab. **Return to Decisions** hides them again. The AI always sees them.

| Work | Cost | When finished |
|---|---|---|
| Royal Roads | 100, then 4 × 125 | Earth Kingdom provinces outside the Si Wong: supply +1, tax +5% |
| A Single Law for the Kingdom (needs the States or Monarchism unity law) | 200, then 3 × 200 | Royal Authority +5, breakaway chance halved, treasury share +25%, Earth tributaries −10 opinion for 20 years |
| Royal Granaries | 100, then 2 × 100 | Ba Sing Se region: tax +10%, disease defence +20% |

**Rules for works:**
- One stage is paid each year.
- If the treasury can't pay, the work stalls. Three stalls in a row abandon it, and the money spent is lost.

**Also:**
- **Draw on the Treasury:** 100 out, 50 to your purse, Royal Authority −5, every 2 years.
- **Sabotage the Crown's Works:** any independent Earth or Way of Chin realm can spend 25 gold, every 5 years. The outcome is a 45% setback, 30% nothing, or 25% caught; being caught is likelier when the king's spymaster is good and less likely with a skilled saboteur.
  - The AI only sabotages if it dislikes the king, is his rival, or follows the Way of Chin.

## Cut from the old ATLA Expanded (duplicated the base mod or added micro)

- My parallel tribute tiers.
- All yearly programmes.
- The Messenger Network, Outer Wall and Investigate the Dai Li works, and Purge the Dai Li.
- The Mandate.
- The Dai Li and resentment meters.
- Far-realm help requests.
- Bureaucracy and Borders.

## Test in game

1. **560 start, as or watching the Earth King:**
   - After the first year, open the treasury overview.
   - game.log should have an `ATLA Ba Sing Se:` line.
2. **Build a work:**
   - Start the Royal Granaries.
   - Watch the stage report the next year and the finished modifiers on Ba Sing Se provinces.
3. **Run the treasury dry during a work:** it should stall, then be abandoned after 3 years.
4. **Breakaways:**
   - Let Royal Authority fall below 30, or play a puppet king.
   - Watch for base `ATLAE.208`–`210` breakaway events, at most 2 a year.
5. **Pleas:** give a Fire Nation realm a war against an Earth realm. The Earth King should get the plea event, or a puppet king a memorandum.
   - As an attacked Earth realm, use the Plea to Ba Sing Se decision.
6. **Reach:** game.log's yearly line shows how many tributaries are out of reach.
7. **Check error.log** for anything mentioning `atxb`.
