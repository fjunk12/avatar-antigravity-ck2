# Avatar - Four Nations Restored: Bugfix Patch

A standalone Crusader Kings II submod that fixes script, gameplay, map, graphics, character history, encoding, and localization bugs in **Avatar - Four Nations Restored** (`Rystic/ATLA-restored`) without modifying the base mod files.

## Installation

1. Copy both `ATLA_Restored_Bugfixes.mod` and the `ATLA_Restored_Bugfixes/` folder into your CK2 mod directory:
   - Windows: `Documents\Paradox Interactive\Crusader Kings II\mod\`
   - Linux: `~/.paradoxinteractive/Crusader Kings II/mod/`
   - macOS: `~/Documents/Paradox Interactive/Crusader Kings II/mod/`
2. Launch CK2 and enable **both**:
   - `Avatar - Four Nations Restored`
   - `Avatar - Four Nations Restored: Bugfix Patch`

The submod declares `dependencies={ "Avatar - Four Nations Restored" }` so CK2 automatically loads all patched files after the base mod.

## Summary of Fixes

### Critical Script, Event & Crash Fixes
- **Claim Duels (`decisions/hf_warrior_lodge_decisions.txt`)**: Fixed broken call to non-existent event `HF.10095` -> `HFP.10095`.
- **Wonder Maintenance (`events/LT_wonder_maintenance_events.txt`)**: Fixed invalid `else = { limit = { ... } }` -> `else_if = { limit = { ... } }`.
- **Tea Society Missions (`events/ATLA_tea_society_events.txt`)**:
  - Fixed all 12 `TEA.1001`–`TEA.1012` quest calls that wrongly invoked `society_quest_event` via `character_event`.
  - Fixed 3 mismatched `clr_quest` names (`quest_educate` -> `quest_teach_kindness`, `quest_take_family_focus` -> `quest_family_focus`, `quest_take_theology_focus` -> `quest_theology_focus`) so those missions actually complete.
- **Sand Sailer Racers Missions (`events/ATLA_society_sand.txt`)**: Fixed mismatched `clr_quest = donation_quest` -> `clr_quest = donate_to_sand_society` (and cleared `donation_quest` flag).
- **White Lotus Missions (`events/ATLA_society_agni_kai.txt`, Issue #347)**:
  - Fixed inverted rank condition on `twl_quest_pacify_rebellion` (`society_rank >= 3` -> `society_rank < 3`).
  - Added missing `society_rank < 2` exclusions to `twl_quest_train` and `twl_investigate_court` so Rank 1 members are no longer assigned impossible Rank 2 missions.
  - Moved `MNSAK.5222` (`hide_window = yes`) ping into `immediate`.
- **Death of Roku Eruption (`events/ATLA_hundred_year_war.txt`, Issue #615)**:
  - Fixed `ATLAE.19` and `ATLAE.10` so Roku reliably dies in the volcano eruption even when `HYW_1` is not set, and prevented `ATLAE.19` from repeating via `roku_volcano_fired`.
  - Fixed `ATLAE.122`/`127`/`130` invalid `FROM = { wealth = ROOT }` after death (replaced with `transfer_scaled_wealth` before death) and removed `trigger = { ai = no }` on `ATLAE.129`'s sole option.
- **"A New Era" Event Spam (`events/ATLA_imperial.txt` & `common/laws/a_atla_laws.txt`, Issue #567)**:
  - Moved `ATLA_imperial.1` calls from law `effect` (which re-runs on load/recalculation) into `pass_effect`, guarded by `GLOBSTATE_age_of_imperialism`.
  - Set `GLOBSTATE_age_of_imperialism` in `ATLA_imperial.1` `immediate` and added fallback desc/option in `ATLA_imperial.2` for rulers outside the Four Nations culture groups.
- **Childhood Bending Sub-Traits (`events/ATLA_bending.txt`, Issue #501)**:
  - Required matching bending element (or Avatar educator) in `bending.162` before firing `bending.163`.
  - Fixed blind seismic sense teaching `seismicsense_nonblind` instead of `seismicsense`.
  - Removed duplicate `# No` option in `bending.163` and converted tier upgrade `if` blocks to `if / else_if`.
- **Air Nomad Elder Council Voting & Laws (`events/ATLA_air_nomad_events.txt`, Issue #303)**:
  - Replaced hardcoded 3-vote threshold across all 6 policies with true majority voting (`yes_votes > no_votes`), so solo Elder Council members and small councils can pass policies.
  - Fixed `NOMAD.608` Protectionism setting `global_cp_trade_vote` instead of `global_cp_protection_vote`.
  - Fixed `NOMAD.612` setting `ROOT`'s law to `an_law_2` in all cases and fixed `NOMAD.619` cascading from `an_law_3` all the way down to `an_law_0` in a single vote.
- **Early History Events (`events/ATLA_early_history.txt`, Issue #595)**:
  - Added `hide_from = yes` and `show_root = yes` to `ATLAE.4000` so Avatar Kyoshi appears as the portrait instead of the random maintenance ruler.
  - Fixed impossible trigger condition in `ATLAE.4007` ("Fall of the Chin Remnant": `year = 588` + `NOT = { year = 580 }` -> `NOT = { year = 590 }`).
  - Fixed `ATLAE.4007` calling `long_character_event` `ATLAE.4004` via `narrative_event`.
- **Fifth Nation CBs & Pirate Cartel Government (`common/cb_types/outlaw_religions_cbs.txt`, `common/governments/feudal_governments.txt`, Issue #632)**:
  - Fixed `cb_slave_colony` ("Enslave Province") calling `set_defacto_liege = THIS` *after* `make_tributary` (which immediately broke the tributary due to `breaks_on_realm_change = yes`), and fixed `culture = THIS` on a duchy scope.
  - Fixed `lawless_piracy` superseding `pirate_cartel` whenever a Pirate Cartel ruler grants land to courtiers or wins Plunder wars.
- **Air Reclamation CB (`common/cb_types/03_cb_types_ATLA.txt`, Issue #71)**: Moved `religion_group = air_religions` into `can_use` so non-Air-Nomad rulers do not receive Air Nomad Reclamation Claims.
- **Colonisation System (`decisions/ATLA_colony_decisions.txt`, `events/ATLA_colony_system.txt`, Issue #505)**:
  - Changed `colonize_province` filter from `owned` to `sub_realm_owned` and fixed inverted `is_liege_or_above = FROM` so rulers can colonize both direct and vassal counties (and never their liege's).
  - Fixed `ATLA.9000` ticking vassal colonies multiple times per year (`any_realm_province` -> `any_demesne_province`).
  - Fixed inverted stewardship penalties in `ATLA.9001` (`> 10`/`> 4` -> `< 10`/`< 4`).
  - Fixed swapped Fire Nation colonial cultures in `ATLA.9006` (`colonial_fire_air` / `colonial_fire_water`).
  - Prevented `ATLA.9008` from double-firing `ATLA.9004` on independent rulers.
- **Spiritual Journey (`decisions/ATLA_religious_decisions.txt`, Issue #50)**: Removed permanent `HYW_0` global flag block on `spiritual_journey`.
- **Religious Conversion & Secret Faith (`decisions/conversion_decisions.txt`, `decisions/mnm_secret_religious_societies_decisions.txt`, Issue #104)**:
  - Changed `convert_to_spouse_religion` filter from `home_court` to `spouse` so landed/foreign spouses are valid targets.
  - Allowed `convert_to_liege_religion` across non-modern religion groups, and added liege support to `secretly_convert_to_close_relations_religion`.
- **Pacifist Airbender Ambitions (`common/objectives/00_ambitions.txt`, `00_zeus_ambitions.txt`, Issue #608)**: Excluded `air_spirituality` from `obj_see_the_realm_grow`, `obj_become_king`, and `obj_build_a_war_chest`.
- **Imprisoned Spouse Fertility (`common/event_modifiers/00_event_modifiers.txt`, Issue #49)**: Added `fertility = -10.0` to `house_arrest` so imprisoned wives stop conceiving children while locked up.
- **Validator Script Fixes**:
  - Removed non-existent `succ_byzantine_elective` in `events/plot_events.txt`.
  - Replaced non-existent `nick_the_devil` with `nick_the_wicked` in `events/wol_intrigue_events.txt` and `events/wol_scholarship_events.txt`.
  - Fixed empty modifier block in `events/wol_family_events.txt`.
  - Replaced non-existent vanilla regions `world_africa`/`world_india` with `world_si_wong`/`world_southern_earth_kingdom` in `common/scripted_effects/00_scripted_effects.txt`.
  - Removed dead `hermetic_glasses` artifact reference in `events/ATLA_avatar_acquintances_events.txt`.
  - Added missing `namespace` declarations to `events/rip_eternal_life_events.txt`, `events/soa_various_events.txt`, `events/hfp_duel_events.txt`, and `events/job_lord_spiritual.txt`.

### Map, Unit Models & Portrait GFX Fixes
- **Army Rally Points & Island Pathfinding (`map/island_region.txt`, Issue #125)**: Rebuilt `island_region.txt` from full-map connected-component analysis, adding missing Southern Water Tribe provinces (`562`–`566`: Ublaami, Inupiatun, Nunavut, Atauhiq, Quana), Northern Water Tribe provinces (`553`–`561`), Fire Nation mainland (`60`–`95`), Air Temple islands, and all outer islands, and removing mainland-connected Western Air Temple.
- **Broken Unit & Ship Models (`common/cultures/00_cultures.txt`, `interface/atla_avatars.gfx`, Issue #506)**:
  - Added `westerngfx` fallback to all 18 culture `graphical_cultures` declarations that lacked one (fixing disappearing armies and ships displaying as infantry).
  - Fixed duplicate `westerngfx_fire_benders_helmet` typo -> `westerngfx_water_benders_helmet` and added missing `westerngfx_sky_bison` actor definitions.
- **Broken `.tga` -> `.dds` Texture Paths**: Fixed `interface/ATLA_traits.gfx` (`house_customizer.dds`), `interface/eventwindow.gfx` (`comet.dds`), `interface/portraits/portraits_earthroyalgfx.gfx` (`young_kuai.dds`, `young_suki.dds`), and `interface/portraits/portraits_korra.gfx` (`young_korra.dds`).

### Character History Fixes
- Fixed invalid parent/child ages and marriage dates in `NE_Characters.txt`, `earth_king_branches.txt`, `omashu_characters.txt`, `BA_Characters.txt`, and `WE_Characters.txt` (including upstream PR #668 fixes).

### Localization, Vanilla Flavor Leaks & Encoding Fixes
- **Last Airbender Bookmark (`common/bookmarks/00_bookmarks.txt`, `localisation/ATLA_bookmarks.csv`, Issue #667)**: Fixed Ozai's broken `ERA_CHAR_NAME_2` -> `ERA_CHAR_NAME_23`, added missing Last Airbender bookmark/character descriptions (`ERA_CHAR_NAME_23/24`, `ERA_CHAR_INFO_23/24`, `BM_AIRBENDER_ERA`), fixed corrupted `erai?1` text, and filled in placeholder Hundred Year War bookmark descriptions.
- **Vanilla Flavor Overrides (`localisation/0000_ATLA_bugfix_loc.csv`)**:
  - Issue #610: Renamed `true_christian_knight` -> "True Honorable Warrior".
  - Issue #609: Added ATLA `chinese_imperial_government_desc` for Earth Monarchy.
  - Issue #597: Added `desc_supporting_the_earth_kingdom` for Earth Kingdom Upkeep.
  - Issue #559: Adapted `EVTDESC_RoI_215`/`218` ("Merchant from Hindustan") to Ba Sing Se / komodo rhino.
  - Issue #312: Adapted `NEWBORN_PURPLE_SETUP`/`LOG` and `born_in_the_purple` to the Royal Earth Palace.
  - Issue #32: Fixed `tooltip_obj_see_the_realm_grow` scope (`[Root.realmSizeGoal.GetValue]` -> `[This.realmSizeGoal.GetValue]`).
  - Added missing localization for 11 ATLA decisions and their descriptions.
- **Windows-1252 Encoding Repairs**: Restored corrupted UTF-8 / `U+FFFD` bytes in `localisation/ATLA_bloodlines.csv` (30 broken `§` color codes), `localisation/ATLA_custom_titles.csv` (85 corrupted diacritics), `events/roi_various_events.txt`, and `events/ze_adolescence_events.txt`.
