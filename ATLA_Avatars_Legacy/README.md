# Avatar - Four Nations Restored: Avatar's Legacy

A standalone, 100% additive Crusader Kings II submod for **Avatar - Four Nations Restored** (`Rystic/ATLA-restored`). Every Avatar solves one problem and leaves another behind.

## Installation

1. Copy both `ATLA_Avatars_Legacy.mod` and the `ATLA_Avatars_Legacy/` folder into your CK2 `mod/` directory.
2. Enable **Avatar - Four Nations Restored** and **Avatar - Four Nations Restored: Avatar's Legacy** (fully compatible with `ATLA_Restored_Bugfixes` and `ATLA_Ba_Sing_Se`; zero base-file overrides).

## Features

When an Avatar dies (`on_death`), they leave one of **five burdens** on the world (fading naturally after 50 years if not lifted sooner):

| Burden | Trigger / Weights | World Effect | Avatar's Answer |
|---|---|---|---|
| **Restless Spirits** | Low learning, landed ruler (less likely if `mystic` or `zealous`) | 4 random owned provinces/year get tax -20%, revolt risk +2% (5 yrs) | *Calm the Restless Spirits* (Learning 10, 50 piety) |
| **Daofei Country** | Died under 40 or withdrawn | 4 random Earth Kingdom provinces/year get tax -15%, revolt risk +3% (5 yrs) | *Hunt the Daofei* (Martial 10) |
| **Zealots of the Old Avatar** | Kyoshi always; high learning/piety, `zealous`, or age 70+ | Up to 2 independent duke+ rulers/year worldwide (weighted 2:1 toward the late Avatar's culture group, max once/5 yrs) face a concrete choice: **Placate** (tier-scaled gold or 50 piety) vs. **Push back** (+50 prestige, 5-yr capital revolt risk +4%) | *Disavow the Zealots* (Diplomacy or Learning 10) |
| **Unchecked Ambition** | Roku always; `kind`, `content`, `charitable` | A Champion rises (united Fire Lord striking the Earth coast; Fire Isles unifier; or Earth imperialist while Ba Sing Se is weak) with special CBs and a 20-yr martial/morale buff | *Confront the Champion of Ambition* |
| **An Iron Peace** | `wroth`, `zealous`, `cruel` | Independent duke+ rulers of the policed culture group suffer -10 vassal opinion + 3 provinces/year gain +2% revolt risk | *Heal the Divide* (Diplomacy 12) |

### Missions & Champion Confrontation
- **Self-targeted Avatar missions:** Both player and AI Avatars (landed or unlanded) can undertake 6-12 month missions (`fully_realised_avatar` bypasses stat thresholds). Success lifts the burden worldwide (+150 prestige); failure costs 50 prestige and applies *The Avatar Doubted* (2 yrs).
- **Champion CBs (1-year truce):**
  - *Strike the Earth Coast* (`atxl_cb_fire_strike`): county-tier, coastal Earth Kingdom counties.
  - *Unite the Fire Islands* (`atxl_cb_fire_unification`): duchy-tier across `world_fire_isles`.
  - *Earth Imperialism* (`atxl_cb_earth_unification`): county-tier, neighboring Earth Kingdom counties.
  - An Earth Champion who seizes `c_royal_earth_palace` and controls northeast Earth Kingdom (or 150 holdings) may **Proclaim the Earth Empire** (`e_earth_empire`).
- **Confronting a Champion:**
  - If the Champion **stands down**, the burden ends and their special CBs become invalid.
  - If the Champion **defies** the Avatar and the Avatar chooses to fight beside the defenders:
    - Every defender fighting the Champion's special wars gains *The Avatar Fights Beside Us* (+15% morale, +10% levies for 3 yrs).
    - A **landed, independent Avatar** joins the defensive wars directly (`join_defender_wars`).
    - An **unlanded Avatar** moves to a defender's court and rallies a war-only **Volunteer Host** (~650 troops, `disband_on_peace = yes`, 3-yr cooldown per defender).
