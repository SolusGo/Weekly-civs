# 003 — The Twelfth Hour

> **Status:** Design archived; implementation not verified · **Target:** Civilization V BNW + Community Patch v151 · **Human-only:** `Playable=1`, `AIPlayable=0`

| Field | Detail |
|---|---|
| Civilization | **The Twelfth Hour** |
| Leader | Keeper of Seconds |
| Capital | Last Minute |
| Theme | Clockwork Grand Chimes |
| Preferred victory | Science / Production |

## UA — When the Clock Strikes
Every sixth owner-turn, a one-turn Grand Chime grants +75% Production and +50% Science to the civilization's cities. Use actual percentage modifiers, not flat yields.

## UU — Pendulum Guard
**Replaces:** Pikeman

+1 Movement and +15% Combat Strength in friendly territory.

Retain the current Community Patch v151 Pikeman's other values, requirements, abilities and upgrade route unless the above explicitly changes them. Verify the relevant promotion schema.

## UB — Municipal Clocktower
**Replaces:** Workshop

+1 Culture, plus +2 Production during an active Grand Chime.

Retain the installed CP Workshop's other effects, prerequisites, maintenance, specialist slots, and applicable companion-table data.

## Gameplay strategy
Build toward **Science / Production** by emphasizing the conditions of **When the Clock Strikes**, using **Pendulum Guard** for its specialized role, and constructing **Municipal Clocktower** where its bonuses apply. Treat yields as additional to normal CP baselines. Evaluate map dependence, timing, and any per-city or empire-wide cap before calling the design balanced.

## Codex implementation and limitations
- Register BNW-compatible civilization/leader metadata; human-only by default.
- Register unit and building through `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Use verified CP v151 XML/SQL fields and Lua hooks only. Preserve standard behavior when cloning uniques.
- **Mechanic-specific caution:** Determine exact chime period boundaries and game-yield timing. Prevent an extra chime after load; remove the percentage bonus immediately on expiration.
- Use persistent state where needed; per-city dummy bonuses must be idempotent and removed when conditions cease or the city is captured.
- Test in the *installed* CP v151: turn timing, save/load, city transfer, unit upgrades, edge conditions, and relevant game speeds.

## Provenance
Mechanics reconstructed from the retained original design specification. This archive is **not a verbatim transcription** of the full narrative or diplomacy dialogue, and it is **not evidence of an implemented or tested mod**.
