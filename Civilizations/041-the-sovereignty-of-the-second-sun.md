# Daily Surprise Civ V #041 — The Sovereignty of the Second Sun

**Release:** 25 November 2026
**Motto:** "The night is merely an engineering problem."
**Theme:** Retro-futurist artificial sunlight and electrical infrastructure
**Leader:** Director Helia Lux
**Capital:** Noonfall
**Victory focus:** Science / Production
**Complexity:** 2/5
**Target:** BNW + Community Patch v151, human-only (Playable=1, AIPlayable=0).
**Status:** Archived design; implementation and gameplay unverified.

## Premise
A society convinced that sunsets are an unacceptable interruption to business builds an artificial sun. Its first prototype is a desk lamp. Its eventual national project is an electrified industrial civilization. The artificial sun is lore, not a global lighting or climate simulation.

## UA — Abolish the Night
Every owned city with a completed Factory or Factory-class replacement gains +2 Science and +2 Gold per turn. Every owned city with a completed Research Lab or Research Lab-class replacement gains +2 Production per turn. Independent binary conditions; no stacking from duplicate buildings, no free electricity or strategic resources. Resistance and other normal yield restrictions remain in force.

## UU — Dynamo Corps (replaces Infantry)
Inherit the installed CP v151 Infantry's strength, movement, cost, technology, resource requirements, combat class and upgrade route. Grants +1 Movement while this unit type is active, and free Cover I (normal CP effect, retained on eligible upgrades). The extra movement is a base unit stat, not a transferable promotion. No other changes.

## UB — Midnight Exchange (replaces Stock Exchange)
Inherit the installed CP v151 Stock Exchange's cost, maintenance, prerequisites, specialist slots and all baseline effects. Add +2 flat Science and +1 flat Production per turn. No additional resource requirements or percentage modifiers.

## Example
A city with a Factory, Research Lab and Midnight Exchange gains +4 Science, +2 Gold and +3 Production per turn above ordinary CP yields, before normal modifiers. A city with none gains nothing. Flat yields do not scale with game speed; Marathon uses the normal longer construction and research costs.

## Strategy and balance
Ancient through Renaissance: entirely ordinary economy; prioritize growth, research and survival. Industrial: secure coal where required and build Factories to activate the first UA benefit. Modern onward: build Midnight Exchanges and Research Labs, protect industrial centers with mobile Dynamo Corps and pursue Science. Late activation is the principal weakness; no early military or growth advantage, no free buildings, and no direct spaceship production modifier. Balance is a proposal, not a tested claim.

## Implementation
Identifiers: CIVILIZATION_SECOND_SUN, LEADER_HELIA_LUX, TRAIT_ABOLISH_NIGHT, UNIT_DYNAMO_CORPS, BUILDING_MIDNIGHT_EXCHANGE.
Use SQL/XML class overrides; clone the active CP v151 Infantry and Stock Exchange definitions and relevant companion tables. Set Infantry Moves to baseline +1, add existing Cover I through Unit_FreePromotions; verify promotion eligibility and LostWithUpgrade. Add flat yields through Building_YieldChanges. Use Lua to resolve completed buildings by BuildingClass (including captured replacements), reconcile separate hidden dummy buildings for Factory and Research Lab conditions to exactly 0 or 1 per city. Check actual building counts, not production queues. Clear dummies from non-owner cities on capture and reconcile on owner turn and load. Standard BNW has no general trait conditional-on-building-class yield table; Lua is required. Verify CP v151 event names/signatures before using immediate construction/capture hooks; owner-turn reconciliation is the fallback and may delay visible updates. No custom DLL, global lighting simulation or Vox Populi dependency intended.

## Acceptance tests
Check no bonuses before industrialization; Factory only (+2 Science/+2 Gold); Lab only (+2 Production); both; Midnight Exchange alone (+2 Science/+1 Production); all three; captured class replacements; loss/sale of buildings where permitted; capture by another civ; save/reload; no duplicate dummy counts; Infantry upgrade loses extra base movement but retains Cover I where eligible; Standard and Marathon. Verify baseline cloning against installed CP v151.

## Diplomacy
Greeting: "Welcome to Noonfall. Please set your watch to noon. It will simplify your stay."
War: "We have reviewed your existence and found it insufficiently illuminated."
Attacked: "An attack at midnight? How quaint. We abolished midnight."
Defeat: "Someone... turn off the lights."
Trade: "We offer electricity, precision instruments, and a very aggressive desk lamp."
