# Avatar - Earth Kingdom

Shown in the launcher as **Avatar - Earth Kingdom** (formerly "ATLA Ba Sing Se"). The folder (`ATLA_Ba_Sing_Se`), the prefix (`atxb_`) and the `ATLA Ba Sing Se:` lines in game.log are unchanged, so saves keep working.

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

## Overextended Crown

In lore Ba Sing Se never ruled the Earth Kingdom directly: it was too vast. Conquest stays possible, but holding the land costs something.

- **The count:** each year the crown counts the provinces in the king's realm **outside the Ba Sing Se region** (`world_ba_sing_se`), his vassals' included. Tributaries don't count. Every bookmark starts at 0: all 34 crown counties lie inside the region.
- **Land counts however it was gained:** conquest, claims or the base mod's Annex Domain.
- **Penalties** (a modifier on the Earth King, renewed every year):

| Provinces outside the walls | Modifier | Vassal opinion | Tax | Revolt risk |
|---|---|---|---|---|
| 15+ | Overextended Crown | −10 | −15% | +2% |
| 45+ | Badly Overextended Crown | −20 | −25% | +4% |

- **Raising capacity:**
  - The Royal Roads raise both thresholds by 15.
  - A Single Law raises both by 15.
  - So with both works the thresholds are 45 / 75.
- **Lifting it:** under Monarchism (`ek_unity_3`) with both works finished, the crown is never overextended.
- **Readout:** the treasury overview and game.log's yearly line show "outside the walls N (capacity X / Y)".
- **This applies under Disunion too.** The base law makes conquest free; this submod makes *holding* the land cost something.

## The treasury of Ba Sing Se

Tribute in CK2 goes to the Earth King's own purse. Each year a share of it moves into a crown treasury (`global_atxb_treasury`, at most 1,000):

- **Crown lands:** 10 gold, +10 at Royal Authority 30, +10 at 60.
- **Share of tribute:** per tributary, outpost 1, territory 2, province 3, state 4 gold (+25% after A Single Law).
  - Never more than 25% of the king's gold.
  - Never more than 80 a year together with the crown lands.
  - Nothing at all while the king has less than 25 gold.
- **Reporting:** every year (365 days; v2 ran every 333 days by mistake) a line starting `ATLA Ba Sing Se:` goes to game.log. The treasury overview shows the same figures.
- **Puppet king** (`trait = earthkingpuppet`): the king cannot spend the treasury. The **Grand Secretariat** does it: the holder of `d_dai_li`, or the chancellor before that title exists.
  - It first saves until the treasury covers the whole Royal Granaries (300), then builds them once, to keep the Lower Ring quiet.
  - It never builds the roads or the single law.
  - Once the Granaries stand, every year it takes a quarter of the treasury (at least 25, while the treasury has 50+) for itself.
  - A player puppet gets an "expenses of state" report.
- **Looting:** a foreign or Way of Chin ruler holding the Royal Palace takes the whole treasury.

**For players, everything sits in one place:** **The Treasury of Ba Sing Se**, a high-priority entry in the Intrigue tab. It opens a popup with the ledger and only the actions you can take right now:
- Start a royal work (a second page lists the works you can afford).
- Draw on the Treasury.
- Call a corvée.

After each action the popup reopens with the new figures. The AI takes the same actions as ordinary decisions. Base-mod and vanilla decisions stay in the Intrigue tab: a submod can't hide them without overriding their files.

| Work | Cost | When finished |
|---|---|---|
| Royal Roads | 100, then 4 × 125 | Earth Kingdom provinces outside the Si Wong: supply +1, tax +5%. Overextension thresholds +15 |
| A Single Law for the Kingdom (needs the States or Monarchism unity law) | 200, then 3 × 200 | Royal Authority +5, breakaway chance halved, treasury share +25%, Earth tributaries −10 opinion for 20 years, overextension thresholds +15 |
| Royal Granaries | 100, then 2 × 100 | Ba Sing Se region: tax +10%, disease defence +20% |

**Rules for works:**
- One stage is paid each year.
- If the treasury can't pay, the work stalls. Three stalls in a row abandon it, and the money spent is lost.
- The AI builds one work at a time, and only starts one with the first payment plus one yearly stage in hand (Roads 225, Law 400, Granaries 200).
- game.log records every stall and abandonment.

**Also:**
- **Draw on the Treasury:** 100 out, 50 to your purse, Royal Authority −5, every 2 years.
- **Call a corvée:** Royal Authority −15, treasury +100, once a year, only while a work is under construction. The AI only does this while Royal Authority is 50 or more.
- **Sabotage the Crown's Works:** any independent Earth or Way of Chin realm can spend 25 gold, every 5 years. The outcome is a 45% setback, 30% nothing, or 25% caught; being caught is likelier when the king's spymaster is good and less likely with a skilled saboteur.
  - The AI only sabotages if it dislikes the king, is his rival, or follows the Way of Chin.

## Petition for a Royal Grant

An Earth Kingdom tributary (duke or above, not Way of Chin) can ask the crown for gold from the treasury. It needs a treasury of 50 or more, and it can ask once every 5 years.

- **Players:** the **Petition for a Royal Grant** decision.
- **AI tributaries:** they ask through the yearly run, only if they have less than 50 gold and an opinion of the king of 25 or more. At most 2 a year across the world.

The Earth King answers:

| Answer | Cost to the treasury | Effect on the tributary |
|---|---|---|
| Grant 100 | −100 | +100 gold, +25 opinion for 10 years, won't break away for 10 years |
| Grant 50 | −50 | +50 gold, +15 opinion for 10 years |
| Refuse | — | −10 opinion for 5 years |

- **AI king:** more generous when charitable or with a full treasury (400+); stingier when greedy.
- **Puppet king:** the Grand Secretariat always refuses.

## The Daofei Underworld (Earth realms outside Ba Sing Se)

Daofei are the outlaw brotherhoods of the Earth Kingdom.
- **Who:** any Earth lord (duke or above, independent or a vassal, not the Earth King and not Way of Chin) whose capital lies in the Earth Kingdom outside the Ba Sing Se region. Nothing is tied to one title.
- **How often:** each year an eligible lord has a 3% chance. That doubles while the crown is weak (Royal Authority below 30) and is ×1.5 at war. At most 3 lords a year worldwide, and each lord at most once every 5 years.

| Choice | Cost | Result |
|---|---|---|
| **Root them out** | 25 gold | 70%: +20 prestige and every daofei presence in the realm is cleared (better odds with martial 12+, worse at war). 30%: −10 prestige and they settle in |
| **A quiet understanding** | — | +30 gold, they settle in |
| **Hire them** (only at war) | 25 gold | 500 irregulars at your capital until peace, and they settle in |

- **Daofei presence** (`atxb_daofei_presence`): a province modifier lasting 5 years, with tax −15% and revolt risk +2%.
- **Hire Daofei Irregulars** (decision, at war, every 3 years): 50 gold for 500 irregulars (light infantry and archers, normal upkeep) until peace. If no daofei are in your realm yet, they settle at your capital.

## Royal Arbitration

The Earth King can order an Earth realm to stop a war against a fellow Earth realm. Use it from the **attacker's diplomacy screen**.

- **Who:** the attacker must be an independent Earth realm (duke or above, not Way of Chin) attacking a non-Chin Earth realm. You must not be at war with it.
- **Cost:** Royal Authority 10 (duke), 15 (king) or 25 (emperor). Once a year. Not for a puppet king.
- **Obey:**
  - Every war it wages against a fellow Earth realm ends in a white peace. A war against the Fire Nation never ends this way.
  - It can't declare war for 2 years.
  - It thinks 10 less of the king for 5 years.
- **Defy:** the crown loses another 5 Royal Authority, and the king loses 25 prestige.
- **AI odds:** obeying is likelier with a strong crown (Royal Authority 60+), as the king's tributary, or with good opinion of the king. It is less likely with a weak crown, bad opinion, or an ambitious or proud ruler. A player target chooses.
- **AI kings:** they don't use it yet.

The base mod's other Royal Authority actions remain:
- Recognise Noble, Annex Subject, Demand Reverence and Loyalty Campaign (targeted decisions on tributaries).
- Sell Titles, the unity laws and the reconquest war.

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
7. **Treasury popup:** open The Treasury of Ba Sing Se, start a work, draw and call a corvée. The popup should reopen with the new figures.
8. **Royal Arbitration:** find two Earth realms at war, open the attacker's diplomacy screen and use Royal Arbitration. With a player target, the target chooses.
9. **Overextended Crown:** game.log's yearly line shows the provinces outside the walls and the capacity. Once the king rules 15 or more provinces outside the walls, the modifier should appear on him.
10. **Royal Grant:** play an Earth tributary and use Petition for a Royal Grant, or watch game.log for `asked Ba Sing Se for a royal grant`.
11. **Daofei:** play an Earth lord outside Ba Sing Se. game.log shows `daofei appeared in`. At war, try Hire Daofei Irregulars.
12. **Check error.log** for anything mentioning `atxb`.
