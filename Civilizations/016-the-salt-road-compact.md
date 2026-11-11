# 016 — The Salt Road Compact

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Salt Road Compact** |
| Leader | First Broker Nahir |
| Capital | White Mile |
| Theme | Desert merchants and caravan economics |
| Preferred victory | Science / Diplomacy |

## UA — The Price of Passage
Each city originating one or more active land trade routes receives +2 Production and +1 Culture. This is a binary city bonus, **not** a bonus per route.

## UU — Dune Escort
**Replaces:** Horseman

+1 Sight and +15% Combat Strength when attacking into or defending on Desert terrain.

Retain the installed Community Patch v151 Horseman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Salt Exchange
**Replaces:** Caravansary

+1 Food and +1 Gold permanently; +1 Science while the city originates at least one active land trade route.

Retain the installed CP Caravansary's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Diplomacy** by optimizing **The Price of Passage**. Dune Escort fills a specialized tactical or exploration role; Salt Exchange amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Dune Escort using `Civilization_UnitClassOverrides` and Salt Exchange using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Check trade-route origin and land domain, refresh as routes start/end, and verify the separate attack-target/defender-terrain modifier against CP v151.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
