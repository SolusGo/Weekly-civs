# Balance and Engine-Feasibility Notes

All bonuses are design values, not an empirical balance finding. Review on **Civ V Brave New World + Community Patch v151** before marking a mod playable.

## Highest-risk mechanics
- **Unverified hooks:** Archaeological excavation completion (#20), combat-death cause and next-attack tracking (#22), foreign city destruction (#19), unit movement bonus timing (#24).
- **Combat modifier specificity:** Defense-only, attacking a target on certain terrain, and coastal land defense require a proven CP v151 modifier or a tested combat event; a generic territorial modifier is *not* equivalent.
- **Stateful civilization mechanics:** #02 Curios, #06 festivals, #09 Quietude, #10 teleports, #12 building-class firsts, #17 emergence cycles, #19 Lost Flames, #22 Lessons, #26 Parliament resolutions.
- **Connections:** #18 owned rail-only paths must be checked by an explicit traversability test rather than a generic capital connection flag.
- **Geography:** #04 Saba, #08 Lantern Fleet, #11 Honeycomb, #15 Hollow Choir, #16 Salt Road, #21 Ryukyu, #23 Kites and #25 Carapace can be map-dependent.
- **Game speed and turn order:** Verify all time windows and speed-scaled one-time rewards, especially #03, #06, #09, #17, #20, #22, #24 and #26.
- **Unique replacement inheritance:** Preserve active CP baseline effects, specialist slots, promotions, construction requirements and class compatibility.

## Reporting a balance change
Record the original and proposed values, reason, game speed/map size, CP version, and validation result. Keep canonical design mechanics identifiable.
