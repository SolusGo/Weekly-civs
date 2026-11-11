# 020 — The Paleontological Directorate

> **Status:** Concept archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Paleontological Directorate** |
| Leader | Director Emeritus Othmar |
| Capital | Stratum Prime |
| Theme | Scientific republic devoted to fossils and archaeology |
| Preferred victory | Science / Culture |

## UA — The Earth Remembers
Each city with a Library BuildingClass gets +1 Science, and each city with a University BuildingClass gets +1 Culture. The two bonuses are independent and do not multiply with duplicate class entries.

## UU — Fossil Expedition
**Replaces:** Archaeologist

+1 Movement and +1 Sight. Each successfully completed excavation grants Science: Quick +17, Standard +25, Epic +38, Marathon +75.

Retain the installed Community Patch v151 Archaeologist's other statistics, prerequisites, costs, and upgrade path unless explicitly changed. Verify appropriate promotion fields.

## UB — Natural History Museum
**Replaces:** Museum

+2 Science and +1 Culture beyond the active CP Museum baseline.

Retain the installed CP Museum's other effects, prerequisites, maintenance, slots, and applicable companion-table values.

## Gameplay strategy
Pursue **Science / Culture** by optimizing **The Earth Remembers**. Fossil Expedition fills a specialized tactical or exploration role; Natural History Museum amplifies the civilization's central economy or culture. Bonuses above are in addition to regular CP baseline values. Consider map dependence, timing, and caps before claiming any design is balanced in competitive play.

## Codex implementation pointers
1. Register BNW civilization/leader in SQL/XML with `Playable=1` and `AIPlayable=0`.
2. Register Fossil Expedition using `Civilization_UnitClassOverrides` and Natural History Museum using `Civilization_BuildingClassOverrides`.
3. Preserve inherited CP values and companion-table data; no default full Vox Populi dependencies.
4. Reconcile conditional flat yields with invisible dummy buildings, setting exact 0/1 states rather than accumulating them. Save custom state persistently where required.
5. **Critical engine concern:** Verify the installed CP v151 archaeology completion event: site disappearance or unit death alone is insufficient proof. Deduplicate rewarded excavations and retain standard Artifact/Landmark mechanics.
6. Test owner-turn timing, game speeds, upgrades, captures, reloads, and special effect boundaries. Report any unavailable CP hook rather than silently substituting different mechanics.

## Archival provenance
Structured entry based on the detailed design discussed in ChatGPT. This is not a verbatim full dialogue/narrative transcript and does not establish that an installable mod has been built or tested.
