# Daily Surprise Civ V #044 — The Commonwealth of Forgotten Names

**Date:** 28 November 2026  
**Motto:** *To be forgotten is not to have never existed.*  
**Leader:** The Nameless Archivist  
**Capital:** Remembrance  
**Theme:** Abstract fantasy; preservation of ordinary lives and archaeological history  
**Victory focus:** Culture / Science  
**Power spike:** Industrial Era  
**Complexity:** ★★★☆☆ — Moderate  
**Target:** Civ V BNW + Community Patch v151; human-only (`Playable=1`, `AIPlayable=0`)  
**Status:** Archived; implementation and gameplay unverified.

## Premise

The Commonwealth preserves the names of overlooked inventors, forgotten poets, unnamed soldiers and abandoned villages. Its leaders relinquish their own names on assuming office; the institution matters more than the ruler. Archaeological Artifacts are scientific evidence as well as cultural treasures.

## UA — Nobody Is Forgotten

Each Archaeological Artifact displayed in a Great Work slot in an owned city provides **+2 Science and +1 Culture per turn** to that city. Count a maximum of **four Artifacts per city** (maximum +8 Science/+4 Culture).

Artifacts obtained by excavation, trading or conquest qualify. Ordinary Art, Writing and Music do not; Landmark improvements do not. No additional Tourism modifiers or free Antiquity Sites.

## UU — Memory Seeker (Archaeologist replacement)

- Cost: 80% of installed CP v151 Archaeologist baseline, rounded to the nearest integer.
- Movement: baseline +1.
- Sight: baseline +1.
- Civilian, no combat strength.
- Technology, excavation speed, excavation options and consumption on successful excavation unchanged. Cannot excavate additional sites after normal consumption.

## UB — Hall of Ordinary Lives (Museum replacement)

Retains CP v151 Museum cost, maintenance, requirements, yields, Great Work slots and theming rules.
- **+1 Culture/turn** permanently.
- **+2 Gold per Archaeological Artifact displayed in this specific building.**
- Ordinary Art can occupy slots but grants no unique Gold. No extra slots.

With two Artifacts in a normal two-slot Hall, the UB alone grants +4 Gold and +1 Culture. With UA, that is +4 Science, +3 Culture and +4 Gold. Eight cities each containing such a Hall with two Artifacts produce +32 Science, +24 Culture and +32 Gold per turn in total, before baseline yields, theming or modifiers.

## Strategy and balance

Ancient–Classical: develop population, exploration and Science conventionally; no early UA. Medieval–Renaissance: prepare cultural infrastructure and secure diplomatic access to sites. Industrial: prioritize Archaeology, train Memory Seekers, construct Halls and claim accessible Antiquity Sites. Modern–Information: distribute Artifacts to balance the per-city cap, Hall Gold and theming; pursue Culture or Science. Weaknesses: very delayed activation (especially Marathon), finite contested Artifacts, no special military advantage.

## CP v151 implementation

Suggested identifiers: CIVILIZATION_FORGOTTEN_NAMES, LEADER_NAMELESS_ARCHIVIST, TRAIT_NOBODY_IS_FORGOTTEN, UNIT_MEMORY_SEEKER, BUILDING_HALL_ORDINARY_LIVES, BUILDING_DUMMY_FORGOTTEN_ARTIFACT, BUILDING_DUMMY_ARTIFACT_GOLD.

Use SQL/XML for registration and class overrides, clone active CP Archaeologist and Museum rows and associated tables, and adjust Units.Cost, Units.Moves, Units.BaseSightRange and Building_YieldChanges. Use gameplay Lua to enumerate occupied Great Work slots in each owned city, identify real Artifact class rather than generic Art-compatible slots, count city Artifacts capped at four, separately count Artifacts inside the Hall, and reconcile hidden dummy building yields to exact values. Remove obsolete bonuses on capture or ownership change; never add incremental stacks without reconciliation. Verify actual v151 Great Work slot and classification APIs: standard building tables cannot distinguish Artifact from ordinary artwork for these conditions. If sufficient information is unavailable, report that the exact mechanic is blocked rather than inventing hooks or silently substituting all Art. Owner-turn reconciliation is the fallback for Great Work transfers if no suitable event exists; displayed yields may lag until that check. No mandatory Vox Populi/custom DLL intended; feasibility remains subject to API validation.

## Acceptance tests

| Test | Expected unique yields/effect |
|---|---|
| Empty Hall, no other Artifacts | +1 Culture |
| Hall with two ordinary artworks, no other Artifacts | +1 Culture |
| Hall with one Artifact, no other Artifacts | +2 Science, +2 Culture, +2 Gold |
| Hall with two Artifacts, no other Artifacts | +4 Science, +3 Culture, +4 Gold |
| Five Artifacts in city | UA capped at four |
| Artifact transferred/traded | Reconcile bonuses and exact building-specific Gold |
| City capture | Remove previous owner's dummy bonuses |
| Reload | No duplicated bonuses |
| Marathon | Normal engine cost scaling, no double scaling |
| Completed excavation | Memory Seeker consumed normally |

## Diplomacy

**Greeting:** “Welcome, traveller. Before we discuss your empire, would you kindly spell your name? History has terrible handwriting.”

**Declaration of war:** “Your historians may omit what you have done. Ours will not.”

**Attacked:** “You may destroy our libraries, but we have made copies. An extraordinary number of copies.”

**Trade:** “You possess a vase belonging to a farmer who died three thousand years ago. We are prepared to negotiate extensively.”

**Defeat:** “When you write the history of this conquest, please remember the people who lived here.”

## Presentation

Emblem: The Book of the Unremembered, an open gold book and star on a dark circular field with gold rim. Colours: Archive Black #292733, Ancient Gold #C4AB72, Parchment #E5DDCB.

City names: Remembrance, Unwritten, Yesterday's End, Last Inscription, Quiet Testament, Evername, The Missing Page, Echohaven, First Witness, The Unforgotten.

*Condensed from the full Daily Surprise design; no implementation or gameplay verification claimed.*
