# Daily Surprise Civ V #043 — The Kingdom of the Borrowed Moon

**Date:** 27 November 2026  
**Motto:** *The tides belong to everyone. The moon belongs to us.*  
**Leader:** Queen Selene IX  
**Capital:** Moonharbour  
**Theme:** Maritime fantasy  
**Victory focus:** Science / Diplomacy  
**Preferred map:** Archipelago  
**Complexity:** ★☆☆☆☆ — Vanilla-style  
**Target:** Civ V BNW + Community Patch v151; human-only (`Playable=1`, `AIPlayable=0`)  
**Status:** Archived; implementation and gameplay unverified.

## Premise

The kingdom believes its ancestors borrowed the moon from the heavens and forgot to return it. Astronomers navigate by moonlight, merchants follow the tides, and the treasury maintains an account for eventual celestial repayment.

## UA — Celestial Navigation

All worked Coast and Ocean tiles provide **+1 Gold**, with or without resources or improvements. Unworked tiles generate no extra income. Lakes represented internally by TERRAIN_COAST also qualify intentionally. No free technologies, naval combat bonuses or extra trade routes.

## UU — Moonrunner (Caravel replacement)

- Cost: 90% of the installed CP v151 Caravel base cost, rounded to the nearest integer.
- Movement: baseline +1.
- Sight: baseline +1.
- Strength, prerequisites, resources, normal abilities and upgrade path: unchanged.
- Intrinsic Movement and Sight bonuses disappear on upgrade.

## UB — Lunar Observatory (Lighthouse replacement)

Retain all CP v151 Lighthouse effects, costs, maintenance, and requirements.
- **+1 Science/turn** permanently.
- **+1 Culture per worked Fish resource**; Fishing Boats are not required.
- No Mountain requirement; retain normal Lighthouse eligibility.

Example: eight cities each working six water tiles and two Fish with the UB receive +48 Gold, +16 Culture and +8 Science per turn in total, before ordinary yields and modifiers.

## Strategy and balance

Ancient–Classical: settle Fish-rich coasts, build Lunar Observatories, develop population. Medieval–Renaissance: pursue Astronomy; use Moonrunners to discover distant trading partners, islands and City-States. Industrial–Information: convert Gold into influence, protection and research infrastructure. Weaknesses: Production-poor water tiles and inland maps. No direct offensive bonuses.

## CP v151 implementation

Suggested identifiers: CIVILIZATION_BORROWED_MOON, LEADER_SELENE_IX, TRAIT_CELESTIAL_NAVIGATION, UNIT_MOONRUNNER, BUILDING_LUNAR_OBSERVATORY.

Use standard civilization/leader registration and unit/building class overrides. Clone active CP baseline rows and related tables, not vanilla hardcoded values. Use Trait_TerrainYieldChanges for Coast/Ocean if confirmed in the installed schema, Units.Moves, Units.BaseSightRange, Units.Cost and Building_YieldChanges for flat Science. Investigate Building_ResourceYieldChanges for Fish Culture, verifying that it affects worked Fish only. The intended SQL/XML-only implementation is subject to these schema and behavior checks; use minimal Lua if required to preserve exact yields rather than silently changing mechanics. No custom DLL or mandatory Vox Populi intended. Moon phases and tides are thematic only; shared Coast terrain cannot distinguish lakes. Preserve ordinary upgrade and cost scaling behavior.

## Acceptance tests

- Coast/Ocean/Lake worked versus unworked yields.
- Fish worked/unworked, with/without Fishing Boats, ordinary Lighthouse versus UB.
- Caravel cost, movement, sight and upgrade; verify no double game-speed scaling on Marathon.
- City capture, unique building conversion, save/load, coexistence with other civ packs.

## Diplomacy

**Greeting:** “Welcome to Moonharbour. Before we begin, you aren't here to collect the moon, are you?”

**Declaration of war:** “Your ambitions are considerably larger than your understanding of the tides.”

**Attacked:** “Mobilise the fleet! And hide the original lunar borrowing agreement!”

**Trade:** “We offer fish, silver and navigational charts. The moon itself is unfortunately not for sale.”

**Defeat:** “Very well. You may inherit the kingdom. You also inherit its outstanding celestial debts.”

## Aesthetics

Midnight Blue #142B50, Lunar Ivory #E4D6A7, Imperial Gold #C5A047.

*Condensed from the full Daily Surprise design; no implementation or gameplay verification claimed.*
