# 🎲 Daily Surprise Civ V #032 — The Muisca Confederation

**Release:** 17 November 2026  
**Leader:** Zipa Tisquesusa  
**Capital:** Bacatá  
**Theme:** Historical Muisca highland chiefdoms, salt and gold craftsmanship, sacred lakes  
**Motto:** *“Gold is not wealth until it is given.”*  
**Complexity:** ★★☆☆☆ — Vanilla-like with light Lua  
**Victory:** Culture / Religion / Diplomacy  
**Target:** Civilization V: Brave New World + Community Patch v151, no Vox Populi requirement  
**Playability:** `Playable=1`, `AIPlayable=0`  
**Status:** Archived concept; implementation and balance unverified

## Premise

In the highlands of what is now Colombia, the Muisca developed prosperous settlements linked by exchange in salt, textiles, and finely worked gold. The civilization treats gold as ceremonial prestige, not simply stored money, and rewards carefully developed resources rather than conquest. Sacred lakes anchor religious life.

The Muisca Confederation is a historical-inspired, deliberately straightforward design. It represents a network of chiefdoms rather than a centralized modern state.

## UA — The Sacred Exchange

- Each city working at least **one owned, improved, unpillaged Gold or Silver resource tile** receives **+2 Faith and +1 Culture**. This is a **binary per-city** bonus: additional qualifying resources do not stack it.
- Each city owning at least **one Lake tile within three plots** of its city center receives **+1 Gold**. This is also a **binary** bonus; the Lake does **not** have to be worked.
- Bonuses are added to normal tile/building yields. The bonuses end when eligibility is lost (e.g., pillage, ownership change or reassignment).

**Design intent:** Reward resource-focused city placement and the Muisca's ceremonial use of precious metal, with a modest lake-based commerce bonus. No global flat Gold multiplier or free military power.

## UU — Guecha Warrior

**Replaces:** Spearman.

- **Combat Strength, Production Cost, Movement, maintenance, resource requirements, upgrade route:** same as the installed CP v151 Spearman.
- **+1 Sight**.
- **+15% Combat Strength when defending on Hills** (not when attacking, and not on flatland).
- Unique Sight and Hill Defense promotions **persist through normal upgrades**. They do not stack multiple copies of themselves.
- Retains the CP Spearman's standard anti-mounted role and other unchanged baseline effects.

**Role:** Protect upland settlements and observe enemy movements. A Guecha Warrior has no offensive combat bonus and is not a replacement for a full military strategy.

## UB — Salt Exchange

**Replaces:** Market.

- Retains **all normal CP v151 Market effects**, specialist slots, prerequisites, maintenance, and building-class compatibility.
- **+1 Faith** permanently.
- **+1 Gold per worked, owned, improved, unpillaged Mine tile**, capped at **+2 Gold per city**. Mines on Gold and Silver qualify if they are actually worked; all qualifying Mine resources/improvements use the same cap.
- No Lake requirement for construction. Its Gold bonus is **not** granted for unworked Mines.

**Role:** Converts a productive mining economy into modest additional commerce and ceremonial prestige.

## Gameplay strategy

**Ancient–Classical:** Settle resource-rich Hills, preferably near freshwater Lakes, but secure enough Food to work mines. Scout with Guecha Warriors and defend Hill approaches.

**Medieval–Renaissance:** Improve Gold/Silver and other Mines, assign citizens to work them, and build Salt Exchanges. The UA provides Faith for religion, while Culture and Gold support policies and trade.

**Industrial–Information:** Use modest persistent resource-based yields to pursue Culture, religious influence, or a diplomatic victory. The Muisca have no direct Production, Science, or offensive military scaling, so conventional infrastructure remains essential.

## Numerical example

A city works one improved Gold Mine and one improved Iron Mine, owns a Lake tile within radius three, and has a Salt Exchange.

- UA: **+2 Faith, +1 Culture, +1 Gold**.
- UB: **+1 Faith and +2 Gold**.
- **Total civilization-specific bonuses: +3 Faith, +1 Culture, +3 Gold per turn**, before normal Market and tile yields.

A third worked Mine does not increase the Salt Exchange's capped Gold bonus. A second Gold/Silver tile does not duplicate the UA bonus.

## CP v151 implementation / Codex pointers

1. Register `CIVILIZATION_MUISCA_CONFEDERATION`, `LEADER_TISQUESUSA`, `TRAIT_SACRED_EXCHANGE`, `UNIT_GUECHA_WARRIOR`, and `BUILDING_SALT_EXCHANGE`. Set `Playable=1`, `AIPlayable=0`.
2. Use standard `Civilization_UnitClassOverrides` and `Civilization_BuildingClassOverrides`. Clone and retain the **actual installed CP v151** Spearman and Market baselines; do not assume vanilla statistics.
3. Reconcile UA city eligibility with Lua: count plots *worked by that city*, requiring the plot's resource to be Gold/Silver, an appropriate improvement, ownership, and no pillage. Do not grant bonuses for unworked resource tiles.
4. For the Lake bonus, identify **actual Lake water plots** (not merely coast, river, or generic freshwater). The plot must be owned by the city/player and within three plots of the city center; the count is binary.
5. Reconcile the Salt Exchange Mine count with Lua and idempotent city dummy buildings: exactly 0, 1, or 2 bonus Gold. Handle citizen assignment, plot purchase, improvement replacement/pillaging, capture, and save/load. Dummy buildings must not be user-constructible.
6. **Engine limitation:** Standard Civ V XML terrain promotions do not necessarily offer a **defense-only Hills modifier** in the desired form. Verify a supported CP v151 promotion or combat hook. Do **not** replace it with a generic +15% Hills attack-and-defense bonus. If unavailable, implement a verified scoped combat effect or explicitly mark that portion as requiring a hook.
7. **Engine limitation:** Gold/Silver resource ownership and worked plots can be checked through Lua, but there is no single XML trait row that expresses this exact *binary, worked-and-improved per-city* condition. Lua reconciliation is necessary.
8. No custom DLL, complex UI, or persistent gameplay ledger is intended. Use a turn-level fallback reconciliation and additional hooks where verified.

**Acceptance tests:** Found city with/without Lake; ownership and radius edge cases; worked/unworked Gold and Silver; pillaged and unimproved resources; two vs. three Mines; unit defense on Hills vs. attack and flatland; upgrade lineage; save/load; city capture; CP v151 Market inheritance; Standard and Marathon.

## Leader dialogue

**Greeting:** “Welcome to Bacatá. You may keep your coins. Tell me what your people consider sacred.”

**Declaration of war:** “You count our gold and mistake it for weakness. Our warriors count the paths through these mountains.”

**When attacked:** “Climb, then. The mountains will decide which of us reaches the summit.”

**Defeat:** “The gold will pass from hand to hand. I wonder if you will ever understand what it meant.”

---
*Design archive only. Historical inspiration is distinct from a claim of exact historical simulation; unit and building effects are fictionalized gameplay abstractions.*
