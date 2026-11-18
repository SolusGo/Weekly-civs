# 🎲 Daily Surprise Civ V #034 — The Chachapoya

**Release:** 19 November 2026  
**Motto:** *“Above the clouds, the stones remember.”*  
**Complexity:** ★★☆☆☆ — Vanilla-like (2/5)  
**Target:** Civilization V: Brave New World + Community Patch v151, SQL/XML/Lua  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Status:** Archived design only; not yet implemented or gameplay-tested

## Premise and identity

Inspired by the **Chachapoya peoples** of the cloud forests in what is now northern Peru, and their dramatic stone settlements such as Kuélap. This design is an imaginative strategy-game interpretation, **not a claim** that all Chachapoya communities were unified under a single historical ruler.

| Field | Value |
|---|---|
| Civilization | The Chachapoya |
| Leader | Guardian Yana (fictional representative leader) |
| Capital | Kuélap |
| Theme | Cloud-forest hill settlements, stone fortifications, and resilient highland agriculture |
| Victory | Culture / Defense |
| Complexity | ★★☆☆☆ (2/5) |
| Recommended terrain | Hills with nearby Forest and Jungle |

## Unique Ability — Cities Above the Clouds

- Every city **founded on a Hill** receives **+1 Culture**.
- Every city possessing **Walls or a unique Walls replacement** receives **+1 Science**.
- Both bonuses are independent; a hill-founded city with Walls receives both.
- The Hill condition checks the underlying city-center plot; the Science bonus uses the actual Walls **BuildingClass**, not a particular building type.
- Bonuses disappear if the city is captured by another civilization. Neither bonus scales with number of hills or wall copies.

## Unique Unit — Cloud Sentinel (replaces Composite Bowman)

- **Combat Strength:** inherit the installed CP v151 Composite Bowman's base melee defense.
- **Ranged Combat Strength:** inherit the installed CP v151 Composite Bowman's base ranged strength.
- **Movement, range, production cost, resources, prerequisites and upgrade path:** inherit the active CP v151 Composite Bowman baseline.
- **+1 Sight**.
- **+15% Combat Strength when defending on Hills**, applying to the unit's melee-defense calculation only, **not** to ranged attacks or offensive melee attacks.
- The Sight and hill-defense lineage bonuses persist through eligible normal upgrades.

The unit is a defensive archer, not a stronger offensive ranged unit. Verify the actual CP v151 promotion or combat-event mechanism for a **defense-only Hills** effect; do not silently substitute a generic Hills combat modifier.

## Unique Building — Cloud Terrace (replaces Granary)

- Retains all active CP v151 Granary effects, cost, prerequisites, maintenance, and applicable food/resource bonuses.
- **+1 Food** permanently.
- **+1 Production** if the city is **founded on a Hill**.
- The Production bonus is binary, not per Hill, and is lost on city transfer if no longer owned by the Chachapoya.

## Example: Kuélap

Kuélap is founded on a Hill, has a Cloud Terrace, and constructs Walls. Beyond its ordinary CP yields, the civilization grants **+1 Culture** (UA), **+1 Science** (UA), **+1 Food** (UB), and **+1 Production** (UB). Its Cloud Sentinel defends on a Hill with +1 Sight and +15% hill-only defensive strength.

## Gameplay strategy

**Ancient–Classical:** Found cities on Hills near Food sources, and build Cloud Terraces to offset the Food constraints of hill settlements. Archery and defensible choke points help early survival.

**Medieval–Renaissance:** Construct Walls to generate modest Science alongside defensive infrastructure. Use Cloud Sentinels to protect strategic Hills, while building ordinary Culture buildings.

**Industrial–Information:** Leverage the secure, culturally developed homeland toward a Culture victory. The civilization lacks strong empire-wide scaling or offensive bonuses and must keep pace with normal Science/Production investment.

**Weaknesses:** Hill-founded cities can be Food-poor; Walls cost Production and maintenance; Cloud Sentinels have no bonus to their ranged attacks. A flat +1 Science per walled city is modest in the late game.

## Codex-ready implementation

Identifiers:
```text
CIVILIZATION_CHACHAPOYA
LEADER_GUARDIAN_YANA
TRAIT_CITIES_ABOVE_CLOUDS
UNIT_CLOUD_SENTINEL
BUILDING_CLOUD_TERRACE
PROMOTION_CLOUD_SENTINEL_HILL_DEFENSE
```

1. Register civilization/leader with BNW-compatible SQL/XML; set `Playable=1` and `AIPlayable=0`.
2. Use `Civilization_UnitClassOverrides` for the Composite Bowman replacement and `Civilization_BuildingClassOverrides` for the Granary replacement. Clone all required companion-table effects from the **installed CP v151** baseline, not vanilla assumptions.
3. Implement hill-founded city Culture, Walls-class Science, and hill-founded Cloud Terrace Production with **idempotent city dummy buildings** or validated trait/building modifiers; check exact class ownership, not merely the presence of a Walls building ID.
4. Give the Cloud Sentinel a Sight promotion and a verified Hills **defense-only** promotion. If CP v151 lacks such a promotion, implement with a verified combat hook or flag the limitation rather than alter the effect.
5. Reconcile city dummy states after construction/sale, city capture, replacement building changes, and load. Avoid duplicate bonuses. Keep unit upgrade lineage correct.
6. Test flatland vs hill-founded cities; Walls and unique Walls replacements; defensive combat on Hills vs Plains; attacking vs defending; city capture; save/load; Standard and Marathon speeds.

**Engine limitations:** Stock BNW tables do not cleanly express every conditional city yield; Lua reconciliation is the safe fallback. The exact defense-only Hills modifier is the principal CP v151 compatibility check. No custom DLL, custom UI, or full Vox Populi dependency is intended.

## Leader and diplomacy

Guardian Yana is a **fictional representative leader** used to avoid claiming that the Chachapoya were a single monarchy.

**Greeting:** “Welcome to Kuélap. You have climbed far to reach us. I hope your intentions are lighter than your armor.”

**Declaration of War:** “You see a wall. We see a home. Come and learn the difference.”

**When attacked:** “You brought ladders to the clouds? How ambitious.”

**Defeat:** “Our stones may fall. Our mountains will not.”

**Trade Offer:** “We offer the treasures of the heights. Please do not ask us to deliver them downhill.”

---
*Concept only. The Chachapoya are real historical peoples; the leader and mechanical details are fictional game design.*
