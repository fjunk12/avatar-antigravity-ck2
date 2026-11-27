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

## 2. Petition the Fire Lord (every bookmark)

The Fire Lord is the holder of `e_fire_nation`, or of `k_fire_nation` while the empire is vacant. A Fire Nation vassal in his realm (count or above) can petition him once every 5 years.

- **Players:** the **Petition the Fire Lord** decision.
- **AI:** the Fire Lord's direct vassals petition through the yearly run, at most 2 a year.

| Petition | Fire Lord grants | Fire Lord refuses |
|---|---|---|
| **Royal patronage** | −50 gold from his purse (needs 50); the petitioner gets +50 gold and +15 opinion for 10 years | petitioner −10 opinion for 5 years |
| **Rebuke a rival** (only with a rival in the Fire Lord's realm) | the rival −20 opinion of the Fire Lord for 10 years; the petitioner +25 prestige and +15 opinion | petitioner −10 opinion for 5 years |

## Parked for v2

- The Fire Sages (`d_fire_sages`) and the Bhanti (`bhanti_spirituality`) against the throne.
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
5. **Check error.log** for anything mentioning `atxf`.
