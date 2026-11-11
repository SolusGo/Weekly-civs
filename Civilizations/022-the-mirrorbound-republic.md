# 022 — The Mirrorbound Republic

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Mirrorbound Republic** |
| Leader | First Reflector Caelis |
| Capital | Verity |
| Theme | Philosophers who learn through failure |
| Preferred victory | Science / Domination |

## UA — Lessons Written in Glass
Eligible combat deaths of own military units to a foreign major civilization's military unit grant one Lesson (max 5). Spend 2 Lessons for **Revised Doctrine**: +10% Combat Strength to military units for 3 owner-turns, independent cooldown 10 owner-turns. Or spend 3 for **Corrected Method**: +10% Capital Science for 5 owner-turns, independent cooldown 10. No stacking the same action while active.

## UU — Reflection Guard
**Replaces:** Swordsman

+1 Sight. After surviving an enemy melee attack, gain +15% Combat Strength on the next attack only; the bonus expires by the end of the next owner-turn if unused, and does not stack. Upgrade lineage persists.

Retain the installed Community Patch v151 Swordsman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Chamber of Revision
**Replaces:** University

+1 Culture and +1 Science permanently; an additional +1 Science while at least 3 Lessons remain stored.

Retain the installed CP University's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Domination** by optimizing **Lessons Written in Glass**. Reflection Guard fills a specialized tactical or exploration role; Chamber of Revision amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Reflection Guard using `Civilization_UnitClassOverrides` and Chamber of Revision using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Actual combat causality, post-combat attack consumption and defense-only tracking need verified hooks. UI must communicate player actions across Lua contexts; persist Lessons, cooldowns and timed effects.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
