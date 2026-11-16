# 🎲 Daily Surprise Civ V #30 — The Glass Orchard

**Release:** 15 November 2026  
**Motto:** *Even the desert can bear fruit, if one learns to harvest the sun.*  
**Complexity:** ★★★☆☆ — Moderate  
**Target:** Civilization V: Brave New World + Community Patch **v151** (not full Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Design status:** Archived concept; gameplay implementation unverified

## Identity

| Field | Value |
|---|---|
| Civilization | The Glass Orchard |
| Leader | First Gardener Solenne |
| Capital | Sunspire |
| Theme | Solar greenhouses and desert agriculture |
| Preferred victories | Science / Culture |
| Preferred maps | Desert with rivers and some Production |

## Unique Ability — Harvest the Sun

- Each **worked, unpillaged Desert tile** provides **+1 Food**, capped at **+4 Food per city**.
- Each city **founded on Desert** receives **+1 Science**.
- While at peace with every major civilization, a city working **at least three Desert tiles** receives **+2 Gold**. The Gold vanishes during any major-civilization war and returns with peace.
- Desert Hills and Desert beneath Flood Plains qualify by their underlying terrain; other terrain does not.

## Unique Unit — Glasswarden

**Replaces:** Spearman

- Inherits the CP v151 Spearman's base Combat Strength, Movement, cost, requirements and upgrades.
- **+1 Sight**.
- **+15% Combat Strength when defending on Desert**, not when attacking. Unique defensive lineage persists through upgrades.

## Unique Building — Solar Conservatory

**Replaces:** Garden

- Retains all active CP v151 Garden specialist, Great Person, and other effects.
- **+1 Food** permanently.
- **+1 Science per two worked Desert tiles**, capped at **+2 Science per city**.
- **+1 Culture** if the city is founded on Desert.
- May be built in **any city**, removing the Garden's usual freshwater (river/lake) condition for this unique without removing other prerequisites.

## Gameplay example

Sunspire founded on Desert, working four qualifying tiles with a Solar Conservatory during peace: +5 Food (4 UA+1 UB), +3 Science (1 UA+2 UB), +2 Gold (peace UA) and +1 Culture (UB), beyond the normal Garden effects.

## Recommended strategy

**Early:** Settle near Desert rivers, Hills, and resources; the worked-Desert Food bonus supports growth while Glasswardens defend.

**Midgame:** Construct Conservatories even in dry inland cities, keep peace to maintain Gold, and use specialists for research.

**Late:** Convert population and science into a conventional victory; invasion removes peace-Gold and the civilization has no direct Production bonus.

## CP v151 feasibility and Codex implementation requirements

- Register civilization, leader, trait, texts, uniques and art using BNW-valid SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Keep the **active Community Patch baseline** for all unchanged unit/building properties, including upgrade paths and specialist/companion tables.
- Use Lua for checks that SQL/XML cannot represent, applying exact dummy building counts and verified unit promotions as appropriate.
- Never silently substitute weaker, stronger, or functionally different mechanics for a missing CP hook.

- Workable, unpillaged Desert plots need explicit worked-tile checks and per-city cap dummies.
- Peace check: only **living major civilizations** count; account for war start/end events and save/load.
- CP Garden freshwater prerequisite removal must not erase unrelated tech/cost requirements.
- Verify Desert-specific **defense-only** promotion. Do not substitute a universal +15% combat bonus if absent; use a verified combat hook.

**Acceptance tests:** Standard and Marathon speed; save/reload; pillaging/terrain changes where relevant; city capture; unit upgrade; exact bonus caps; revalidation of applicable CP hooks; no dummy stacking or duplicate one-off rewards.

## Leader dialogue

> **Greeting:** Welcome to Sunspire. You expected sand and stone? Come, let me show you our orchards.

> **Declaration of war:** You have mistaken our preference for peace as an inability to defend ourselves.

> **Defeat:** The glass is shattered... but the seeds remain.

---
*Provenance: This is a structured archive of the original Daily Surprise concept from the ChatGPT conversation, preserving its numerical gameplay design and key lore. It is not a verbatim export of all prose or an assertion that CP v151 has been tested.*
