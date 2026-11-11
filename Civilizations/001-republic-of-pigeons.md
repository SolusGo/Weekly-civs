# 001 — Republic of Pigeons

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **Republic of Pigeons** |
| Leader | Postmaster General Coo |
| Capital | Coopolis |
| Theme | Absurd messenger pigeons |
| Preferred victory | Science / Culture |

## UA — Messages on the Wing
Each outgoing land trade route grants its origin city +2 Science and +2 Culture; from the Renaissance onward the per-route bonus becomes +3 Science and +3 Culture.

## UU — Carrier Pigeon
**Replaces:** Scout

+1 Sight and ignores terrain movement costs.

Retain the current Community Patch v151 Scout's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Rooftop Roost
**Replaces:** Caravansary

+1 Culture; +2 Production if the city originates at least one active land trade route.

Retain the installed CP Caravansary's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Science / Culture** by emphasizing the conditions of **Messages on the Wing**, using **Carrier Pigeon** for its specialized role, and constructing **Rooftop Roost** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Track active trade routes by origin city and owner's era. Bonuses are *per active route*; the building's Production condition is binary.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
