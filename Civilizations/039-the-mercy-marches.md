# 🎲 Daily Surprise Civ V #039 — The Mercy Marches

**Date:** 23 November 2026  
**Motto:** *“The wounded are not the forgotten.”*  
**Theme:** Borderland sanctuary, battlefield medicine, and disciplined defensive warfare  
**Leader:** Matron Caldra Vale (fictional)  
**Capital:** Havenford  
**Complexity:** ★★★☆☆ — Moderate (Lua-based healing and garrison reconciliation)  
**Victory focus:** Culture / Religion / Defensive Domination  
**Target:** Civilization V: Brave New World + Community Patch v151 only; no mandatory Vox Populi or custom DLL  
**Playability:** `Playable=1`, `AIPlayable=0`  
**Status:** Concept archived; not implemented or gameplay-tested

## Premise

The Mercy Marches are a federation of contested frontier settlements that learned to survive endless wars by sheltering the wounded, regardless of their former allegiance. Their matron-led orders maintain infirmaries, dispatch medical escorts, and insist that a soldier who returns home alive is worth more than a monument built in their memory. Their neighbors admire the compassion, but occasionally mistake it for weakness.

## Unique Ability — No One Left Behind

1. At the **start of each owner turn**, every **owned, living land combat unit** physically standing in **the Mercy Marches' own territory** with **1–49 HP remaining** (on the normal 100-HP scale) receives **+5 HP**, capped at its maximum HP. This is **additional healing**, independent of ordinary healing rules, and can trigger even if the unit moved or fought on the previous turn. It triggers at most once per unit per owner turn.
2. Each city with **Walls or a unique replacement of Walls** receives **+1 Faith per turn**. This bonus is binary, even if other defensive buildings are present.
3. The healing does **not** apply to embarked land units, naval units, aircraft, civilians, foreign units, or units outside owned territory. It does not restore dead units and does not apply when a unit has **50 or more HP** at the beginning of the check.

**Balance:** +5 healing only on badly wounded units in friendly territory; no offensive damage, production, science or empire-wide food boost. The Walls bonus is a modest religious incentive, not an instant faith engine.

## Unique Unit — White Banner Bearer

**Replaces:** Pikeman.

- Combat Strength, Production Cost, Movement, prerequisites, resource costs, obsolescence, upgrade path and other normal properties: **identical to the installed CP v151 Pikeman**.
- **+1 Sight**.
- Starts with **Medic I** for the normal CP v151 adjacent-unit healing effect, with the **actual healing magnitude inherited from CP v151** rather than invented.
- Sight and Medic I remain on eligible normal upgrades. The Medic effect does not stack with another identical Medic I on the same unit; follow CP promotion stacking behavior.
- No bonus against cities or on attack beyond the inherited Pikeman baseline.

## Unique Building — Wayside Infirmary

**Replaces:** Barracks.

- Retains **all** normal installed CP v151 Barracks effects, prerequisites, cost, maintenance, XP bonuses, and any specialist effects.
- **+1 Food** permanently.
- **+1 Culture** while an **owned, non-embarked land combat unit** is garrisoned on the city's centre plot. This is binary per city, independent of unit type or remaining HP.
- The Culture disappears when no eligible garrison remains, including after unit movement, death, or capture.

## Worked example

Havenford has Walls, a Wayside Infirmary, and a White Banner Bearer garrison. Its unique bonuses are **+1 Faith**, **+1 Food**, and **+1 Culture per turn**, plus the installed CP Barracks effects. A friendly land combat unit with 37 HP ending its turn on an owned non-city tile begins its next owner turn at 42 HP from the UA, before accounting for any normal healing; a unit at 51 HP receives no UA healing.

## Strategy

**Ancient–Classical:** Build defensive frontier cities and Barracks replacements to prepare garrisons. The UA's healing is useful immediately for retreating warriors, but does not make risky attacks profitable in enemy territory.

**Medieval–Renaissance:** Construct Walls for Faith and field White Banner Bearers in defensive formations. Rotate damaged units behind the line so they benefit from Medic support and the friendly-territory emergency healing.

**Industrial–Information:** Retain a resilient defensive core and develop conventional Science, Culture and military infrastructure. The +5 HP emergency heal becomes a smaller fraction of late-game unit durability, while Barracks Food/Culture remains modest.

**Weaknesses:** The UA does nothing for healthy units, for offensive armies outside your territory, or for embarked forces. There are no direct Science, Production, or trade bonuses.

## Codex-ready CP v151 implementation

Suggested IDs:
```text
CIVILIZATION_MERCY_MARCHES
LEADER_CALDRA_VALE
TRAIT_NO_ONE_LEFT_BEHIND
UNIT_WHITE_BANNER_BEARER
BUILDING_WAYSIDE_INFIRMARY
BUILDING_MERCY_WALLS_FAITH_DUMMY
BUILDING_MERCY_GARRISON_CULTURE_DUMMY
```

1. Register the civilization, leader, trait, city names, texts, and overrides with BNW-compatible SQL/XML. `Civilization_UnitClassOverrides` maps the Pikeman class to the White Banner Bearer; `Civilization_BuildingClassOverrides` maps the Barracks class to the Wayside Infirmary. Set `Playable=1`, `AIPlayable=0`.
2. Use CP v151's actual Pikeman and Barracks database rows as baselines; do not assume vanilla numeric combat values, XP percentages, or costs. Give the unique unit Sight +1 and verified CP Medic I promotion.
3. For the UA, on `GameEvents.PlayerDoTurn` (if verified in the installed CP build), enumerate owned units, select land combat units with `0 < currentHP < 50`, ensure not embarked and plot owner matches the civilization, and reduce damage by 5 (bounded at zero) through the verified unit damage API. **Check health before applying the heal.** Track one execution per owner turn; do not also run healing in unit-movement handlers.
4. For the Walls Faith, check the city's actual **Walls building class** (including replacements), not just a hardcoded `BUILDING_WALLS` type, and apply a **single +1 Faith dummy**. Reconcile on capture, demolition, construction, and load.
5. For the Infirmary garrison Culture, verify `City:GetGarrisonedUnit()` behavior in CP v151 or inspect the centre plot, filtering for owned non-embarked land combat units. Apply one +1 Culture dummy only if the city actually has the unique Infirmary and an eligible garrison.
6. Use idempotent dummy-building reconciliation; remove dummies when conditions fail or a city changes owner. Persist no mutable healing accumulator if the owner-turn event is already guaranteed once per player turn; otherwise store a per-unit turn guard in save-safe data.
7. **Engine limitations:** Standard BNW XML cannot represent this exact HP-threshold healing, unit type/territory filter, or conditional garrison Culture. Lua is required. CP v151 APIs must be validated for HP, unit domains, garrison state and event frequency. Natural healing and Medic I may apply in a different phase; **do not claim a fixed final HP total** unless event order is tested. Standard BNW does not simulate medicine or battlefield triage independently.
8. Tests: HP 1/49/50/51, move/fight before turn, embarked, foreign territory, unit upgrade, city centre garrison, missing Barracks replacement, captured city, Walls replacement, save/reload, Marathon speed, and simultaneous natural/Medic healing. Flat HP is deliberately **not** game-speed scaled.

## Leader diplomacy

**Greeting:** “Welcome to Havenford. If you have come in peace, there is bread. If you have come wounded, there is a bed.”

**Declaration of war:** “I had hoped never to meet you across a battlefield. Our healers will be ready for those you abandon.”

**When attacked:** “You threaten our sanctuary? Then you have given every patient a reason to stand.”

**Defeat:** “Take the walls, if you must. Leave the infirmaries standing.”

**Trade offer:** “We have spare bandages, grain, and a rather unreasonable belief in second chances.”

---
*Archived design specification, not a claim of implemented or verified CP v151 gameplay.*
