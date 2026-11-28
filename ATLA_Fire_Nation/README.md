# Avatar - Fire Nation

Fire Nation submod for **Avatar - Four Nations Restored** (`Rystic/ATLA-restored`). It depends only on the main mod and overrides no base file. Everything is prefixed `atxf_` (event namespace `atxf`). **Not yet tested in game.**

Install: copy `ATLA_Fire_Nation.mod` and the `ATLA_Fire_Nation/` folder into the CK2 `mod/` folder and enable it with the main mod.

Design: agreed in fjunk12/avatar-antigravity-ck2#5 and signed off by the owner. v1 has two systems.

## 1. The Camellia-Peony War (560)

In history the Fire Lord's throne (`e_fire_nation`) is vacant from 545 to 643: Zoryu holds `k_fire_nation`, and his half-brother Chaejin (Saowon dynasty) holds `k_western_fire_nation`.
- They are already rivals.
- Each has a claim on the other's kingdom, so the vanilla claim war is the war itself.
- The clans' crests: the Keohso (Zoryu's mother's clan) bear the **winged peony**, the Saowon the **stone camellia**.

**Start.** The first yearly run before 576 starts the dispute if:
- `e_fire_nation` is vacant,
- a Saowon holds `k_western_fire_nation`,
- and that ruler is the rival of the `k_fire_nation` holder.

The sides go by title, so heirs carry on the quarrel. When it starts:
- **The clans take sides automatically:** Keohso lords (dynasty 3994) join the Peony, Saowon lords (3995) the Camellia.
- **Every other Fire Isles lord** (count or above, capital in `world_fire_isles`) chooses Peony, Camellia or neither.
- **Backing a side:** +20 opinion of that champion and −20 of the other, for 15 years.
- **Call of the Clans:** while one champion attacks the other, independent supporters join the war on their champion's side. Supporters who are vassals already fight in their liege's wars.
- **The Avatar's warning:** if an Earth Avatar is alive (Kyoshi in 560), both claimants get a letter. Heeding gives +25 piety; dismissing gives +25 prestige.

**Court intrigue.** Each year, up to 2 lords receive an envoy from the other side (or from either side, for a neutral lord).
- **Accepting:** the lord changes sides and gets 25 gold, paid by that champion.
- **Refusing:** an aligned lord gets +10 prestige.
- **Limit:** a lord can be courted at most once every 2 years.

**End.** The dispute ends once one ruler holds `e_fire_nation` or both kingdoms, or once one kingdom has no holder. The winner (if of Fire culture) chooses:

| Choice | Modifier (20 years) | Keohso and Saowon opinion of the winner (20 years) |
|---|---|---|
| **Break the clans** (canon: Zoryu) | tax +10%, levy +10%, vassal opinion −5; 50% chance of `dishonourable` | −25 |
| **Compact with the clans** | vassal opinion +10, tax −5% | +15 |

If nothing is decided by 600, the dispute fades quietly. Titles are never taken from anyone automatically.

### After the war (v1.1): the choice lasts for generations

Canon: Zoryu began *a generational project* to make the clans irrelevant, and Kyoshi demanded clemency for the Saowon ([Avatar Wiki](https://avatar.fandom.com/wiki/Camellia-Peony_War)). Both paths now go on after the choice, through every later Fire Lord. The "Fire Lord" is the holder of `e_fire_nation`, or of `k_fire_nation` while the empire is vacant.

**Break the clans: a generational project** (`global_atxf_centralization`, 0–100; it starts at 10).
- **Each year:** +4, and game.log records the progress.
- **About every 3 years**, the Fire Lord faces a hard step:

| Step | Effect |
|---|---|
| **Confiscate a clan's estates** | +75 gold; that clan lord −30 opinion for 20 years; +15 |
| **Raise commoner officials** | −25 prestige; all Keohso and Saowon −10 opinion for 10 years; +10 |
| **Purge the Saowon** | all Saowon −40 opinion for 20 years; 50% chance of `dishonourable`; +25 |
| **Not yet** | nothing |

- **Kyoshi's clemency:** the first purge, while an Earth Avatar lives, waits for the Avatar's letter.
  - Heeding it spares the Saowon, gives +25 piety and blocks purges for 10 years.
  - Defying it costs 50 piety, and the purge goes ahead.
- **Backlash:** each year, a 20% chance that an aggrieved Keohso or Saowon lord (opinion below 0) remonstrates.
  - **Silence them:** +10 prestige, that lord −20 opinion, project +5.
  - **Give ground:** that lord +20 opinion, project −10.
- **At 100: the Absolute Throne.** Every Fire Lord from then on gets tax +10%, levies +10% and +0.5 prestige a month, renewed by the yearly run.

**The Compact: obligations.**
- **The modifier** (vassal opinion +10, tax −5%) passes to every Fire Lord while the Compact holds.
- **About every 3 years**, the clan council demands one of three things:
  - 100 gold.
  - A seat on the council: −50 prestige, and a 10-year modifier (tax −5%, vassal opinion +5).
  - A royal match: −25 prestige.
- **Honouring a demand:** the clans +10 opinion for 10 years.
- **Refusing:** the second refusal **shatters** the Compact. The clans −40 opinion for 20 years, and the throne starts the project to break them, from 0.

**The Fire Sages and the throne.** Every new Fire Lord (Fire culture) is asked once.

| Choice | Modifier for life | Other effects | Clan project |
|---|---|---|---|
| **Revere the old ways** | +0.5 piety a month, vassal opinion +5 | — | −10 |
| **Subordinate the Sages** | +0.5 prestige a month, tax +5% | −50 piety; the holder of `d_fire_sages` −30 opinion | +10 |

## 2. Petition the Fire Lord (every bookmark)

The Fire Lord is the holder of `e_fire_nation`, or of `k_fire_nation` while the empire is vacant. A Fire Nation vassal in his realm (count or above) can petition him once every 5 years.

- **Players:** the **Petition the Fire Lord** decision.
- **AI:** the Fire Lord's direct vassals petition through the yearly run, at most 2 a year.

| Petition | Fire Lord grants | Fire Lord refuses |
|---|---|---|
| **Royal patronage** | −50 gold from his purse (needs 50); the petitioner gets +50 gold and +15 opinion for 10 years | petitioner −10 opinion for 5 years |
| **Rebuke a rival** (only with a rival in the Fire Lord's realm) | the rival −20 opinion of the Fire Lord for 10 years; the petitioner +25 prestige and +15 opinion | petitioner −10 opinion for 5 years |

## Parked for v2

- The Bhanti (`bhanti_spirituality`).
- Colonial tension or a war council.
- The dynamic Hundred Year War.
- The Yuyan Archers already exist in the base mod (`d_yuyan_archers`).

## Test in game

1. **560 start:**
   - After the first year, game.log should have `ATLA Fire Nation: the Camellia-Peony dispute begins`.
   - Zoryu and Chaejin should get the opening event.
   - A Fire Isles lord should get the choice of sides.
2. **Play Zoryu or Chaejin:** press the claim on the other kingdom. Independent supporters should join the war.
3. **Win the war, or take both kingdoms:** the aftermath choice should appear within a year.
4. **Petition:** play a Fire vassal and use Petition the Fire Lord. AI petitions appear in game.log as `petitioned the Fire Lord`.
5. **After the war:** game.log shows `the project to break the clans stands at N/100` every year on the Break path, and `honoured a demand` / `refused the clan council` on the Compact path. A new Fire Lord gets the Fire Sages event.
6. **Check error.log** for anything mentioning `atxf`.
