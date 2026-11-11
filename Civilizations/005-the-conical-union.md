# 005 — The Conical Union

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Conical Union** |
| Leader | High Marshal Bollard |
| Capital | Permanent Detour |
| Theme | Sentient traffic cones and civil works |
| Preferred victory | Science / Domination |

## UA — Sorry for the Inconvenience
Each noncapital city connected to the Capital receives +2 Production and +1 Culture.

## UU — Road Crew
**Replaces:** Worker

+1 Movement and +25% Work Rate.

Retain the current Community Patch v151 Worker's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Detour Office
**Replaces:** Walls

+1 Culture; additionally +2 Gold in a connected noncapital city.

Retain the installed CP Walls's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Science / Domination** by emphasizing the conditions of **Sorry for the Inconvenience**, using **Road Crew** for its specialized role, and constructing **Detour Office** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Use the game's verified capital-connection test; recalculate after route disruption, reconnection, capture, and capital movement. Verify Work Rate modifier compatibility.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
