# 015 — The Hollow Choir

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Hollow Choir** |
| Leader | The First Note |
| Capital | Resonance |
| Theme | A civilization of singing mountain crystals |
| Preferred victory | Culture / Religion |

## UA — Songs Beneath Stone
A city founded on a Hill gains +1 Production. For each adjacent Mountain it gains +1 Faith, to a maximum of +2 Faith per city.

## UU — Chorus Sentinel
**Replaces:** Swordsman

+1 Sight and +20% Combat Strength when defending on Hills.

Retain the installed Community Patch v151 Swordsman's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Resonance Hall
**Replaces:** Amphitheater

+1 Culture and +1 Science for every two owned Mountain tiles within three tiles of the city, capped at +2 Science.

Retain the installed CP Amphitheater's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Culture / Religion** by optimizing **Songs Beneath Stone**. Chorus Sentinel fills a specialized tactical or exploration role; Resonance Hall amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Chorus Sentinel using `Civilization_UnitClassOverrides` and Resonance Hall using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Verify the installed CP can implement hill-only defensive combat (not attacking), count owned Mountains within a three-plot city radius, and preserve Amphitheater effects.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
