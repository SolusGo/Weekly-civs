# 026 — The Octopus Parliament

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Octopus Parliament** |
| Leader | Speaker Eightfold |
| Capital | Inkminster |
| Theme | Eight-armed democratic absurdity |
| Preferred victory | Science / Culture |

## UA — The Eightfold Assembly
At the start of the Ancient Era and again at **each player technological era advance**, choose exactly one motion, locked until the next era: **Prosperity** (+1 Gold and +1 Production per city); **Enlightenment** (+1 Science and +1 Culture per city); **Defence** (+10% Combat Strength to eligible military units). Only one resolution may operate at a time.

## UU — Inkguard
**Replaces:** Pikeman

+15% Combat Strength on defense only; survives through normal upgrade lineage.

Retain the installed Community Patch v151 Pikeman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Deliberation Chamber
**Replaces:** Library

+1 Culture permanently; +1 Science during Enlightenment, OR +1 Gold during Prosperity; no additional Science/Gold from Defence.

Retain the installed CP Library's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **The Eightfold Assembly**. Inkguard fills a specialized tactical or exploration role; Deliberation Chamber amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Inkguard using `Civilization_UnitClassOverrides` and Deliberation Chamber using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Save active and pending resolutions. Display a real player choice in a custom Lua popup and sync its selection into gameplay context; protect against repeated sessions after reload and recalc all city/unit effects on transition.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
