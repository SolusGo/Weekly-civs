# 025 — The Carapace Dominion

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Carapace Dominion** |
| Leader | High Claw Thalassar |
| Capital | Red Shoal |
| Theme | Intelligent crab coastal fortress empire |
| Preferred victory | Science / Domination |

## UA — The Unbroken Shore
Every coastal city receives +1 Production. A coastal city possessing a Walls BuildingClass additionally receives +1 Science.

## UU — Shellbreaker
**Replaces:** Swordsman

+20% Combat Strength when defending on a passable **coastal land tile adjacent to water**; no attack benefit. The lineage bonus survives upgrading.

Retain the installed Community Patch v151 Swordsman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Tidal Bastion
**Replaces:** Walls

+1 Production permanently; +1 Gold if the city is coastal.

Retain the installed CP Walls's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Domination** by optimizing **The Unbroken Shore**. Shellbreaker fills a specialized tactical or exploration role; Tidal Bastion amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Shellbreaker using `Civilization_UnitClassOverrides` and Tidal Bastion using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Civ V has no simple stock promotion for defense specifically on *all coastal land plots*. Verify CP v151 combat hooks or scoped temporary promotion reconciliation without granting inland bonuses.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
