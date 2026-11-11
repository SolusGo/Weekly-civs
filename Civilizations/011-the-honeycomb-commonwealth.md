# 011 — The Honeycomb Commonwealth

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Honeycomb Commonwealth** |
| Leader | Speaker Mellia |
| Capital | First Comb |
| Theme | Bee civilization with communal plantations |
| Preferred victory | Science / Culture |

## UA — A Thousand Small Hands
Per city, each worked owned unpillaged Plantation gives +1 Production, capped at +4. If at least two such Plantations are worked, the city also gains +1 Culture.

## UU — Forager
**Replaces:** Scout

+1 Movement and +1 Sight.

Retain the current Community Patch v151 Scout's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Honey Exchange
**Replaces:** Market

+1 Food permanently; +1 Gold per two worked qualifying Plantations, capped at +2 Gold.

Retain the installed CP Market's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Science / Culture** by emphasizing the conditions of **A Thousand Small Hands**, using **Forager** for its specialized role, and constructing **Honey Exchange** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Check worked tiles (not merely improved tiles). Reconcile when citizens change assignments, tile ownership changes, or improvements are pillaged.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
