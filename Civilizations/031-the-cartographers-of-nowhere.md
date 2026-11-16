# 🎲 Daily Surprise Civ V #31 — The Cartographers of Nowhere

**Release:** 16 November 2026  
**Motto:** *A place does not truly exist until someone has drawn it.*  
**Complexity:** ★★★☆☆ — Moderate  
**Target:** Civilization V: Brave New World + Community Patch **v151** (not full Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Design status:** Archived concept; gameplay implementation unverified

## Identity

| Field | Value |
|---|---|
| Civilization | The Cartographers of Nowhere |
| Leader | Grand Surveyor Elian Vey |
| Capital | Meridian |
| Theme | Expeditions, discovery, mapping the unknown |
| Preferred victories | Science / Culture |
| Preferred maps | Continents, Terra, Fractal |

## Unique Ability — The Unfinished Atlas

- For every **10 qualifying, previously unseen land plots personally revealed** through the civilization's own units or city visibility, earn **+15 Science and +10 Culture** (Standard speed).
- Maximum **10 such rewards per technological era**. Unspent exploration progress carries into the next era.
- Quick ×0.67, Standard ×1, Epic ×1.5, Marathon ×3 for the one-time Science and Culture amounts (nearest integer).
- Map-trading, shared revelation, World Congress, and other civilizations' visibility **do not count as personally discovered**.
- This reward is a **one-time exploration yield**, not +15 Science/turn.

## Unique Unit — Pathfinder

**Replaces:** Scout

- Inherits the active CP v151 Scout's cost, Combat Strength, base movement and upgrade path.
- **+1 Sight**.
- **Ignores terrain movement costs** via an applicable existing promotion; does not bypass impassable tiles, closed borders, or embark/ocean restrictions.
- Unique Sight and movement properties persist through normal upgrades.

## Unique Building — Atlas House

**Replaces:** Library

- Retains all CP v151 Library effects and requirements.
- **+1 Science** permanently.
- **+1 Culture** after the civilization has revealed at least **100 total land plots** (regardless of reveal source).
- **+1 Gold** after the civilization has revealed at least **200 total land plots** (regardless of source).
- Each Atlas House independently receives the threshold bonuses. These are one-way thresholds, but keep counts correct through load.

## Gameplay example

At Standard speed, 50 qualifying newly revealed land plots give 5 rewards: +75 Science and +50 Culture, provided the era's 10-reward cap has not been reached.

## Recommended strategy

**Early:** Build Pathfinders and explore in different directions. Carefully protect them from Barbarians.

**Midgame:** Unlock naval exploration, chart new continents, and build Atlas Houses to activate knowledge thresholds.

**Late:** Once the map is substantially revealed, shift from one-off exploration yields to normal Science/Culture infrastructure.

## CP v151 feasibility and Codex implementation requirements

- Register civilization, leader, trait, texts, uniques and art using BNW-valid SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Keep the **active Community Patch baseline** for all unchanged unit/building properties, including upgrade paths and specialist/companion tables.
- Use Lua for checks that SQL/XML cannot represent, applying exact dummy building counts and verified unit promotions as appropriate.
- Never silently substitute weaker, stronger, or functionally different mechanics for a missing CP hook.

- **Major source-attribution limitation:** Standard reveal-state queries generally show *that* a plot is revealed, not *how*. Exact personal-discovery identification requires a verified CP v151 reveal event carrying provenance or carefully tested turn-source correlation; generic fog counts cannot distinguish shared map discovery.
- Track personally discovered land plot IDs persistently, avoid duplicate grants, enforce per-era cap and carry-over.
- Science grant must handle team tech completion/overflow; Culture and era-speed rewards must be accurate.
- Atlas House thresholds intentionally count *all revealed* land plots, unlike the UA.
- Reconcile site counts and dummy buildings after reload, capture, and threshold crossing; avoid promising perfect attribution if hooks lack it.

**Acceptance tests:** Standard and Marathon speed; save/reload; pillaging/terrain changes where relevant; city capture; unit upgrade; exact bonus caps; revalidation of applicable CP hooks; no dummy stacking or duplicate one-off rewards.

## Leader dialogue

> **Greeting:** Welcome to Meridian. Tell me, traveller, have you seen anything that isn't on my maps?

> **Declaration of war:** Your borders are merely lines on parchment. I intend to redraw them.

> **Defeat:** So many places... still left unseen.

---
*Provenance: This is a structured archive of the original Daily Surprise concept from the ChatGPT conversation, preserving its numerical gameplay design and key lore. It is not a verbatim export of all prose or an assertion that CP v151 has been tested.*
