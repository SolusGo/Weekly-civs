# 🎲 Daily Surprise Civ V #28 — The Republic of Borrowed Tomorrows

**Release:** 13 November 2026  
**Motto:** *We have already spent what has not yet come.*  
**Complexity:** ★★★★☆ — Advanced  
**Target:** Civilization V: Brave New World + Community Patch **v151** (not full Vox Populi)  
**Human only:** `Playable=1`, `AIPlayable=0`  
**Design status:** Archived concept; gameplay implementation unverified

## Identity

| Field | Value |
|---|---|
| Civilization | The Republic of Borrowed Tomorrows |
| Leader | Chancellor Aevra Voss |
| Capital | Tomorrow's End |
| Theme | Temporal debt, advances against future economic output |
| Preferred victories | Science / Culture |
| Preferred maps | Any; favors a strong capital |

## Unique Ability — The Future Is Collateral

- Once every **15 owner-turns** on Standard speed, choose **one** advance in the Capital. Only one advance can operate at a time.
- **Production Advance:** Immediately receive Production equal to **3 × current base Capital Production/turn**, capped at **150 Production** (Standard); enter repayment with an intended **−50% Production** for **6 owner-turns**.
- **Research Advance:** Immediately receive Science equal to **3 × current base Capital Science/turn**, capped at **150 Science** (Standard); enter repayment with an intended **−50% Science** for **6 owner-turns**.
- The amount advanced is recorded as an **exact outstanding debt**. Deduct up to **50% of eligible actual yield** per owner-turn; unpaid debt persists beyond six turns until fully repaid. No new advance during repayment; cooldown starts on activation.
- Reward caps and borrowed amounts use standard game-speed multipliers; duration and cooldown scale appropriately on Quick/Epic/Marathon and are rounded up. **No net free production/science may be introduced by the advance itself.**

## Unique Unit — Debt Collector

**Replaces:** Pikeman

- Inherit CP v151 Pikeman base Combat Strength, Movement, cost, resource requirements and upgrade lineage.
- **+15% Combat Strength in friendly territory.**
- **+10% Combat Strength while any UA debt remains outstanding**, in any territory.
- Both modifiers can apply when in friendly territory; these bonuses are not base-strength increases.

## Unique Building — Temporal Exchange

**Replaces:** Market

- Retains the installed CP v151 Market's normal effects.
- **+1 Gold** at all times.
- **+1 Science** while the civilization has **no outstanding temporal debt**.
- **+1 Production** while **any debt is outstanding**.
- The Science and Production conditions are mutually exclusive. The building does not alter the amount or rate of borrowed resources.

## Gameplay example

Capital base Production = 30/turn. Production Advance supplies 90 immediately and records debt 90. If eligible repayment capacity stays 30/turn, 15/turn is deducted for six owner-turns. Production must be deducted from actual yield rather than assuming a −50% dummy alone repays exactly 90.

## Recommended strategy

**Early:** Grow a productive capital and avoid advances that cannot be repaid before the next opportunity.

**Midgame:** Advance resources at decisive production/research breakpoints, especially contested Wonders and prerequisite technologies.

**Late:** Align advance timing with a key project or technology, but avoid debt that would starve the capital during a crucial finish. Debt Collectors provide some protection during repayment.

## CP v151 feasibility and Codex implementation requirements

- Register civilization, leader, trait, texts, uniques and art using BNW-valid SQL/XML. Use `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`.
- Keep the **active Community Patch baseline** for all unchanged unit/building properties, including upgrade paths and specialist/companion tables.
- Use Lua for checks that SQL/XML cannot represent, applying exact dummy building counts and verified unit promotions as appropriate.
- Never silently substitute weaker, stronger, or functionally different mechanics for a missing CP hook.

- **High-risk feasibility:** Civ V's ordinary yield modifiers cannot guarantee exact advance/repayment accounting. Reliable pre/post-yield hooks or equivalent verified CP v151 APIs are required for debt neutrality. If missing, the concept requires a DLL hook or a clearly acknowledged compromise; do **not** silently award free yield.
- Production-progress and team research-progress API behavior must be validated (project completion, overflow, rounding, multiple technologies).
- Save the exact debt ledger, outstanding type, next eligible turn, repayment count and active UI choice across reloads.
- Reconcile conditional market dummies and Debt Collector promotions, including unit upgrades, capital loss/relocation, and game-speed differences.

**Acceptance tests:** Standard and Marathon speed; save/reload; pillaging/terrain changes where relevant; city capture; unit upgrade; exact bonus caps; revalidation of applicable CP hooks; no dummy stacking or duplicate one-off rewards.

## Leader dialogue

> **Greeting:** Welcome, stranger. I would offer you tomorrow's hospitality, but I have already sold it.

> **Declaration of war:** Your defeat is inevitable. We have merely arranged for it to occur ahead of schedule.

> **Defeat:** The debt... has finally come due.

---
*Provenance: This is a structured archive of the original Daily Surprise concept from the ChatGPT conversation, preserving its numerical gameplay design and key lore. It is not a verbatim export of all prose or an assertion that CP v151 has been tested.*
