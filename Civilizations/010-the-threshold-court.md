# 010 — The Threshold Court

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Threshold Court** |
| Leader | Queen Elsewhere |
| Capital | First Door |
| Theme | Magic doorways between cities |
| Preferred victory | Domination / Culture |

## UA — A Door in Every Wall
Once per owner-turn, teleport one eligible land melee unit from an owned city with a Threshold House to another owned city with a Threshold House. Source city cooldown: eight owner-turns. Cost: 50 Gold plus 25 Gold per era index. Exhaust the unit's remaining moves and attacks.

## UU — Hingeguard
**Replaces:** Pikeman

+1 Movement and +15% Combat Strength in friendly territory.

Retain the current Community Patch v151 Pikeman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Threshold House
**Replaces:** Market

+1 Culture and participates as a teleport-network endpoint.

Retain the installed CP Market's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Domination / Culture** by emphasizing the conditions of **A Door in Every Wall**, using **Hingeguard** for its specialized role, and constructing **Threshold House** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Provide a verified UI for selecting a source unit and target city. Validate placement, occupancy, combat, movement exhaustion, Gold transaction, per-origin cooldown, and save safety; use CP hooks only if present.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
