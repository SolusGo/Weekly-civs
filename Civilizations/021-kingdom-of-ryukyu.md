# 021 — Kingdom of Ryukyu

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Kingdom of Ryukyu** |
| Leader | Shō Shin |
| Capital | Shuri |
| Theme | Historic Ryukyuan maritime and cultural exchange |
| Preferred victory | Diplomacy / Culture |

## UA — The Maritime Kingdom
Every coastal city gains +1 Gold. A coastal city with a Harbor BuildingClass gains an additional +1 Culture, including its own Harbor replacement.

## UU — Ryukyuan Guard
**Replaces:** Pikeman

+1 Sight and +15% Combat Strength when defending inside friendly territory.

Retain the installed Community Patch v151 Pikeman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Naha Trading Port
**Replaces:** Harbor

+2 Gold and +1 Science, retaining the installed CP Harbor's normal effects.

Retain the installed CP Harbor's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Diplomacy / Culture** by optimizing **The Maritime Kingdom**. Ryukyuan Guard fills a specialized tactical or exploration role; Naha Trading Port amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Ryukyuan Guard using `Civilization_UnitClassOverrides` and Naha Trading Port using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Use the actual coastal-city predicate and Harbor BuildingClass; coastal defense bonus must truly be defense-only. Historical design is intentionally vanilla-like.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
