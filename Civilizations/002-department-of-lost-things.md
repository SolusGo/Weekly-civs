# 002 — Department of Lost Things

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Department of Lost Things** |
| Leader | Chief Registrar Nobody |
| Capital | Unclaimed |
| Theme | Supernatural lost-property office |
| Preferred victory | Culture / Science |

## UA — Nothing Is Ever Truly Lost
Eligible combat kills near an owned city generate one Recovered Curio for that city, to a maximum of 4 per city; every Curio produces +1 Culture and +1 Science in its city.

## UU — Retrieval Officer
**Replaces:** Spearman

+1 Sight and +15% Combat Strength against Barbarians.

Retain the current Community Patch v151 Spearman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Lost Property Office
**Replaces:** Library

+1 Culture and +1 Gold per Recovered Curio in the city.

Retain the installed CP Library's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture / Science** by emphasizing the conditions of **Nothing Is Ever Truly Lost**, using **Retrieval Officer** for its specialized role, and constructing **Lost Property Office** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Persist a per-city Curio ledger. Verify proximity, combat-kill hook, ownership, capture, and razing behavior. Never reward a disband.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
