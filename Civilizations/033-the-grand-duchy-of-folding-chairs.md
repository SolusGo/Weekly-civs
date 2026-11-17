# 🎲 Daily Surprise Civ V #033 — The Grand Duchy of Folding Chairs

**Date:** 18 November 2026  
**Motto:** *“A seat for every citizen. A weapon for every emergency.”*  
**Leader:** Grand Duke Stackwell IV  
**Capital:** Seatopolis  
**Theme:** Absurd civic militarism; a prosperous nation whose entire political philosophy revolves around the folding chair  
**Victory focus:** Culture / Defensive Domination  
**Complexity:** ★★☆☆☆ (simple to moderate, no custom DLL intended)  
**Target:** Civilization V: Brave New World + Community Patch v151  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Status:** Concept archived; implementation and gameplay balance unverified

## Premise

Centuries ago, the duchy's parliament could not agree on who deserved the throne. To end the dispute, a carpenter produced an inexpensive folding chair and declared that every citizen could have a throne of their own. The duchy has since treated chairs as civic institutions, diplomatic gifts, emergency barricades, and, when necessary, weapons of war.

A civilization that converts **garrisoning cities into a cultural and industrial investment**. The central decision is whether to retain units at home for steady yields or send them away to fight.

## Unique Ability — The Right to Remain Seated

Every owned city with at least one **eligible land military combat unit garrisoned on its city-center plot** receives:
- **+2 Culture per turn**
- **+1 Production per turn**

Only one qualifying garrison is counted per city; multiple units never multiply the bonus. A civilian, embarked unit, naval unit, or aircraft does not qualify. The garrison unit must be owned by the duchy, be alive, and be capable of land combat. No bonus is earned while the city is empty, including immediately after the garrison leaves. No special yields in ungarrisoned cities.

For balance, the UA starts at full strength in the Ancient Era but costs military opportunity: every productive garrison is a military unit unavailable to project power. No direct Science, Food, Happiness, or global combat bonus.

## Unique Unit — Chair Marshal (replaces Spearman)

- Inherits **all active CP v151 Spearman base statistics**, production cost, movement, resource requirements, and upgrade path.
- **+1 Sight** through a unique promotion.
- Starts with the existing CP v151 **Cover I** promotion (its *actual installed* ranged-defense percentage; do not hardcode a guessed value).
- Both unique Sight and free Cover I remain through normal upgrades where promotion inheritance permits.
- No extra Combat Strength or Movement and no special combat-trigger Lua required.

The Chair Marshal protects public meetings, escorts furniture caravans, and survives ranged harassment while guarding settlements. The unique is defensive and does not increase early rushing power.

## Unique Building — Grand Assembly Hall (replaces Walls)

- Inherits all normal **CP v151 Walls** defense, city HP, cost, technology, maintenance, and other applicable companion-table effects.
- **+1 Culture per turn** permanently.
- **+1 Gold per turn** while the city has an eligible garrison under the UA's exact definition.
- The conditional Gold is binary and stops immediately when the garrison leaves or the city is captured.
- Does not create a free unit, change garrison maintenance, or alter unit stacking.

## Worked example

Seatopolis has a Chair Marshal garrisoned and a Grand Assembly Hall:
- UA: **+2 Culture and +1 Production**
- UB: **+1 Culture and +1 Gold**
- Total civilization-specific yield: **+3 Culture, +1 Production, +1 Gold per turn**.

If the Chair Marshal leaves, the city keeps only the Hall's permanent **+1 Culture**. Its UA bonuses and the Hall's conditional Gold disappear.

## Strategy

**Ancient–Classical:** Build enough Chair Marshals or ordinary land military units to garrison priority cities. Do not overexpand without a viable defensive budget. Build the Grand Assembly Hall in border cities.

**Medieval–Renaissance:** Use the steady Culture to accelerate social policies and the small Production bonus to improve infrastructure. Keep some units home while fielding a separate expeditionary army. Garrison replacement after upgrading is straightforward.

**Industrial–Information:** Continue a Culture victory with fortified cities or pivot into defensive conquest. Garrison yields are intentionally modest relative to late-game economies; the duchy must build normal science and specialist infrastructure to compete.

**Weaknesses:** Every productive city ties down a military unit; unit maintenance and opportunity costs matter. No free yields when a city is undefended, no early Science bonus, and no offensive military advantage.

## Codex implementation pointers

1. Register `CIVILIZATION_FOLDING_CHAIRS`, `LEADER_STACKWELL_IV`, `TRAIT_RIGHT_TO_REMAIN_SEATED`, `UNIT_CHAIR_MARSHAL`, `BUILDING_GRAND_ASSEMBLY_HALL`. Set `Playable=1`, `AIPlayable=0`.
2. Register uniques with `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`; clone **active CP v151** Spearman/Walls values, not vanilla BNW defaults. Verify promotion tables and the installed Cover I effect.
3. For the UA, check each owned city's center plot for a qualifying **friendly land military combat unit**. Use **idempotent dummy buildings** to apply exactly +2 Culture and +1 Production when qualified, and 0 when not. A garrison on an adjacent tile does not count.
4. The Hall's permanent +1 Culture can be XML/SQL. Its conditional +1 Gold uses a separate reconciled dummy building or a verified Lua-driven building yield.
5. **Engine limitation:** Standard building/trait XML cannot express the UA's exact land-military garrison predicate plus conditional yields. Lua is needed. CP v151's garrison API may classify units differently; verify `City:GetGarrisonedUnit()` behavior in the installed build and, if necessary, inspect the city-center plot's units with a strictly defined combat/domain filter.
6. Refresh bonuses on owner-turn start, unit movement into/out of a city, unit death, upgrade, capture, city creation, and save/load. If reliable unit-move hooks are absent, owner-turn reconciliation is an acceptable **turn-boundary** implementation; document that the UI may update on the next owner-turn rather than immediately.
7. Do not require Vox Populi or a custom DLL. Test empty city, civilian-only city, garrisoned Spearman, garrisoned Chair Marshal, unit upgrades, unit loss, city capture, and reload. Confirm the Hall's +1 Culture survives without a garrison and no dummy stacking occurs.

## Leader and diplomacy

**Grand Duke Stackwell IV** wears a tiny gilded folding chair as his ceremonial crown. He insists every visiting diplomat sit down before negotiations begin.

**Greeting:** “Welcome to Seatopolis! Please, take a seat. No, not that one. That is the throne.”

**Declaration of War:** “You have insulted our sovereignty. Prepare to be folded.”

**When attacked:** “They come for our chairs! Form the seating arrangement!”

**Defeat:** “My kingdom... collapsed. Much like an improperly secured hinge.”

**Trade offer:** “Our craftsmen have perfected the portable throne. Would you care for twelve thousand?”

## Archival note

This is a complete **design**, not a claim of implemented or tested mod files. Balance and CP v151 API behavior require validation before release.
