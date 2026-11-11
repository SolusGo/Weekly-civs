# 006 — The Wandering Circus

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Wandering Circus** |
| Leader | Ringmaster Aurelio |
| Capital | Grand Pavilion |
| Theme | Roaming performers and festivals |
| Preferred victory | Culture |

## UA — The Show Must Go On
A Carnival Crew that ends its turn in an eligible friendly city starts a three-owner-turn festival granting that city +3 Culture and +2 Gold. Per-city cooldown: 12 owner-turns from the festival start. Festivals cannot stack.

## UU — Carnival Crew
**Replaces:** Worker

+1 Movement; triggers the civic festival when ending a turn in an eligible city.

Retain the current Community Patch v151 Worker's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Ticket Office
**Replaces:** Market

+1 Culture always; +2 Production during the city's active festival.

Retain the installed CP Market's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture** by emphasizing the conditions of **The Show Must Go On**, using **Carnival Crew** for its specialized role, and constructing **Ticket Office** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Track festival start, expiration, and next eligible turn separately for each city; save the ledger. Use an owner-turn and unit-ended-turn hook confirmed for CP v151.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
