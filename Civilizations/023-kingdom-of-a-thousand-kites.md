# 023 — Kingdom of a Thousand Kites

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Kingdom of a Thousand Kites** |
| Leader | Sky-King Aeral |
| Capital | Windspire |
| Theme | Wind festivals and open grassland culture |
| Preferred victory | Culture / Science |

## UA — Children of the Open Sky
A city founded on Plains or Grassland receives +1 Production. A city with at least three of its six adjacent plots having underlying Plains or Grassland receives +1 Culture. Hills and Forests do not erase qualifying terrain.

## UU — Windrunner
**Replaces:** Horseman

+1 Movement and +10% Combat Strength when attacking a defender occupying Plains or Grassland; no defensive bonus.

Retain the installed Community Patch v151 Horseman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Kite Pavilion
**Replaces:** Amphitheater

+1 Culture; +1 Gold if the city is founded on Plains or Grassland.

Retain the installed CP Amphitheater's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Culture / Science** by optimizing **Children of the Open Sky**. Windrunner fills a specialized tactical or exploration role; Kite Pavilion amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Windrunner using `Civilization_UnitClassOverrides` and Kite Pavilion using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Use underlying terrain types, not features; check the defending plot for the offensive promotion. Confirm the specific CP combat hook or modifier before coding.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
