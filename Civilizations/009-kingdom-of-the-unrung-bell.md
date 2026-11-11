# 009 — Kingdom of the Unrung Bell

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Kingdom of the Unrung Bell** |
| Leader | Keeper Sable |
| Capital | Stillhaven |
| Theme | Pacifism with a devastating retaliatory toll |
| Preferred victory | Culture / Defense |

## UA — Silence Before the Storm
For every five consecutive owner-turns at peace, gain one Quietude stack (maximum 3). Each stack gives +1 Culture in each city. When entering war, consume the stacks to activate Great Toll for five turns: +5%, +10%, or +15% Combat Strength on friendly land according to the number consumed.

## UU — Bellwarden
**Replaces:** Pikeman

+1 Sight and +15% Combat Strength in friendly territory, stacking with the Great Toll when eligible.

Retain the current Community Patch v151 Pikeman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Silent Belfry
**Replaces:** Temple

+1 Culture and +1 Science per current Quietude stack.

Retain the installed CP Temple's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture / Defense** by emphasizing the conditions of **Silence Before the Storm**, using **Bellwarden** for its specialized role, and constructing **Silent Belfry** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Persist peace streak, stack count, toll duration and war-start processing. Avoid multiple war triggers or infinite Great Toll. Verify friendly-land-only combat modifiers.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
