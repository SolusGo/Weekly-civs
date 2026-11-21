# 🎲 Daily Surprise Civ V #038 — The Emberwatch Compact

**Release:** 22 November 2026  
**Theme:** A fictional federation of forest-fire stewards that treats controlled clearings as civic infrastructure  
**Motto:** *“We do not worship the flame. We decide where it stops.”*  
**Leader:** High Warden Sera Ashfall  
**Capital:** Cinderrest  
**Victory focus:** Culture / Science / Defensive Domination  
**Complexity:** ★★★★☆ (4/5, advanced Lua/SQL; no custom DLL intended)  
**Target:** Civilization V: Brave New World + Community Patch v151, **not** mandatory Vox Populi  
**Playability:** `Playable=1`, `AIPlayable=0`  
**Status:** Archived concept; implementation and CP v151 gameplay unverified.

## Premise

The Emberwatch Compact is a confederation of settlements living beside ancient forests. Rather than indiscriminately cutting trees or relying on supernatural fires, its people deliberately maintain clear corridors between settlements and woodlands. A Firebreak is simultaneously an emergency route, a community gathering ground, and a warning that wilderness is to be respected, not conquered.

## Unique Ability — The Line Holds

- Each city receives **+1 Culture for every two owned, unpillaged Firebreak improvements within three hexes**, capped at **+3 Culture per city**. This counts actual plots, **not worked plots**.
- If a city owns at least **three Forest-feature tiles within three hexes**, it receives **+1 Science**. This is binary and the Forest tiles need not be worked.
- The UA does not create real wildfire, destroy features, spread fires, or grant free yields on ordinary Forest plots.

The UA rewards maintaining both intact woodland and carefully spaced protective clearings. It cannot exceed +3 Culture and +1 Science per city.

## Unique Unit — Firewarden

**Replaces Worker.**

- **Production cost: 125% of the installed CP v151 Worker cost**, rounded up to an integer; all other base Worker traits and build capabilities are inherited.
- **Movement: CP v151 Worker movement +1**.
- Can construct the exclusive **Firebreak** improvement; ordinary Workers and captured foreign Workers cannot.
- No military Combat Strength or combat bonuses. Upgrades and captures must not duplicate or transfer exclusive build capability accidentally.

### Firebreak improvement (unique build supplied by the Firewarden)

This is the Firewarden's special construction ability, **not a third civilization unique slot**.

- **Build time:** 6 Worker-turns at the active CP v151 baseline WorkRate, before game-speed/work-rate modifiers; tune the Build's Time value to match the tested Worker rate.
- **Placement:** Owned, non-city land tiles only; **flat Grassland, Plains, or Tundra**, with **no Forest, Jungle, Marsh, resource, or existing improvement**; cannot be built on Hills. Must be adjacent to at least **one Forest-feature tile** at the time of construction.
- **Yield:** **+1 Production** on the Firebreak plot, only while the improvement is intact.
- Firebreaks **do not remove a Forest**; they occupy an already clear neighboring tile.
- Pillaging removes the improvement's Production yield and its contribution to the UA and UB. Repair restores the normal contribution. The Firebreak cannot coexist with a Farm, Mine, or other improvement.

## Unique Building — Smokehouse Archive

**Replaces Library.**

- Inherits **all active CP v151 Library effects**, tech prerequisites, maintenance, specialist slots, and other properties.
- **+1 Culture permanently**.
- **+1 Science per two owned, unpillaged Firebreak improvements within three hexes**, capped at **+2 Science per city**.
- Firebreaks need not be worked. The threshold is checked per city; the Archive is not required to activate the UA.

## Example

Cinderrest owns **five intact Firebreaks** within three hexes and **three Forest tiles**, and has a Smokehouse Archive:

- UA Culture: **+2** (floor(5/2), capped at 3).
- UA Science: **+1** (at least three Forests).
- Archive Science: **+2** (floor(5/2), capped at 2).
- Archive Culture: **+1**.
- Total civilization-specific city bonuses: **+3 Culture and +3 Science per turn**, plus **+1 Production on each intact Firebreak tile actually worked**, before normal terrain/Library yields.

A sixth Firebreak raises the UA Culture to +3 but does not increase the Archive Science above +2.

## Gameplay strategy

**Ancient–Classical:** Settle near mixed Forest and clear flat terrain. A Firewarden is a more expensive Worker, so choose sites carefully. Create two Firebreaks to begin the first Culture threshold, without sacrificing all productive Farms.

**Medieval–Renaissance:** Use Smokehouse Archives to translate the growing network into Science. Maintain three Forests near core cities to keep the UA's +1 Science. Defend the corridors and repair pillaged Firebreaks.

**Industrial–Information:** Build a conventional Culture or Science economy around the early advantage. Firebreak yields remain flat and cost valuable improvement slots, so the Compact should not overwhelm specialized late-game tile improvements.

**Weaknesses:** Poor on treeless maps and on sites with insufficient empty flatland. The exclusive Worker costs 25% more, and every Firebreak competes with a conventional improvement. No offensive unit or military damage bonuses.

## Implementation pointers (Codex-ready)

Suggested IDs:

```text
CIVILIZATION_EMBERWATCH_COMPACT
LEADER_SERA_ASHFALL
TRAIT_LINE_HOLDS
UNIT_FIREWARDEN
BUILDING_SMOKEHOUSE_ARCHIVE
IMPROVEMENT_EMBERWATCH_FIREBREAK
BUILD_EMBERWATCH_FIREBREAK
BUILDING_EMBERWATCH_UA_CULTURE_DUMMY
BUILDING_EMBERWATCH_UA_SCIENCE_DUMMY
BUILDING_EMBERWATCH_ARCHIVE_SCIENCE_DUMMY
```

1. Register the civilization, leader, trait, Worker replacement, Library replacement, unique improvement and unique Build in SQL/XML; set `Playable=1`, `AIPlayable=0`. Preserve the **installed CP v151** Worker and Library baseline, not an assumed vanilla baseline.
2. Register `Improvement_Yields` with +1 Production for the Firebreak. Use `Unit_Builds` so **only Firewardens** can perform the special Build. Check the actual CP v151 `Builds`, `Improvements`, `Improvement_ValidTerrains`, and feature/placement fields rather than guessing table columns.
3. **Major engine limitation:** The condition “adjacent to a Forest feature at build time” and the exact disallowed-feature/resource/owned-plot restrictions may not all be expressible in vanilla XML. Use a verified CP v151 `GameEvents.PlayerCanBuild` (or equivalent exposed build-validity hook) for placement checks. If no appropriate build-validation hook exists, this exact design **cannot be implemented faithfully with only XML/Lua**; do not silently allow unrestricted Firebreaks.
4. Lua should count **owned, intact improvements** and **owned Forest-feature plots** within three hexes of each city, then reconcile dummy buildings to the exact +Culture/+Science values. Firebreak improvements are **not worked-plot requirements**; only their tile Production requires working the plot.
5. Count plots by **actual city ownership** to avoid one Firebreak contributing to two overlapping cities; test city acquisition, ownership reassignment, pillage/repair, terrain-feature removal, unit capture, and reload.
6. Building replacement inherits the active CP Library; avoid granting Library effects twice. Save-safe recalculation should be idempotent and run on owner-turn boundaries and supported improvement/city events. Do not create fire-spread simulations, fake terrain changes, or custom DLL dependencies.
7. Verify Build time on Quick, Standard, Epic, and Marathon; a literal six-turn duration is a design target **at standard speed**, not a guarantee of a universal XML Time constant.
8. If the special Build is available to captured Firewardens, decide explicitly whether the captured unit retains its build ability; the intended design is **only Emberwatch-owned Firewardens**. Enforce through `PlayerCanBuild` and test capture. This is a further potential hook limitation.

**Acceptance tests:** No Firebreak on Forest, Hills, resource plots, foreign land, or tiles without adjacent Forest; only Firewarden can build; counts 0–7 produce the correct threshold values; repair and pillage toggle effects; unique Worker capture does not leak special construction; no duplicate dummies after reload; standard and Marathon speed.

## Diplomacy dialogue

- **Greeting:** “Welcome to Cinderrest. The trees are older than our laws, and considerably better at following them.”
- **Declaration of war:** “We drew a line to keep danger away from our homes. You have mistaken it for an invitation.”
- **When attacked:** “You brought torches into a forest nation? That is either bravery or spectacular ignorance.”
- **Defeat:** “The firebreak failed. May those who remain learn where we placed it wrongly.”
- **Trade offer:** “We offer timber, maps, and exceptionally strict safety regulations.”

---
*This is a complete design archive, not a verified CP v151 implementation.*
