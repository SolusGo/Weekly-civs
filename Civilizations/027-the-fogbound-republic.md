# 🎲 Daily Surprise Civ V #27 — The Fogbound Republic

**Release:** 12 November 2026  
**Motto:** *What cannot be seen cannot be conquered.*  
**Complexity:** ★★☆☆☆ — Simple  
**Target:** Civilization V: Brave New World + Community Patch **v151** (not full Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Design status:** Archived concept; gameplay implementation unverified

## Identity

| Field | Value |
|---|---|
| Civilization | The Fogbound Republic |
| Leader | First Warden Mirelle |
| Capital | Greyfen |
| Theme | Swamp cities, hidden approaches, wetland science |
| Preferred victories | Science / Domination |
| Preferred maps | Marsh-rich riverlands |

## Unique Ability — The Living Mist

- Every **worked, unpillaged Marsh** tile contributes **+1 Science**, capped at **+4 Science per city**.
- A city with at least **two owned Marsh tiles within three hexes** receives **+1 Culture** (they need not be worked).
- Eligible military units receive **+10% Combat Strength when defending on Marsh**.
- All bonuses are additional to ordinary Civ V tiles/buildings. The Science cap is **per city**; the defensive effect is **not an all-terrain bonus**.

## Unique Unit — Fen Stalker

**Replaces:** Scout

- Same CP v151 Scout Combat Strength, production cost, base Movement, and upgrade route.
- **+1 Sight**.
- **Double movement on Marsh** through a verified feature-specific movement modifier.
- **+15% Combat Strength when defending on Marsh**, in addition to the UA's defensive bonus, for **+25 percentage points of nominal combat modifiers** before other calculations.
- Preserve the *unique* applicable bonuses through normal upgrades, but do not allow passage through impassable terrain.

## Unique Building — Marsh Conservatory

**Replaces:** Library

- Inherits the active CP v151 Library's normal effects and requirements.
- **+1 Science** permanently.
- **+1 Food** while the city owns at least **two Marsh tiles** within three hexes.
- **+1 additional Science** while the city owns at least **four Marsh tiles** within three hexes.
- Each threshold is binary; additional tiles beyond a threshold cannot stack the same benefit.

## Gameplay example

Greyfen works three Marsh tiles and owns at least two: the UA yields +3 Science and +1 Culture. A Marsh-defending Fen Stalker has the UA's +10% plus its unique +15% defensive modifier.

## Recommended strategy

**Early:** Found defensible river-marsh settlements with enough Hills or Forests for Production; scout waterways with Fen Stalkers.

**Midgame:** Construct Marsh Conservatories and work Marsh plots deliberately while preserving Food and Production growth.

**Late:** Convert the wetland Science advantage into research and a conventional modern army; avoid fighting off Marsh where the defensive advantage vanishes.

## CP v151 feasibility and Codex implementation requirements

- Register civilization, leader, trait, texts, uniques and art using BNW-valid SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Keep the **active Community Patch baseline** for all unchanged unit/building properties, including upgrade paths and specialist/companion tables.
- Use Lua for checks that SQL/XML cannot represent, applying exact dummy building counts and verified unit promotions as appropriate.
- Never silently substitute weaker, stronger, or functionally different mechanics for a missing CP hook.

- In Civ V, **Marsh is a feature, not terrain**. Generic terrain defense or movement modifiers cannot be substituted without changing the mechanics.
- Verify CP v151 feature-specific defensive and double-movement promotion support, or a reliable combat hook; if absent, flag the feature-specific effect rather than claim a complete implementation.
- Use worked-plot counting for capped Science, owned-plot counting for Conservatory thresholds. A global tile yield change would ignore the city cap.
- Reconcile on citizen assignment, improvements, city capture, fog updates, feature removal, and load. No DLL or custom UI intended.

**Acceptance tests:** Standard and Marathon speed; save/reload; pillaging/terrain changes where relevant; city capture; unit upgrade; exact bonus caps; revalidation of applicable CP hooks; no dummy stacking or duplicate one-off rewards.

## Leader dialogue

> **Greeting:** Welcome to Greyfen. Stay on the wooden paths. The marsh has a habit of remembering those who wander.

> **Declaration of war:** You have studied our borders. You have counted our soldiers. But you have forgotten to count the marsh.

> **Defeat:** The fog lifts... and for the first time, I can see the end.

---
*Provenance: This is a structured archive of the original Daily Surprise concept from the ChatGPT conversation, preserving its numerical gameplay design and key lore. It is not a verbatim export of all prose or an assertion that CP v151 has been tested.*
