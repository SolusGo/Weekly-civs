# 012 — Republic of First Drafts

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Republic of First Drafts** |
| Leader | Editor-in-Chief Marginalia |
| Capital | First Edition |
| Theme | A culture of revisions, editing and publishing |
| Preferred victory | Culture / Science |

## UA — Nothing Is Ever Final
The first time the civilization completes each distinct eligible non-wonder constructible BuildingClass, it receives +12 Culture and +20 Gold at Standard game speed; scale for other speeds. Keep a permanent ledger of rewarded classes.

## UU — Ink Mortar
**Replaces:** Catapult

+1 Movement and +1 Sight.

Retain the current Community Patch v151 Catapult's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Revision Workshop
**Replaces:** Workshop

+1 Culture; +1 Science per four distinct eligible building classes in the city, capped at +3 Science.

Retain the installed CP Workshop's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Culture / Science** by emphasizing the conditions of **Nothing Is Ever Final**, using **Ink Mortar** for its specialized role, and constructing **Revision Workshop** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Use BuildingClass rather than building type; exclude wonders and dummy buildings. Save the historical class ledger to avoid exploits after sell, capture, or reload.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
