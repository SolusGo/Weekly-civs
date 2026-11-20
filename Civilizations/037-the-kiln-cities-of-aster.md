# 🎲 Daily Surprise Civ V #037 — The Kiln Cities of Aster

**Release:** 21 November 2026  
**Motto:** *“Fire makes the fragile endure.”*  
**Complexity:** ★★★☆☆ — Moderate (Lua city reconciliation, no custom UI)  
**Target:** Civilization V: Brave New World + Community Patch v151, **not mandatory full Vox Populi**  
**Playability:** `Playable=1`, `AIPlayable=0`  
**Status:** Archived concept; gameplay implementation and CP v151 compatibility unverified.

## Theme and identity

A fictional league of rival ceramic city-states where every civic milestone is immortalised in fired clay. Their workshops turn common stone into architectural prestige; their disciplined kiln guards protect the vulnerable supply of artisans and fuel. The league values permanence more than conquest, and its artisans insist that a poorly fired vase is a national emergency.

| Field | Value |
|---|---|
| Civilization | The Kiln Cities of Aster |
| Leader | First Kilnmaster Ilyra Venn |
| Capital | Aster |
| Unique Ability | Fired Into History |
| Unique Unit | Kiln Guard (Spearman replacement) |
| Unique Building | Civic Kiln (Workshop replacement) |
| Victory focus | Culture / Science |
| Preferred terrain | Hills, Stone and Marble resources |

## UA — Fired Into History

- Each city **working at least one owned, unpillaged Quarry improvement** gains **+1 Culture per turn**. This is a **binary per-city** bonus, not per Quarry.
- Each city with a **completed Workshop or its replacement** gains **+1 Science per turn**. The Science bonus is binary and is not multiplied by the number of Quarries.
- These bonuses are independent. A city with a Quarry and a Workshop receives both.
- A Quarry is determined by its actual improvement type (`IMPROVEMENT_QUARRY`), not by Stone/Marble resource presence alone. Quarries on valid mod-added resources qualify; unimproved Stone/Marble do not.

## UU — Kiln Guard (replaces Spearman)

- **Combat Strength:** identical to installed CP v151 Spearman.
- **Cost, Movement, resource requirements, upgrades, and all other properties:** identical to installed CP v151 Spearman.
- **+1 Sight**, granted through a verified promotion that survives normal upgrades.
- **+15% Combat Strength when defending in friendly territory**, never when attacking. Implement with a CP v151 promotion or reliable combat hook that can distinguish defense from attack and territory ownership.
- The bonus does not apply in neutral, allied city-state, or foreign territory; the friendly territory is territory belonging to the unit's player.

## UB — Civic Kiln (replaces Workshop)

- Retains **all installed CP v151 Workshop** effects, costs, technology requirements, maintenance, specialist slots, and relevant building-class interactions.
- **+1 Culture** permanently.
- **+1 Production per worked, owned, unpillaged Quarry**, capped at **+2 Production per city**. This applies only while the Civic Kiln is present and the eligible Quarry is being worked.
- No additional bonuses from unworked or pillaged Quarries.

## Worked example

Aster works **two owned, unpillaged Quarries** and has built its Civic Kiln:
- **+2 Culture/turn:** +1 UA for having at least one qualifying Quarry, +1 Civic Kiln permanently.
- **+1 Science/turn:** +1 UA because it has the Workshop replacement.
- **+2 Production/turn:** Civic Kiln's capped Quarry bonus.
- All values are **in addition** to the ordinary CP Workshop and tile yields.

If one Quarry is unworked, the city still has the binary UA Culture and receives +1 instead of +2 unique Production. If both are unworked, it loses UA Culture and Quarry Production but retains +1 Culture from the Civic Kiln and +1 Science from the Workshop-based UA.

## Gameplay strategy

**Ancient–Classical:** Prioritise Stone/Marble Quarry access and productive Hills. Aster's early Culture rewards working at least one Quarry, but weak Food can punish overspecialisation. Kiln Guards hold defensive lines; they have no offensive combat advantage.

**Medieval–Renaissance:** Build Civic Kilns and keep up to two Quarries worked per city for extra Production. Workshops also activate the UA's Science bonus. Focus on Wonders, infrastructure, and social policies rather than conquest.

**Industrial–Information:** Use the accumulated Culture and modest Science/Production benefits to support a Culture victory, or transition to Science. The flat yields deliberately taper in relative value late game.

**Weaknesses:** Requires workable Quarries for the main synergy; no free Food, Gold, Happiness, or offensive power. Maps with scarce Stone/Marble reduce the UA and UB effectiveness.

## CP v151 implementation / Codex pointers

Suggested IDs:
```text
CIVILIZATION_KILN_CITIES_ASTER
LEADER_ILYRA_VENN
TRAIT_FIRED_INTO_HISTORY
UNIT_KILN_GUARD
BUILDING_CIVIC_KILN
PROMOTION_KILN_GUARD_WATCH
PROMOTION_KILN_GUARD_DEFENDER
```

1. Register the civ, leader, trait, texts, UU, UB, art placeholders and BNW-valid overrides via XML/SQL. Set `Playable=1`, `AIPlayable=0`. Preserve CP v151 Spearman and Workshop baselines, including any mod-added effects and specialist tables.
2. Count **worked**, **owned**, **unpillaged** `IMPROVEMENT_QUARRY` plots per city in Lua. Apply UA Culture (0/1) and UB Production (0/1/2) through idempotent dummy buildings. Do not globally alter Quarry yields: that would award yields to unworked Quarries and bypass the cap.
3. Detect the installed Workshop building class, including the Civic Kiln override, and apply UA Science (0/1) with an independent dummy. Reconcile when a Workshop is constructed, sold, replaced, or a city changes owner.
4. Add +1 Sight to Kiln Guards with a verified upgrade-persistent promotion. **Meaningful engine limitation:** standard friendly-territory combat modifiers can affect both attack and defense. Do **not** substitute a generic +15% modifier. Verify the CP v151 promotion schema or combat hooks for defense-only friendly-territory modifiers; if none is available, explicitly mark that single UU effect as requiring an extension or a revised design rather than claiming exact implementation.
5. For reconciliation, use reliable CP v151 city events plus an owner-turn fallback. Citizen assignment can change without a useful event; a turn-based fallback may produce a temporary UI lag. Do not allow dummy stacking or save/load duplication.
6. Test 0/1/2/3 worked Quarries, ownership swaps, pillaging/repair, citizen reassignment, multiple cities, Workshop/Civic Kiln recognition, city capture, unit upgrades, combat defense vs attack, Standard/Marathon speed, and save/reload. No custom DLL or UI is intended.

## Leader dialogue

**Greeting:** “Welcome to Aster. Mind the pottery. The last diplomat broke a bowl and caused a constitutional crisis.”

**Declaration of war:** “You may shatter our walls, but we shall fire new ones.”

**When attacked:** “An invasion? Someone move the porcelain!”

**Defeat:** “So this is what it feels like to be dropped before the glaze has dried.”

**Trade offer:** “We have excellent ceramics. Please refrain from asking whether they are dishwasher-safe.”

---
*Design archive only. Do not mark as an installed or tested mod without examining the actual CP v151 implementation.*
