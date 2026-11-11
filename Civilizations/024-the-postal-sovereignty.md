# 024 — The Postal Sovereignty

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Postal Sovereignty** |
| Leader | Postmaster-General Elowen |
| Capital | First Address |
| Theme | An entire nation run by the postal service |
| Preferred victory | Science / Culture |

## UA — The Unbroken Correspondence
Each city with a Central Post Office gains +1 Science. For every three such offices across the empire, each participating city receives +1 Culture, capped at +2 Culture per city at six offices.

## UU — Royal Courier
**Replaces:** Scout

+1 base Movement; another +1 Movement for turns **beginning in friendly territory**; remove temporary benefit outside. Temporary promotion does not survive upgrades.

Retain the installed Community Patch v151 Scout's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Central Post Office
**Replaces:** Market

+1 Gold and +1 Science beyond the inherited CP Market effects.

Retain the installed CP Market's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **The Unbroken Correspondence**. Royal Courier fills a specialized tactical or exploration role; Central Post Office amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Royal Courier using `Civilization_UnitClassOverrides` and Central Post Office using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Track active Post Office count and city participation. Confirm that conditional movement added at owner-turn start produces *usable* movement points rather than only a displayed bonus.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
