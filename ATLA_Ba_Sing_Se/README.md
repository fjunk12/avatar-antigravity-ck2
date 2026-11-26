# ATLA Ba Sing Se

Earth Kingdom submod for **Avatar - Four Nations Restored** (`Rystic/ATLA-restored`). It depends only on the main mod and overrides no base file. Everything is prefixed `atxb_` (event namespace `atxb`), so it can run alongside `ATLA_Restored_Bugfixes` and `ATLA_Avatars_Legacy` (`atxl_`).

Install: copy `ATLA_Ba_Sing_Se.mod` and the `ATLA_Ba_Sing_Se/` folder into the CK2 `mod/` folder and enable it with the main mod. **Not yet tested in game.**

Design: agreed in fjunk12/avatar-antigravity-ck2#5 (Topic 1) and signed off by the owner.

## Living tributaries (built on the base mod's own system)

The base mod already has four Earth Kingdom tributary types: outpost 10%, territory 12%, province 16% and state 20%. Each tributary adds to Royal Authority (`earthking.56`). The base mod also has the pledge and break-away decisions, but the AI never uses them (`ai_will_do = 0`). This submod adds the AI side:

| What | When | Effect |
|---|---|---|
| **Breakaway** | AI tributary, duke or above, opinion of the Earth King below 0, and the crown is weak (puppet king, Royal Authority below 30, or at war with Royal Authority below 50). Not in the first 3 years of a campaign, not within 10 years of pledging. | Exactly the base decision's effect (events `ATLAE.208`–`210`, flag `earth_kingdom_rebel`). The Earth King's answer is the base `earth_kingdom_reconquest` war. 20% chance a year per candidate (10% after A Single Law), **at most 2 a year**. |
| **Peacetime pledge** | AI independent Earth realm at peace, bordering a Fire Nation or Way of Chin realm or a neighbour at least twice as strong. Or: Royal Authority 60+, opinion of the king 25+, and not Disunion. A realm that broke away waits 20 years. | Becomes a territory tributary (as the base `pledge_to_earth_king`, event `ATLAE.212`). 15% a year per candidate, 8% once the crown has 10 tributaries, 4% at 20. **At most 2 a year.** |
| **Wartime petition** | AI independent Earth realm defending against a Fire Nation or Way of Chin attacker. At most once every 5 years per realm, at most 2 a year in total. | The Earth King chooses: **Fund Local Defense** (treasury −50: the petitioner gets 25 gold and about 650 soldiers raised at its capital, with no upkeep, which disband at peace) / **March to Their Aid** (only within 450 map pixels of Ba Sing Se, and not as a puppet: joins their defensive wars) / **Tribute Only** / **Refuse**. The first three make them a territory tributary. |

Wartime pledging deliberately goes past the base decision's `allow = { war = no }`: that is the point of a petition.

## The treasury of Ba Sing Se

Tribute in CK2 goes to the Earth King's own purse. Each year a share of it moves into a crown treasury (`global_atxb_treasury`, at most 1,000):

- **Crown lands:** 10 gold, +10 at Royal Authority 30, +10 at 60.
- **Share of tribute:** per tributary, outpost 1, territory 2, province 3, state 4 gold (+25% after A Single Law).
  - Never more than 25% of the king's gold.
  - Never more than 80 a year together with the crown lands.
  - Nothing at all while the king has less than 25 gold.
- **Reporting:** every year a line starting `ATLA Ba Sing Se:` goes to game.log. The treasury overview shows the same figures.
- **Puppet king** (`trait = earthkingpuppet`): the king cannot spend the treasury. The **Grand Secretariat** does it: the holder of `d_dai_li`, or the chancellor before that title exists. It starts one work at a time (granaries, roads, then the law) and in 1 year out of 5 takes 100 gold for itself. A player puppet gets a report.
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
5. **Wartime petitions:** give a Fire Nation realm a war against an Earth realm. The Earth King should get the petition event.
6. **Check error.log** for anything mentioning `atxb`.
