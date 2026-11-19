# 🎲 Daily Surprise Civ V #035 — The Calendar of Unofficial Holidays

**Release:** 20 November 2026  
**Motto:** *“Work can wait. The parade cannot.”*  
**Complexity:** ★★☆☆☆ — Simple / moderate  
**Target:** Civilization V: Brave New World + Community Patch v151 (not mandatory Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Status:** Design archived; mod implementation and CP compatibility unverified.

## Premise

The Calendar of Unofficial Holidays is a fictional parliamentary nation that turned administrative procrastination into a national art form. Every municipal disagreement is resolved by declaring a commemorative day. The resulting celebrations are absurdly frequent—but they also stimulate workshops, markets and civic participation.

The civilization is a **We Love the King Day (WLTKD)** specialist. It turns celebrations into a modest burst of Production, Science and Culture, but does not generate celebrations for free.

## Identity

| Field | Value |
|---|---|
| Civilization | The Calendar of Unofficial Holidays |
| Leader | Minister Pippa Day |
| Capital | Longweekend |
| Unique Ability | A Reason to Celebrate |
| Unique Unit | Parade Marshal (Pikeman) |
| Unique Building | Holiday Office (Colosseum) |
| Preferred victories | Culture / Science |
| Complexity | 2/5 |
| Map preference | Any, with diverse luxury resources |

## UA — A Reason to Celebrate

Each city currently experiencing **We Love the King Day** receives **+2 Production and +1 Science per turn**. These are **flat, binary city yields**, not percentage modifiers and not multiplied by the number of WLTKD triggers. The UA does not increase WLTKD duration or generate WLTKD by itself. The effects stop as soon as the city's celebration counter reaches zero.

**Balance:** No bonuses outside WLTKD, no Food, Happiness or combat bonus; the player must obtain the demanded luxury or otherwise trigger the celebration normally.

## UU — Parade Marshal (replaces Pikeman)

- **Base Combat Strength, production cost, movement, resource requirements and upgrades:** identical to the installed CP v151 Pikeman.
- **+1 Sight**.
- **+15% Combat Strength while defending in friendly territory**; does not apply on attack, outside friendly territory, or to ranged attack calculations.
- Both unique properties should persist through eligible normal upgrades.

The Parade Marshal's brightly colored parade shield makes a surprisingly serviceable defensive barrier. It is not stronger when attacking.

## UB — Holiday Office (replaces Colosseum)

- Retains **all** active CP v151 Colosseum effects, prerequisites, cost, maintenance and happiness.
- **+1 Culture** permanently.
- **+2 Gold per turn while the city is in WLTKD**.
- The conditional Gold is binary per city and is removed when WLTKD ends.

No extra Happiness is added, avoiding a feedback loop that would make celebrations trivial.

## Numerical example

Longweekend has a Holiday Office and is celebrating WLTKD. It receives **+2 Production and +1 Science** from the UA and **+1 Culture and +2 Gold** from the UB, beyond the ordinary Colosseum effects. On the next turn, when WLTKD expires, the +2 Production, +1 Science and +2 Gold disappear; the +1 Culture remains.

## Gameplay strategy

**Ancient–Classical:** Scout for luxury resources and trade opportunities. Develop ordinary Food and Production infrastructure, because the UA provides nothing when celebrations are absent. Parade Marshals can secure the homeland.

**Medieval–Renaissance:** Construct Holiday Offices, trade for the requested luxury resources, and time city development to exploit WLTKD bursts. Different cities may celebrate at different times.

**Industrial–Information:** Maintain luxury diversity and diplomacy to generate more celebrations. Use bursts to support infrastructure and Science, but do not rely on permanent WLTKD uptime. Culture victories benefit from the permanent +1 Culture per Holiday Office.

**Weaknesses:** Resource dependence, weak starts with scarce luxury diversity, no offensive strength, no early Science outside WLTKD, and small flat bonuses relative to late-game empires.

## CP v151 implementation pointers

1. Register `CIVILIZATION_UNOFFICIAL_HOLIDAYS`, `LEADER_PIPPA_DAY`, `TRAIT_REASON_TO_CELEBRATE`, `UNIT_PARADE_MARSHAL`, and `BUILDING_HOLIDAY_OFFICE` with standard BNW SQL/XML. Set `Playable=1`, `AIPlayable=0`.
2. Preserve the CP v151 Pikeman and Colosseum baselines via unit/building class overrides; do not hardcode vanilla values if the installed CP modifies them.
3. In Lua, check each owned city's current WLTKD counter (verify the exact CP v151 exposed method, e.g. `City:GetWeLoveTheKingDayCounter()`). Set **exact** dummy-building counts to provide +2 Production and +1 Science when counter > 0, and remove otherwise. Add the Holiday Office's +2 Gold only when the building exists and WLTKD is active. Its permanent +1 Culture can be a regular building yield.
4. Reconcile each owner-turn, on city acquisition, and after save/load. Turn-boundary reconciliation is sufficient for yield accuracy if performed before city yields are calculated. Do not add yields cumulatively every turn.
5. For Parade Marshal, verify a promotion/CP hook supporting **defense-only in friendly territory**. Standard friendly-land combat modifiers can apply on attack too; if a defense-only filter is unavailable, use a verified combat hook or flag the exact modifier as not implementable without extension. Do not silently substitute a generic +15% friendly-territory combat bonus.
6. Do not claim WLTKD trigger callbacks are needed: polling the celebration counter suffices. No custom DLL or mandatory VP dependency is intended, conditional on the defensive combat modifier being available.

**Acceptance tests:** City with/without WLTKD; holiday office present/absent; WLTKD expiry and retrigger; city capture; save/load; multiple cities with independent counters; CP Pikeman upgrades; friendly defense vs friendly attack; Standard and Marathon speeds; ensure no duplicated dummy yields.

## Leader diplomacy

**Greeting:** “Welcome to Longweekend! You've arrived just in time for National Arriving Just in Time Day.”

**Declaration of war:** “You have interrupted our celebrations. We hereby declare tomorrow National Retaliation Day.”

**When attacked:** “An invasion? But the entire army has already booked annual leave!”

**Defeat:** “We request that our surrender be observed as a public holiday.”

**Trade offer:** “Would you exchange your Spices for our finest commemorative calendar? Every page is a holiday.”

---
*Archived design, not an installable mod. Historical claims: none; fictional comedic civilization.*
