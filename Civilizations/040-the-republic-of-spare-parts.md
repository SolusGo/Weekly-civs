# 🎲 Daily Surprise Civ V #040 — The Republic of Spare Parts

**Date:** 24 November 2026  
**Theme:** Improvisational engineering, repair shops, and upgrading old machinery rather than discarding it  
**Leader:** Chief Mechanist Ada Rivet (fictional)  
**Capital:** Secondhand  
**Complexity:** ★★★☆☆ — Moderate (3/5)  
**Victory focus:** Science / Defensive Domination  
**Compatibility:** Civilization V: Brave New World + Community Patch v151; SQL/XML/Lua, no mandatory full Vox Populi  
**Human-only:** `Playable=1`, `AIPlayable=0`  
**Status:** Design archived; implementation and gameplay unverified

> “Nothing is obsolete until we've taken it apart.”

## Premise

The Republic of Spare Parts was founded by mechanics, salvagers, and apprentices who inherited a mountain of broken equipment after the collapse of an industrial kingdom. Rather than seek new resources, they learned to rebuild the old. Its engineers have become famous for fielding outdated-looking armies that inexplicably keep pace with the world's latest military technology. The republic believes the true measure of a machine is how often it can be improved.

## Unique Ability — A Second Life for Everything

- Each time an **owned land combat unit is successfully upgraded to a different unit type**, gain **+12 Science** at Standard speed.
- The reward applies to **at most six qualifying upgrades per era** (maximum +72 Science per era at Standard speed).
- Each *individual unit ID* may earn this reward **only once per era**, even if it upgrades through multiple types in the same era. It can qualify again in a later era after another legitimate upgrade.
- Rewards scale with game speed: Quick ×0.67, Standard ×1, Epic ×1.5, Marathon ×3, rounded to nearest integer.
- Purchased, gifted, captured, spawned, or newly trained units grant **no reward on acquisition**. Civilian, air, and naval upgrades do not qualify. Upgrades require the normal costs, resources, prerequisites, and upgrade rules; the UA does not discount them.
- Era limits reset on entering a new era; unused capacity does not carry forward. Only the human player's owned units count.

## Unique Unit — Retrofit Guard

**Replaces:** Pikeman.

- Same base Combat Strength, Production cost, Movement, prerequisites, resource requirements, and upgrade chain as the **installed CP v151 Pikeman**.
- **+1 Sight**.
- Begins with **Cover I** for the exact ranged-defense modifier defined by the installed CP v151 version.
- Its unique Sight promotion and Cover I persist through eligible normal upgrades, using the installed promotion persistence rules.
- No direct attack-strength increase, no upgrade cost discount, and no extra movement.

The Retrofit Guard protects the workshops while surviving ranged harassment. Upgrading it can activate the UA exactly as with any other eligible land combat unit.

## Unique Building — Refit Depot

**Replaces:** Workshop.

- Retains all normal CP v151 Workshop yields, specialists, maintenance, production cost, technology prerequisites, and building-class interactions.
- **+1 Production** permanently.
- **+1 Science** if the city owns at least **one improved, unpillaged Iron resource** within three hexes.
- **+1 additional Science** if the city owns at least **one improved, unpillaged Coal or Oil resource** within three hexes.
- Both Science conditions are binary; a city can gain at most **+2 Science** from these resource conditions.
- The resource need not be worked. The improvement must be appropriate and intact; a resource visible only after the relevant technology becomes known qualifies only when visible to the player.
- Strategic-resource conditions are checked independently of whether the player's current stockpile is positive.

## Numerical example

At Standard speed, upgrading six distinct eligible land combat units in the Renaissance era awards **6 × 12 = 72 Science**. A seventh upgrade in that era grants nothing. A Refit Depot city with one improved Iron and one improved Coal receives **+1 Production and +2 Science**, in addition to all CP Workshop effects.

## Gameplay strategy

**Ancient–Classical:** Build a sustainable army instead of repeatedly sacrificing units. The UA does not pay until upgrades become available. Expand to productive terrain and acquire Iron.

**Medieval–Renaissance:** Time legitimate upgrades around new military technologies. Six distinct upgrades can give a modest Science bump; Retrofit Guards can hold defensive lines while waiting for their next upgrade. Build Refit Depots in strategic-resource cities.

**Industrial–Information:** Coal and Oil improve the Refit Depot's conditional Science. Upgrades remain valuable but capped; the republic must still invest in conventional science and production infrastructure. Use an up-to-date army for defense or opportunistic conquest.

**Weaknesses:** Unit upgrades cost Gold and sometimes resources, so the UA is not free income. Civilizations with no accessible strategic resources lose the conditional Refit Depot bonus. The UA does not improve combat power directly and can be weak on peaceful, low-unit-count games.

## CP v151 implementation and limitations

1. Register civilization, leader, trait, unit and building in SQL/XML; set `Playable=1`, `AIPlayable=0`. Use the normal `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides` tables.
2. For upgrade detection, **verify whether CP v151 exposes a reliable pre/post unit-upgrade event** and whether it provides both the old and new unit identities. Standard BNW Lua does not universally guarantee a dedicated upgrade-complete callback. If missing, use a rigorously tested snapshot/reconciliation of unit ID, type and owner at owner-turn boundaries, with documented limitations for multiple upgrades in one turn; **do not award on unit training or spawning**.
3. Persist a ledger of unit IDs rewarded in the current era, the era reward count, and relevant upgrade snapshots. On upgrade, verify that the unit is owned by this civilization, is land combat, actually changed type, and has not already been rewarded this era. Check CP v151 behavior regarding whether upgrades preserve unit IDs. If IDs are replaced, use a verified upgrade event or provenance; never treat an arbitrary new unit as an upgrade.
4. Grant Science with verified research-progress APIs and test tech completion and overflow. Scale one-off reward by game speed, not per-turn dummy buildings.
5. Refit Depot resource Science can be implemented with reconciled dummy buildings, one each for Iron and Coal/Oil thresholds. Query the city's **actual owned plots** and visible improved strategic resources; avoid counting duplicate radius overlaps for two cities.
6. Preserve the active CP v151 Pikeman and Workshop baselines. Verify the Sight and Cover I promotions, upgrade persistence, and no mandatory full Vox Populi dependencies.
7. Test Standard and Marathon, multiple upgrades in one turn, disbanding/capture, unique unit upgrades, game reload, era transition, technology visibility, pillaging, city capture, and Science overflow.

**Engine feasibility:** The building and unit are straightforward with SQL/XML plus Lua. **Exact upgrade attribution is the key risk**: a missing reliable CP v151 upgrade hook or identity continuity may prevent full fidelity without a DLL change. If it cannot be verified, report this limitation and leave the UA incomplete rather than claiming it works.

## Diplomacy — Chief Mechanist Ada Rivet

**Greeting:** “Welcome to Secondhand. Please ignore the smoke. It means the workshop is functioning.”

**Declaration of war:** “You call our equipment obsolete? We'll send it back with improvements.”

**When attacked:** “Wonderful. More spare parts are being delivered directly to our borders.”

**Defeat:** “Don't scrap the republic. Give me one more turn with a wrench.”

**Trade offer:** “I can offer you a perfectly functional engine. Some assembly is required.”

---
*Design only; not a tested mod.*
