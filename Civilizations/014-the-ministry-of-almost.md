# 014 — The Ministry of Almost

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Ministry of Almost** |
| Leader | Acting Chancellor Penultimate |
| Capital | Runner-Up |
| Theme | A government eternally finishing second |
| Preferred victory | Science / Culture |

## UA — Always the Challenger
If the civilization trails the leading rival major civilization by 3–5 technologies, all owned cities receive +1 Science and +1 Culture. If 6+ technologies behind, those bonuses become +2 Science and +1 Culture per city; otherwise no bonus.

## UU — Second Wind Guard
**Replaces:** Spearman

+1 Movement and +15% Combat Strength when defending in friendly territory.

Retain the installed Community Patch v151 Spearman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Runner-Up Academy
**Replaces:** Library

+1 Culture permanently; +1 Production when the civilization trails by at least six technologies.

Retain the installed CP Library's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **Always the Challenger**. Second Wind Guard fills a specialized tactical or exploration role; Runner-Up Academy amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Second Wind Guard using `Civilization_UnitClassOverrides` and Runner-Up Academy using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Determine the rival technology lead using verified team-tech counts. Exclude own team and eliminated players; ensure the UA switches off when catching up.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
