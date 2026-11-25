# Daily Surprise Civ V #042 — The Republic of Unfinished Wars

Release: 26 November 2026. Complexity: 3/5 (moderate). Target: BNW + Community Patch v151, Standard and Marathon. Human only: Playable=1, AIPlayable=0. Design archived; implementation and gameplay unverified.

## Identity and premise
Leader: Chancellor Trucewell. Capital: Ceasefire. Motto: "We win by knowing when to stop." A fictional republic founded by veterans who turned peace negotiations into a national institution. Focus: diplomacy and economic recovery, with limited defensive military strength.

## UA — The Peace Dividend
At each owner-turn callback, if at war with any living major civilization, reset the consecutive peaceful-turn counter to zero. Otherwise increment it by one. At 10 consecutive peaceful owner-turn samples on Standard (Quick 7, Epic 15, Marathon 30), activate +2 Gold and +1 Culture per turn in the capital only. The bonus remains until a sampled war or capital loss; transfer it to the current capital when applicable. City-state and barbarian wars do not count. Initial counter zero; no retroactive credit. This is deliberately sampled at owner turns, not a claim to detect every intra-turn war. No lump-sum rewards, no benefit from repeatedly declaring peace. 

## UU — Treaty Escort (Musketman)
Clone active CP v151 Musketman including strength, cost, tech, resources, movement, upgrade and baseline promotions. Add free Cover I and +1 intrinsic Movement. Cover I uses installed effect and persists where normal upgrade rules permit; extra base Movement disappears on upgrade. No other changes.

## UB — Reconstruction Office (Bank)
Clone active CP v151 Bank including cost, maintenance, tech, prerequisites, slots and all companion tables. Add permanent +1 Production and +1 Culture per turn in each city with the building. No conditional effects, no free building or discounts.

## Strategy and balance
Early: survive conventionally and maintain peace to earn modest capital yields. Midgame: mobile Treaty Escorts screen borders and deter ranged units; avoid unnecessary wars. Renaissance onward: Banks provide reliable rebuilding yields even during war. Six cities with Offices and active UA yield +6 Production, +7 Culture and +2 Gold per turn before modifiers. Capital-only UA avoids wide early snowballing; delayed UB and lost peace streak constrain aggression. On Marathon flat yields are unchanged; only streak duration scales. Not a simulated balance result.

## Implementation
Identifiers CIVILIZATION_UNFINISHED_WARS, LEADER_TRUCEWELL, TRAIT_PEACE_DIVIDEND, UNIT_TREATY_ESCORT, BUILDING_RECONSTRUCTION_OFFICE. SQL/XML class overrides and Unit_FreePromotions; clone installed baseline, avoid duplicate Cover I. Lua GameEvents.PlayerDoTurn (verify signature/order in CP v151), Teams:IsAtWar and living major player enumeration; use persistent player-keyed counter and last processed game turn via save data. Set dummy building count to exactly 0/1 in all cities, only current eligible capital gets it; clear on capture and load, reconcile every owner turn. No custom DLL required by design. BNW XML cannot express a consecutive peace streak; owner-turn sampling intentionally misses wars started and ended between samples. Yield activation timing relative to engine yield collection must be tested; document any one-turn delay. Use explicit speed table, default unknown speeds to Standard with warning.

Tests: peaceful turns 9/10 and Marathon 29/30; war resets; city-state wars ignored; multiple major wars; eliminated opponents; capital capture/relocation; save/load and duplicate callback; non-owner dummy cleanup; Musketman upgrades; Bank baseline and yields. 

## Diplomacy
Greeting: "Welcome to Ceasefire. We have already drafted the treaty in case this conversation goes badly."
War: "Our peace committee has reluctantly approved a temporary exception."
Attacked: "You have interrupted a perfectly good economic quarter."
Defeat: "At least the paperwork for our surrender is immaculate."
Trade: "We offer reconstruction loans. Please do not ask why we have so much experience."
