# 004 — Kingdom of Saba

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Kingdom of Saba** |
| Leader | Karib'il Watar |
| Capital | Ma'rib |
| Theme | Historical South Arabian irrigated kingdom |
| Preferred victory | Culture / Science |

## UA — Where the Desert Blooms
Each city founded beside a river gains +1 Food and +1 Production; a city founded on Desert receives +1 Culture. Both effects may apply in the same city.

## UU — Wadi Sentinel
**Replaces:** Spearman

+15% Combat Strength on Desert or Hills and +1 Sight.

Retain the current Community Patch v151 Spearman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Ma'rib Cistern
**Replaces:** Water Mill

+1 Food and +1 Gold beyond the active CP Water Mill baseline.

Retain the installed CP Water Mill's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture / Science** by emphasizing the conditions of **Where the Desert Blooms**, using **Wadi Sentinel** for its specialized role, and constructing **Ma'rib Cistern** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Check underlying founding-plot terrain and river adjacency. Preserve the Water Mill class requirements; do not mistakenly grant it inland where the base building is disallowed.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
