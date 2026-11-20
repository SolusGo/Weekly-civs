# 🎲 Daily Surprise Civ V #036 — The Velvet Menagerie

**Release:** 21 November 2026  
**Motto:** *“A kingdom is measured by what it chooses not to destroy.”*  
**Complexity:** ★★★☆☆ — Moderate  
**Target:** Civilization V: Brave New World + Community Patch **v151**, not full Vox Populi  
**Design status:** Archived concept; implementation and gameplay unverified  
**Human only:** `Playable=1`, `AIPlayable=0`

## Premise and identity

The Velvet Menagerie is a fictional league of naturalists, field biologists, and eccentric aristocrats who insist that wild animals are citizens of the realm. The royal census includes deer, foxes, elephants, and one exceptionally argumentative peacock. Rather than clearing every forest for farms, its people build a research economy around managed wildlife habitats.

| Field | Value |
|---|---|
| Civilization | The Velvet Menagerie |
| Leader | Curator-Regent Elowen Quill |
| Capital | Velvetgrove |
| UA | A Census of the Wild |
| UU | Habitat Ranger (Crossbowman) |
| UB | Royal Field Station (Zoo) |
| Victory focus | Science / Culture |
| Favored maps | Mixed forest, jungle, and plains with Camp resources |

## Unique Ability — A Census of the Wild

- Each **worked, owned, improved, unpillaged Camp resource** provides **+1 Science**, capped at **+3 Science per city**. This is a **city-level** bonus, not a permanent global tile yield change.
- A city working **at least two distinct resource types improved by Camps** receives **+1 Culture**. Two Deer tiles do not qualify; Deer plus Furs do. This is binary per city.
- The resources must be **valid Camps in the installed CP v151 ruleset**, not a hardcoded vanilla resource whitelist. The resource must be on the worked plot, the plot must be owned by the city, and the Camp improvement must be intact.
- No free Food, Production, or military strength is granted by the UA.

## Unique Unit — Habitat Ranger

**Replaces:** Crossbowman

- Inherits all active CP v151 Crossbowman base statistics: melee Combat Strength, ranged Combat Strength, range, movement, cost, resource requirements, and upgrade path.
- **+1 Sight**.
- **Ignores movement penalties from Forest and Jungle** via the normal Woodsman-style feature movement promotion, if the installed CP promotion supports both features; otherwise implement two feature-specific double-movement promotions with the same intended effect.
- No extra attack damage or free ranged promotions.
- The unique movement and Sight promotions persist through eligible normal upgrades. Impassable terrain and normal embarkation restrictions remain in force.

## Unique Building — Royal Field Station

**Replaces:** Zoo

- Retains the active CP v151 Zoo baseline, including prerequisites, maintenance, Happiness and other effects.
- **+2 Science** permanently.
- **+1 Culture** if the city is working **at least one owned, improved, unpillaged Camp resource**.
- Conditional Culture is binary; the permanent Science is not conditional.
- Does not grant extra Happiness beyond the CP Zoo baseline.

## Example

Velvetgrove works two Deer Camps and one Furs Camp, all owned, improved, and unpillaged, and has a Royal Field Station:

- UA: **+3 Science** (three eligible worked Camp resources; cap reached).
- UA: **+1 Culture** (two distinct Camp resource types: Deer and Furs).
- UB: **+2 Science** permanently and **+1 Culture** for at least one eligible worked Camp.
- **Total civilization-specific bonuses: +5 Science and +2 Culture per turn**, beyond ordinary tile, building and CP Zoo yields.
- If one of the Deer Camps is pillaged, the UA Science falls to +2; the distinct-type Culture remains as long as the Furs and at least one Deer Camp are worked. If the Furs Camp is pillaged, the distinct-type Culture is lost.

## Gameplay strategy

**Ancient–Classical:** Scout for Deer, Furs, Ivory, Truffles, or other CP-valid Camp resources. Found settlements with enough food and production to support working Camp plots. Prioritize improving and working different Camp resource types over clearing habitats indiscriminately.

**Medieval–Renaissance:** Use the Science from Camps to support technology progression. Habitat Rangers explore forests and jungles, protect valuable wildlife resources and respond to raids without becoming stronger ranged attackers than ordinary Crossbowmen.

**Industrial–Information:** Construct Royal Field Stations and use the permanent Science plus conditional Culture to support Science or Culture victories. On resource-poor maps, the UA can be weak; the Zoo replacement supplies a modest fallback.

**Weaknesses:** Terrain/resource dependence; no direct Production or Happiness boost beyond the standard Zoo; early Science requires citizens to work Camps; distinct-type Culture is not activated by duplicate resource copies.

## Codex-ready identifiers

```text
CIVILIZATION_VELVET_MENAGERIE
LEADER_ELOWEN_QUILL
TRAIT_CENSUS_OF_THE_WILD
UNIT_HABITAT_RANGER
BUILDING_ROYAL_FIELD_STATION
```

## Implementation pointers and meaningful engine limitations

1. Register the civilization, leader, trait, unit, building, texts, and art in BNW-compatible SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`. Set `Playable=1`, `AIPlayable=0`.
2. Do **not** use a global `Improvement_Yields` or `Resource_YieldChanges` entry for the UA: that would ignore worked ownership, pillaging, the **per-city cap**, and distinct resource types. Reconcile exact per-city Science/Culture through nonconstructible dummy buildings with fixed yields and controlled counts.
3. For each city, inspect worked plots (`city:IsWorkingPlot(plot)` or the equivalent verified API), plot owner/city assignment, improvement type, resource type, and pillage state. Determine valid Camp resources from the installed CP rules or validated plot improvement compatibility, not from a guessed hardcoded list.
4. Verify `PROMOTION_WOODSMAN` (or the CP-equivalent feature movement promotion) covers **both Forest and Jungle** in this version. If not, use verified feature-specific double-movement entries. No ability to ignore all terrain costs is intended.
5. Copy the **active CP v151** Crossbowman and Zoo baselines, including all extra tables, specialist interactions, upgrades, and CP-specific effects. The replacement must not accidentally strip CP additions.
6. Reconcile dummy buildings on citizen assignment, tile swaps, improvements/pillaging, city capture, and save/load. If no reliable tile assignment events are available, owner-turn reconciliation is acceptable but may create a documented one-turn UI delay.
7. Unit promotions should survive eligible upgrades. Verify promotion effects, no impassable bypass, and no ranged attack-strength bonus.
8. Test one versus two Camp resource types, two duplicate Deer Camps, three/four worked Camps and the cap, pillaged Camp, unworked Camp, city ownership changes, CP-specific Camp resources, Zoo prerequisites, and Marathon.

**Feasibility:** Standard BNW Lua/SQL/XML with CP v151 should suffice. No custom DLL or mandatory Vox Populi features are intended. The principal implementation risk is accurately tracking **worked, valid, unpillaged Camp resource plots** as citizen assignments change.

## Diplomacy and lore

**Greeting:** “Welcome to Velvetgrove! The wolves have approved your visit. The peacock remains undecided.”

**Declaration of War:** “You have burned our habitats. The forest has filed a complaint, and I am here to deliver it.”

**When attacked:** “Our animals are not your trophies. Rangers, defend the preserves!”

**Defeat:** “Promise me one thing... do not turn the last sanctuary into a parking lot.”

**Trade offer:** “We can offer Furs, Ivory, and an official certificate declaring your horse a distinguished foreign ambassador.”

---
*This is a concept archive, not a claim of tested CP v151 gameplay implementation.*
