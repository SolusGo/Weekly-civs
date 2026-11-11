# 007 — Assembly of Scarecrows

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Assembly of Scarecrows** |
| Leader | Old Man Thistle |
| Capital | First Harvest |
| Theme | Sentient agricultural scarecrows |
| Preferred victory | Culture / Growth |

## UA — The Fields Have Eyes
A city with at least 3 owned unpillaged Farms within radius 3 receives +2 Culture and +1 Production. At 6 or more qualifying Farms it additionally receives +2 Food.

## UU — Wicker Sentinel
**Replaces:** Spearman

+1 Sight and +15% Combat Strength in friendly territory.

Retain the current Community Patch v151 Spearman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Harvest Bell
**Replaces:** Granary

+1 Culture, and +1 Gold per 3 qualifying owned Farms, capped at +3 Gold.

Retain the installed CP Granary's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture / Growth** by emphasizing the conditions of **The Fields Have Eyes**, using **Wicker Sentinel** for its specialized role, and constructing **Harvest Bell** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Count only owned, unpillaged Farms inside the city radius and avoid double counting. Update after improvement changes, pillaging, tile ownership changes, and load.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
