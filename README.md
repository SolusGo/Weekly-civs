# 🎲 Weekly Civs — The Civilization V Surprise Encyclopedia

**26 Daily Surprise Civilization concepts**, archived for Sid Meier's **Civilization V: Brave New World + Community Patch v151**. This is a *design library*, not an installable mod pack.

Every civ has one Markdown entry with its known numerical mechanics, unique components, and Codex implementation cautions. Human-only by default: `Playable=1`, `AIPlayable=0`.

## Complete index

| # | Civilization | Theme | Victory focus |
|---|---|---|---|
| 01 | [Republic of Pigeons](Civilizations/001-republic-of-pigeons.md) | Absurd postal birds | Science / Culture |
| 02 | [Department of Lost Things](Civilizations/002-department-of-lost-things.md) | Lost-property registry | Culture / Science |
| 03 | [The Twelfth Hour](Civilizations/003-the-twelfth-hour.md) | Clockwork timing | Science / Production |
| 04 | [Kingdom of Saba](Civilizations/004-kingdom-of-saba.md) | Historical South Arabia | Culture / Science |
| 05 | [The Conical Union](Civilizations/005-the-conical-union.md) | Sentient traffic cones | Science / Domination |
| 06 | [The Wandering Circus](Civilizations/006-the-wandering-circus.md) | Travelling carnival | Culture |
| 07 | [Assembly of Scarecrows](Civilizations/007-assembly-of-scarecrows.md) | Living scarecrows | Culture / Growth |
| 08 | [The Lantern Fleet](Civilizations/008-the-lantern-fleet.md) | Sea beacons | Science / Culture |
| 09 | [Kingdom of the Unrung Bell](Civilizations/009-kingdom-of-the-unrung-bell.md) | Silence and retaliation | Culture / Defense |
| 10 | [The Threshold Court](Civilizations/010-the-threshold-court.md) | Intercity teleportation | Domination / Culture |
| 11 | [The Honeycomb Commonwealth](Civilizations/011-the-honeycomb-commonwealth.md) | Bees and plantations | Science / Culture |
| 12 | [Republic of First Drafts](Civilizations/012-republic-of-first-drafts.md) | Writing and revisions | Culture / Science |
| 13 | [Kingdom of Makuria](Civilizations/013-kingdom-of-makuria.md) | Medieval Nubia | Culture / Religion |
| 14 | [The Ministry of Almost](Civilizations/014-the-ministry-of-almost.md) | Perpetual runner-up | Science / Culture |
| 15 | [The Hollow Choir](Civilizations/015-the-hollow-choir.md) | Singing mountain crystals | Culture / Religion |
| 16 | [The Salt Road Compact](Civilizations/016-the-salt-road-compact.md) | Desert trade | Science / Diplomacy |
| 17 | [The Seventeenth Summer](Civilizations/017-the-seventeenth-summer.md) | Cyclical cicadas | Science / Culture |
| 18 | [The Perpetual Timetable](Civilizations/018-the-perpetual-timetable.md) | Rail bureaucracy | Science / Culture |
| 19 | [The Candlekeeper's Covenant](Civilizations/019-the-candlekeepers-covenant.md) | Memorials of vanished cities | Culture / Science |
| 20 | [The Paleontological Directorate](Civilizations/020-the-paleontological-directorate.md) | Fossils and archaeology | Science / Culture |
| 21 | [Kingdom of Ryukyu](Civilizations/021-kingdom-of-ryukyu.md) | Maritime commerce | Diplomacy / Culture |
| 22 | [The Mirrorbound Republic](Civilizations/022-the-mirrorbound-republic.md) | Learning from defeat | Science / Domination |
| 23 | [Kingdom of a Thousand Kites](Civilizations/023-kingdom-of-a-thousand-kites.md) | Wind festivals | Culture / Science |
| 24 | [The Postal Sovereignty](Civilizations/024-the-postal-sovereignty.md) | Postal networks | Science / Culture |
| 25 | [The Carapace Dominion](Civilizations/025-the-carapace-dominion.md) | Crab coastal fortresses | Science / Domination |
| 26 | [The Octopus Parliament](Civilizations/026-the-octopus-parliament.md) | Octopus democracy | Science / Culture |

## Other files
- [Implementation Status](IMPLEMENTATION_STATUS.md) — tracked separately from concept design.
- [Balance Notes](BALANCE_NOTES.md) — known areas needing verification.
- [Civilization Template](TEMPLATE.md) — structure for the next surprise.

## Archival integrity
Entries 1–18 are reconstructed from retained design specifications, **not verbatim copies of the original long-form drafts**. Entries 19–26 are based on full designs from the chat, condensed for convenient reference. Missing original details are marked rather than invented.

## Implementation conventions
- Target **Community Patch v151**, not mandatory full Vox Populi.
- SQL/XML/Lua; no custom DLL requirement assumed. Report missing hooks instead of inventing effects.
- Preserve the active CP replacement baseline for unique units and buildings.
- Lua bonuses must be idempotent and save-safe; clean up on capture, unit upgrades, and reload.
- Do not mark a design implemented without verified mod files and tests.

Initial archive: **11 November 2026**.
