# 008 — The Lantern Fleet

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Lantern Fleet** |
| Leader | High Keeper Maren |
| Capital | First Beacon |
| Theme | Coastal lights and harbor protection |
| Preferred victory | Science / Culture |

## UA — No Harbor Goes Dark
A coastal city whose city-center tile is occupied by a friendly naval military unit at its owner-turn check gains +2 Science and +1 Culture while guarded.

## UU — Beacon Cutter
**Replaces:** Trireme

+1 Sight and +15% Combat Strength in friendly territory.

Retain the current Community Patch v151 Trireme's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Signal Lighthouse
**Replaces:** Lighthouse

+1 Culture, and +2 Gold while its city qualifies as a Guarded Harbor.

Retain the installed CP Lighthouse's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Science / Culture** by emphasizing the conditions of **No Harbor Goes Dark**, using **Beacon Cutter** for its specialized role, and constructing **Signal Lighthouse** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Verify whether naval units can occupy the city-center plot with the installed CP rules. If the city-center check is unsatisfiable, flag the design before coding; do not silently substitute an adjacent tile.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
