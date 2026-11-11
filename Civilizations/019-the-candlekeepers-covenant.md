# 019 — The Candlekeeper's Covenant

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Candlekeeper's Covenant** |
| Leader | High Keeper Seraphine |
| Capital | Last Light |
| Theme | Preservation of the memory of vanished cities |
| Preferred victory | Culture / Science |

## UA — The Names We Carry
Each eligible **permanently destroyed** city formerly belonging to a foreign major civilization records 1 Lost Flame, to a maximum of 12. Each Flame gives +1 Culture in the Capital; every 3 Flames give +1 Science there. Captures without destruction, own cities and city-state cities do not count.

## UU — Vigil Keeper
**Replaces:** Pikeman

+1 Sight and +15% Combat Strength when defending inside friendly territory; lineage bonus persists after upgrading.

Retain the installed Community Patch v151 Pikeman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Hall of Remembrance
**Replaces:** Temple

+1 Culture; +1 Science when the Covenant has 3+ Lost Flames, and another +1 Science at 9+ Lost Flames.

Retain the installed CP Temple's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Culture / Science** by optimizing **The Names We Carry**. Vigil Keeper fills a specialized tactical or exploration role; Hall of Remembrance amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Vigil Keeper using `Civilization_UnitClassOverrides` and Hall of Remembrance using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Track destroyed cities, last observed ownership and processed identities robustly. City destruction is not reliably identifiable from generic Lua prekill alone; verify installed CP hooks and acknowledge rapid capture/raze cases.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
