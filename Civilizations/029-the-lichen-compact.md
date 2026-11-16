# 🎲 Daily Surprise Civ V #29 — The Lichen Compact

**Release:** 14 November 2026  
**Motto:** *We do not conquer the wilderness. We learn to endure alongside it.*  
**Complexity:** ★★☆☆☆ — Vanilla-like  
**Target:** Civilization V: Brave New World + Community Patch **v151** (not full Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Design status:** Archived concept; gameplay implementation unverified

## Identity

| Field | Value |
|---|---|
| Civilization | The Lichen Compact |
| Leader | Elder Thallia |
| Capital | Symbiosis |
| Theme | Cold-country survival inspired by lichen symbiosis |
| Preferred victories | Science / Culture |
| Preferred maps | Cold Tundra and Snow regions |

## Unique Ability — The Art of Endurance

- **Worked Tundra** tiles provide **+1 Food**, capped at **+4 Food per city**.
- **Worked Snow** tiles provide **+1 Science**, capped at **+3 Science per city**.
- A city **founded on Tundra or Snow** receives **+1 Culture**.
- Identify Tundra/Snow by **underlying terrain**, not feature; hills do not disqualify. No direct military or Production bonus.

## Unique Unit — Stonewalker

**Replaces:** Scout

- Retains CP v151 Scout base Combat Strength, cost, Movement and upgrade route.
- **+1 Sight**.
- **Double movement in Tundra** and **double movement in Snow**.
- Unique terrain-movement promotions persist through normal upgrades; impassable terrain stays impassable.

## Unique Building — Symbiotic Garden

**Replaces:** Granary

- Retains the installed CP v151 Granary's normal effects and construction requirements.
- **+1 Food** permanently.
- **+1 Science** if the city owns at least **three Tundra/Snow tiles** within three hexes.
- **+1 Culture** if the city owns at least **six Tundra/Snow tiles** within three hexes.
- Conditional bonuses are each binary, irrespective of worked status.

## Gameplay example

Symbiosis is founded on Tundra, works 3 Tundra + 2 Snow plots, owns 6+ cold tiles, and has a Symbiotic Garden: unique bonuses total +4 Food (3 UA +1 UB), +3 Science (2 UA +1 UB) and +2 Culture (1 UA +1 UB).

## Recommended strategy

**Early:** Settle cold rivers with Hills or resources; scouts explore tundra/snow efficiently. Gardens help counter poor Food.

**Midgame:** Use cold-tile worked yields to grow and research while investing in ordinary buildings.

**Late:** Transition into Science or Culture; lack of combat/Production bonuses requires diplomacy, defensive terrain, and normal development.

## CP v151 feasibility and Codex implementation requirements

- Register civilization, leader, trait, texts, uniques and art using BNW-valid SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Keep the **active Community Patch baseline** for all unchanged unit/building properties, including upgrade paths and specialist/companion tables.
- Use Lua for checks that SQL/XML cannot represent, applying exact dummy building counts and verified unit promotions as appropriate.
- Never silently substitute weaker, stronger, or functionally different mechanics for a missing CP hook.

- Terrain yield tables do not express the **capped per-city *worked* tile** mechanic; use Lua census and reconciled dummy yields.
- The UB uses **owned** plot counts, not worked counts. Handle tiles that are in multiple city radii using actual city ownership policy.
- Verify CP terrain double-movement promotions survive upgrades.
- Reconcile after city/citizen changes and reload; no custom DLL or UI needed.

**Acceptance tests:** Standard and Marathon speed; save/reload; pillaging/terrain changes where relevant; city capture; unit upgrade; exact bonus caps; revalidation of applicable CP hooks; no dummy stacking or duplicate one-off rewards.

## Leader dialogue

> **Greeting:** A lichen is neither one creature nor truly alone. Perhaps your people will understand this wisdom.

> **Declaration of war:** We have endured winters that swallowed kingdoms. We shall endure you.

> **Defeat:** Even now... life will find a way to return.

---
*Provenance: This is a structured archive of the original Daily Surprise concept from the ChatGPT conversation, preserving its numerical gameplay design and key lore. It is not a verbatim export of all prose or an assertion that CP v151 has been tested.*
