# 017 — The Seventeenth Summer

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Seventeenth Summer** |
| Leader | Chorus-Mother Ixa |
| Capital | First Emergence |
| Theme | Sentient cicadas and synchronized emergence |
| Preferred victory | Science / Culture |

## UA — The Long Emergence
Cyclical phases per game speed: Quick 9-turn Dormancy / 3-turn Emergence; Standard 13/4; Epic 20/6; Marathon 39/12. Dormancy: +1 Food per city. Emergence: +2 Production and +1 Culture per city.

## UU — Shellguard
**Replaces:** Spearman

+1 Sight; unique upgrade-persistent lineage makes the unit eligible for +20% Combat Strength during Emergence.

Retain the installed Community Patch v151 Spearman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Brood Nursery
**Replaces:** Granary

+1 Faith permanently; +1 Production during Emergence.

Retain the installed CP Granary's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **The Long Emergence**. Shellguard fills a specialized tactical or exploration role; Brood Nursery amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Shellguard using `Civilization_UnitClassOverrides` and Brood Nursery using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Persist cycle phase, phase turn and per-unit promotion eligibility. Test save/load at phase boundaries and exact game speed lengths.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
