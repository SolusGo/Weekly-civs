# 018 — The Perpetual Timetable

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Perpetual Timetable** |
| Leader | Grand Stationmaster Veyl |
| Capital | Terminus Prime |
| Theme | Rail networks, timetables and civil bureaucracy |
| Preferred victory | Science / Culture |

## UA — The Grand Schedule
Every noncapital city connected to the Capital gets +1 Production and +1 Science. After Railroad, cities linked through a continuous **owned fully railroad land connection** gain +1 Culture.

## UU — Line Surveyor
**Replaces:** Worker

+1 Movement and +10% Work Rate relative to the installed CP Worker.

Retain the installed Community Patch v151 Worker's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Dispatch Office
**Replaces:** Workshop

+1 Gold and +1 Culture when connected to the Capital; an extra +1 Production for an owned strict-railroad connection.

Retain the installed CP Workshop's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **The Grand Schedule**. Line Surveyor fills a specialized tactical or exploration role; Dispatch Office amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Line Surveyor using `Civilization_UnitClassOverrides` and Dispatch Office using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** A normal Civ V city connection is insufficient to prove an owned rail-only route. Implement/verify graph traversal of eligible owned land plots with railroad links; handle city terminals, roads, pillaging, and captures.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
