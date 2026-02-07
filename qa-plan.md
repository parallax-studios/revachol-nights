# REVACHOL NIGHTS — QA Plan

**Document Owner**: CRASH (QA Lead)
**Status**: Complete Pre-Production QA Specification
**Version**: 1.0
**Date**: 2026-02-07

---

## 0. Quality Philosophy

This document defines what "works" means. Every system. Every edge case. Every failure mode.

You don't ship a roguelite with save corruption. You don't ship a detective game where evidence randomly disappears. You don't ship a psyche-based combat system where builds feel identical. These aren't bugs — they're career-ending mistakes that turn 1-star reviews into permanent reputation damage.

Define "works." Then test until it does.

---

## 1. Test Plan Overview

### 1.1 Testing Phases

| Phase | Timeline | Focus | Exit Criteria |
|-------|----------|-------|---------------|
| **Unit Testing** | Ongoing (M1-M8) | Data structures, core logic | 100% pass rate on critical systems |
| **Integration Testing** | M3-M7 | System interactions, data flow | No blockers, <5 critical bugs |
| **Feature Testing** | M4-M6 | Per-feature validation | All features meet spec |
| **Roguelite Loop Testing** | M5-M7 | Run pacing, meta-progression | 30+ complete runs without progression block |
| **Balance Testing** | M6-M7 | Combat difficulty, Insight economy | All archetypes viable, economy feels tense |
| **Platform Testing** | M6-M8 | PC, Switch performance/compatibility | 60 FPS PC, 30 FPS Switch min |
| **Regression Testing** | M7-M8 | Re-test all systems post-fix | No regressions on previous pass |
| **Closed Beta** | M7 (Month 18-20) | Player feedback, edge cases | <10 critical bugs reported |

### 1.2 Testing Environment

**Hardware:**
- PC: Min spec (GTX 1050, 8GB RAM, Win 10), mid spec, high spec
- Switch: Dev kit (docked and handheld)
- Input: Keyboard/mouse, Xbox controller, PS5 controller, Switch Pro Controller

**Software:**
- Godot 4.3 builds (debug and release)
- Steam build (with Steam SDK)
- Switch build (with Nintendo SDK)

**Save States:**
- Fresh save (Run 1)
- Early game save (Runs 1-5, Layer 1)
- Mid game save (Runs 10-15, Layer 2-3)
- Late game save (Runs 25+, Layer 4-5)
- Corrupted save (for recovery testing)

---

## 2. Core Systems Test Plan

### 2.1 Psyche System

**Responsibility:** Generate builds, track sub-skills, validate Internal Voice checks.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| PSY-001 | Generate valid psyche build | None | Start new run → observe psyche reveal | Build displays 4 archetypes, points sum to 24, dominant archetype is 8-12 points, dump stat is 1-3 points |
| PSY-002 | Archetype determines combat verbs | Run started | Check unlocked verbs in HUD | Authority has heavy_strike, Empathy has light_strike, Logic has logic_dart, Electrochemistry has electro_rush |
| PSY-003 | Sub-skills activate at correct thresholds | Authority 9+ build | Check active sub-skills | All 6 Authority sub-skills are active (Tier 3) |
| PSY-004 | Dominant archetype displayed in HUD | Run started | Check HUD color/text | HUD tint matches dominant archetype color, archetype name displayed |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| PSY-005 | Point distribution error check | Debug: force invalid build (25 points) | Start run | Game catches error, regenerates valid build OR crashes gracefully with error log |
| PSY-006 | Dump stat is 0 points | Debug: force dump stat = 0 | Start run | Build regenerates OR allows 0 (Tier 0 behavior is correct) |
| PSY-007 | All archetypes equal (6/6/6/6) | Debug: force balanced build | Start run | Game designates a dominant (highest sub-skill activation?) OR handles gracefully |
| PSY-008 | Sub-skill check with inactive sub-skill | Empathy Tier 0 build | Trigger Suggestion Internal Voice | Check auto-fails, psychic damage taken |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| PSY-009 | Spam psyche reshuffle | Precinct hub | Die/complete 50 runs in rapid succession | Every build is valid, no duplicate builds in a row (pity system), no memory leak |
| PSY-010 | Save/load mid-psyche-reveal | Run starting, psyche reveal cinematic playing | Alt-tab, force quit, reload | Game resumes at precinct hub OR completes reveal correctly |
| PSY-011 | Memory Anchor persistence | Purchase Memory Anchor for Intimidation | Complete run, die, start new run | Intimidation is active in new build regardless of Authority points |
| PSY-012 | Meditation Focus stacking | Purchase 5x Meditation Focus (Authority) | Start 10 new runs | Authority is dominant in >70% of runs (verify weight adjustment works) |

#### Edge Cases

- What happens if all 4 archetypes are locked by Memory Anchors? (Should be impossible — only 1 sub-skill can be locked, not full archetype)
- What happens if player has 0 Psyche Echoes and tries to purchase? (Button should be disabled)
- What happens if psyche build generation fails 3 times in a row? (Fallback to balanced build?)
- Internal Voice check during player death animation? (Should cancel or auto-fail)

**Risk Areas:**
1. **Build generation randomness feels "wrong"** — players get same dominant 4 times in a row despite pity system
2. **Sub-skill activation thresholds are off** — Tier 2 feels like Tier 1
3. **Internal Voice timing window inconsistent across framerates** — 1.5s at 60 FPS feels different than 1.5s at 30 FPS

**Pass Criteria:**
- 1000 generated builds, all valid (sum to 24, no negative values)
- Pity system prevents same dominant 3+ times in a row
- Sub-skill activation matches spec (Tier 1 at 3+, Tier 2 at 6+, Tier 3 at 9+)
- Internal Voice timing windows are delta-time based, feel consistent at 30 FPS and 60 FPS

---

### 2.2 Combat System

**Responsibility:** Player movement, attacks, dodges; enemy AI; hitbox detection; HP management.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| COM-001 | Player movement (all directions) | In combat room | Move left/right/up/down with keyboard and gamepad | Player moves smoothly at archetype-specific speed (Authority 150, Empathy 250, etc.) |
| COM-002 | Basic attack executes | Any archetype | Press attack button | Attack animation plays, hitbox activates, enemy takes damage on contact |
| COM-003 | Dodge grants i-frames | Any archetype | Dodge through enemy attack | Player is invulnerable during dodge, takes no damage |
| COM-004 | Enemy pursues player | Standard enemy in room | Enter aggro range | Enemy switches to CHASE behavior, follows player |
| COM-005 | Enemy attacks when in range | Enemy in CHASE | Get within attack range | Enemy executes attack animation, deals damage if player is hit |
| COM-006 | Enemy dies and drops Insight | Standard enemy, <10% HP | Kill enemy | Death animation plays, enemy despawns, Insight pickup spawns at position |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| COM-007 | Attack during dodge animation | Player mid-dodge | Press attack button | Attack input queues OR is ignored (no animation break) |
| COM-008 | Dodge with zero velocity | Player standing still | Press dodge | Dodge executes in default direction (forward), doesn't lock player in place |
| COM-009 | Player takes damage during hit stun | Player in HIT state | Second enemy attacks during hit animation | Damage applies OR i-frames extend (define intended behavior) |
| COM-010 | Enemy pathfinding fails | Enemy spawns in unreachable area | Observe behavior | Enemy returns to PATROL OR teleports to valid navmesh point OR despawns with warning log |
| COM-011 | Multiple enemies attack simultaneously | 3+ enemies in attack range | Wait for attacks | All attacks register OR there's a stagger system (define intended) |
| COM-012 | Player death during attack animation | Player at 1 HP, mid-attack | Enemy attack lands | Death animation interrupts attack, DEAD state triggers, run ends |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| COM-013 | Button mashing attack spam | Any archetype | Spam attack button 100 times | Attack animations queue OR spam is rate-limited, no animation lock, no crash |
| COM-014 | Dodge spam | Any archetype | Spam dodge button constantly | Dodge cooldown is respected OR consecutive dodges are allowed but feel responsive, no stamina break |
| COM-015 | Attack hitbox lingers after animation | Debug: extend hitbox duration artificially | Execute attack, move away | Hitbox deactivates when animation ends, doesn't persist as invisible damage zone |
| COM-016 | Electrochemistry combo counter overflow | Electrochemistry build | Land 100+ consecutive hits without taking damage | Combo counter doesn't overflow (int max?), damage scaling caps at reasonable value |
| COM-017 | Enemy AI stack overflow | 20+ enemies in room | Trigger all enemy AI updates simultaneously | No frame drop >16ms, no crash, AI updates are throttled if necessary |
| COM-018 | Hitbox collision on frame 1 of attack | Player and enemy attack on same frame | Both execute attacks simultaneously | Both take damage OR priority system is defined (player always wins? enemy always wins? simultaneous hit?) |

#### Edge Cases

- What happens if player dodges into a wall? (Dodge distance shortens OR player phases through?)
- What happens if enemy is killed mid-attack? (Attack cancels OR completes as "ghost attack"?)
- What happens if player alt-tabs during combat? (Game pauses OR continues in background — define for PC vs Switch)
- Signature ability used at 0% HP (on death frame)? (Ability cancels OR executes with brief invuln?)
- Logic archetype trap placement on invalid terrain? (Trap fails to place with feedback OR snaps to nearest valid tile?)

**Risk Areas:**
1. **Combat doesn't feel responsive** — input lag, animation locks, attack queuing feels sluggish
2. **Hitboxes are wrong** — attacks miss when visually connected, or hit from too far away
3. **Enemy AI is exploitable** — players can cheese encounters by standing in a corner, enemies get stuck
4. **Archetype balance is broken** — Empathy is trivial (too much evasion), Electrochemistry is unplayable (too punishing)

**Pass Criteria:**
- Combat feels responsive at 60 FPS (input to action <100ms)
- Hitbox accuracy >95% (visual contact = damage)
- Enemy AI completes PATROL → CHASE → ATTACK → RETREAT loop without getting stuck
- All 4 archetypes can clear District 1-3 reliably (QA tester with 10 hours experience)
- No combat softlocks (player or enemy stuck in terrain, unable to move/attack)

---

### 2.3 Case Refraction Engine

**Responsibility:** Filter evidence by psyche build, assemble case conclusions, maintain case logic.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| CRE-001 | Authority build sees Authority evidence | Authority Tier 1+ build | Enter room with "bruises_on_arms" evidence | Evidence object is visible and interactable |
| CRE-002 | Empathy build does NOT see Authority evidence | Empathy Tier 3 build (Authority Tier 0) | Enter same room | Evidence object is greyed out with tooltip "You sense something here, but can't perceive it" |
| CRE-003 | Collect evidence adds to case board | Any build, visible evidence | Interact with evidence object | Evidence ID added to CaseRefraction.collected_evidence, confirmation UI/sound |
| CRE-004 | Case conclusion available with 3+ evidence | Collected 3+ evidence pointing to "conclusion_authority_power_struggle" | Reach end-of-run case close screen | "Accuse [Suspect A]" option is available and unlocked |
| CRE-005 | Case conclusion unavailable with <3 evidence | Collected 2 evidence for a conclusion | Reach case close screen | That conclusion option is locked OR not displayed |
| CRE-006 | Multiple conclusions available | Collected 3+ evidence for two different conclusions | Reach case close screen | Both options available, player chooses one |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| CRE-007 | Collect evidence with no archetype requirement | Any build | Interact with "universal" evidence (required_archetype = "") | Evidence collects normally regardless of build |
| CRE-008 | Evidence visibility changes mid-run | Start as Authority 6, use Insight upgrade to boost to Authority 9 | Re-enter previously visited room with Authority Tier 3 evidence | Evidence is now visible (or isn't — define: does visibility update dynamically or lock at room load?) |
| CRE-009 | No case conclusions available | Collected only evidence that doesn't point to conclusions | Reach case close screen | Game provides fallback "inconclusive" ending OR forces player to return to district (define intended) |
| CRE-010 | Evidence JSON is missing required field | Debug: remove "required_archetype" from an evidence node | Load evidence database | Game logs error, skips invalid evidence OR crashes gracefully with error message |
| CRE-011 | Duplicate evidence collection | Collect same evidence twice in same run (if somehow possible) | Interact with evidence twice | Second interaction is ignored OR provides feedback "Already collected" |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| CRE-012 | Collect 100+ evidence in one run | Debug: spawn all evidence in one room | Collect all | No array overflow, no performance degradation, all evidence tracked |
| CRE-013 | Evidence node points to non-existent conclusion | Debug: set "points_to_conclusion" to invalid ID | Collect evidence, reach case close | Game handles gracefully (logs error, ignores evidence for conclusion assembly) |
| CRE-014 | Save/load mid-evidence-collection | Collect 2 evidence, save, quit, reload | Check case board | 2 evidence are still collected (unless save happened at run end only — clarify save timing) |
| CRE-015 | Case conclusion with circular evidence dependencies | Debug: Evidence A requires Evidence B, Evidence B requires Evidence A | Attempt to assemble conclusion | No infinite loop, conclusion assembles OR is correctly marked unavailable |
| CRE-016 | Evidence filtering with corrupted PsycheProfile | Debug: set Authority = -5 | Enter room with Authority-gated evidence | Game catches invalid profile, regenerates OR evidence visibility fails gracefully |

#### Edge Cases

- What happens if ALL evidence in a district is invisible to the current build? (Intended? Room should guarantee 1-2 visible evidence per build — verify DistrictGenerator)
- What happens if player reaches case close with 0 collected evidence? (Fallback ending? Force return to hub?)
- Can evidence be "un-collected" if player reloads a save? (Depends on save timing — clarify)
- Evidence object spawns inside wall (bad spawn point)? (Player can't interact — need collision check on spawn)

**Risk Areas:**
1. **Case Refraction feels arbitrary** — players don't understand why they can/can't see evidence
2. **Evidence visibility is inconsistent** — same build sees different evidence across runs (RNG seed issue?)
3. **Case conclusions are imbalanced** — one archetype has 10 available conclusions, another has 2
4. **Meta-case connections don't appear** — evidence with matching meta_tags doesn't create threads on board

**Pass Criteria:**
- Evidence visibility is 100% consistent with archetype requirements (no false positives/negatives)
- Every archetype build can collect 3+ evidence per district (verify with 50 runs per archetype)
- All 10 case conclusions are reachable (Authority, Empathy, Logic, Electrochemistry dominant + hybrid conclusions)
- Meta-case board correctly identifies and displays evidence connections (shared meta_tags)

---

### 2.4 Insight Economy

**Responsibility:** Track Insight, handle drops, validate spending, balance tension.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INS-001 | Insight drops from enemy kill | Enemy at low HP | Kill enemy | Insight pickup spawns, value = 1-2 (standard) or 3-4 (elite) |
| INS-002 | Insight pickup adds to counter | Insight counter at 5 | Collect pickup worth 3 | Counter updates to 8, audio/visual feedback |
| INS-003 | Spend Insight on combat upgrade | 10 Insight, at debrief shop | Purchase "Damage +15%" (cost 6) | Insight drops to 4, upgrade applies to CombatController, player damage increases |
| INS-004 | Spend Insight on narrative unlock | 8 Insight, at debrief shop | Purchase "Interrogate Witness A" (cost 7) | Insight drops to 1, dialogue starts immediately |
| INS-005 | Cannot afford purchase | 5 Insight | Attempt to purchase 8-Insight item | Button is disabled OR purchase fails with feedback "Not enough Insight" |
| INS-006 | Insight persists across rooms in a run | 10 Insight in Room 1 | Complete room, enter Room 2 | Counter still shows 10 (plus any drops from Room 1) |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INS-007 | Insight drops outside playable area | Enemy dies near edge of room | Kill enemy | Pickup spawns in accessible area OR is auto-collected with range check |
| INS-008 | Multiple pickups overlap | 3 enemies die in same location | Collect pickups | All 3 pickups are collected OR they stack into single pickup with combined value |
| INS-009 | Insight purchase during Internal Voice | At shop, Internal Voice triggers | Attempt purchase mid-check | Purchase is queued OR blocked until check resolves |
| INS-010 | Spend all Insight, then enter combat | 0 Insight at run start | Enter District 1 | Player can still fight (combat isn't gated by Insight), Insight drops allow future purchases |
| INS-011 | Insight counter overflow | Debug: set Insight to 9999 | Collect pickup | Counter increments correctly OR caps at max value (define max) |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INS-012 | Rapid pickup collection | 20 pickups spawned in tight cluster | Run through cluster, collect all in <1 second | All pickups register, counter updates correctly, no drops lost |
| INS-013 | Spend Insight faster than UI updates | 50 Insight | Spam purchase button on 6-Insight item 8 times rapidly | Only valid purchases execute (max 8), UI updates correctly, no negative Insight |
| INS-014 | Purchase after death but before run end | Player at 1 HP, shop open | Purchase upgrade, player dies during purchase | Purchase completes OR is cancelled (define intended), Insight change persists OR reverts |
| INS-015 | Insight duplication exploit | Any method to trigger double-collect | Attempt exploit | Exploit is impossible OR detected and blocked |
| INS-016 | Save/load to reset Insight spend | 20 Insight, spend 15, save mid-run | Reload save | Insight is 5 (spent Insight is saved) OR 20 (reverted — unintended?) |

#### Edge Cases

- What happens if Insight drops during death animation? (Auto-collect? Lost?)
- Can player collect Insight pickup after death but before respawn? (Shouldn't be possible — define)
- Insight shop with 0 available purchases (all already bought)? (Shop shows "Nothing left to purchase" OR closes)
- Insight drop from Internal Voice success during boss fight? (+2 Insight bonus applies immediately)

**Risk Areas:**
1. **Insight economy is too generous** — players can afford both combat AND narrative every debrief, tension collapses
2. **Insight economy is too punishing** — players can barely afford survival, never unlock narrative, case feels blocked
3. **Insight drop rates vary unpredictably** — RNG spikes/droughts break balance
4. **Exploit allows infinite Insight** — duplication, pickup respawn, shop refund

**Pass Criteria:**
- Insight budget per run (5 districts, full clear) is 50-66 (matches design spec)
- Max combat upgrades cost ~45 Insight, max narrative unlocks cost ~55 Insight (tension is real)
- No Insight exploits possible (tested by red team QA)
- 100 runs tested: Insight drop variance is <15% from expected value (no RNG outliers)

**Balance Validation:**
- 20 QA runs per archetype (80 total): record Insight earned and spent per run
- Target: Players agonize over spend choices in 70%+ of debriefs
- If players consistently skip narrative OR consistently skip combat, economy needs tuning

---

### 2.5 Meta-Case Board & Persistence

**Responsibility:** Save/load, cross-run evidence tracking, conspiracy layer unlocks.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| MET-001 | Evidence pins to board after run | Complete run with 3 evidence collected | Return to precinct hub | 3 evidence fragments appear on meta-case board, marked "Confirmed" (confidence 1.0) |
| MET-002 | Evidence from death-ended run | Die in District 3 with 2 evidence | Return to hub | 2 evidence fragments appear, marked "Unconfirmed" (greyed out, confidence 0.5) |
| MET-003 | Evidence connection appears | Run 1: collect evidence with meta_tag "conspiracy_layer_1", Run 2: collect different evidence with same tag | View board after Run 2 | Red thread connects the two evidence fragments |
| MET-004 | Conspiracy layer unlocks | 5+ connections with "conspiracy_layer_2" meta_tags | View board | Layer 2 unlocks, new lore text appears, new evidence types become available |
| MET-005 | Save file persists across sessions | Complete 3 runs, quit game | Relaunch game, load save | Meta-case board shows all 3 runs' evidence, run count = 3, Psyche Echoes correct |
| MET-006 | Run history tracks all runs | Complete 10 runs | View run history screen | All 10 runs listed with: run number, psyche profile, conclusion, districts cleared, death status |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| MET-007 | Save file doesn't exist | Fresh install, no save file | Launch game, start new run | Game initializes blank save (Run 0, empty board, 0 Echoes) |
| MET-008 | Save file is corrupted | Edit save file to break JSON | Launch game, load save | Game detects corruption, offers "Start Fresh" or "Attempt Recovery" (define recovery behavior) |
| MET-009 | Save during run (if allowed) | Mid-run, District 2 | Save and quit | Next launch resumes at District 2 start OR precinct hub (define save timing) |
| MET-010 | Evidence fragment with no meta_tags | Collect evidence with empty meta_tags array | View board | Fragment appears but has no connections (valid behavior) |
| MET-011 | Duplicate evidence across runs | Run 1 and Run 2 both collect same evidence_id | View board | 2 separate fragments appear (same evidence, different runs, different confidence) OR single fragment updates |
| MET-012 | Conspiracy layer unlock condition not met | 4/5 required connections for Layer 2 | View board | Layer 2 remains locked, progress indicator shows "4/5" |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| MET-013 | 1000+ evidence fragments on board | Debug: simulate 500 runs | View board | UI remains responsive (<2s load time), all fragments render OR UI paginates/filters |
| MET-014 | Save file size explosion | 100+ runs logged | Check save file size | File is <500KB OR game warns/compresses old runs |
| MET-015 | Save/load spam | Save and load 100 times in succession | Check save file integrity | No corruption, no data loss, no crash |
| MET-016 | Run history with identical builds | 10 runs, all with same psyche profile (via Meditation Focus spam) | View history | All 10 runs are distinct entries (run number increments correctly) |
| MET-017 | Meta-case board auto-organization bug | Evidence fragments create circular dependency in graph | View board | No infinite loop, graph renders with cycle OR detects and breaks cycle |
| MET-018 | Delete save file during save operation | Save operation in progress | Force quit game | Save completes OR save is cancelled cleanly (no partial save corruption) |

#### Edge Cases

- What happens if player completes 1000 runs? (Save file size, board UI performance — define cap?)
- Can meta-case board be reset without deleting save? (Intentional? Probably no.)
- Evidence fragment with invalid evidence_id (ID doesn't exist in database)? (Skip fragment with log error)
- Conspiracy layer unlock triggered twice (due to bug)? (Idempotent unlock — second trigger ignored)
- Save file from older game version loaded in newer version? (Migration path defined? Backwards compatibility?)

**Risk Areas:**
1. **Save corruption** — THE career-ending bug. Players lose 30+ hours of progress, 1-star review guaranteed.
2. **Meta-case board doesn't reveal connections** — players complete 20 runs, see no threads, feel stuck
3. **Conspiracy layer unlock is too slow** — Layer 1 unlocks at Run 10+, players churn before experiencing hook
4. **Save file size grows unbounded** — 100 runs = 10MB save file, performance degrades

**Pass Criteria:**
- Save/load 100 times with no data loss or corruption
- Meta-case board correctly identifies all evidence connections (100% accuracy)
- Conspiracy Layer 1 unlocks by Run 3-4 (verified with 50 playthroughs)
- Save file size <100KB after 50 runs, <500KB after 200 runs
- No save-related crashes or softlocks in 100-hour stress test

**Save Corruption Test Protocol:**
- Force quit during save (10 times)
- Power loss simulation (if testable on Switch)
- Corrupt save file, attempt load (graceful degradation?)
- Concurrent save operations (shouldn't be possible, but verify)
- Save file size limit test (fill disk to <1MB free space, attempt save)

---

### 2.6 Internal Voices

**Responsibility:** Trigger mid-combat skill checks, provide buffs/penalties, deliver narrative fragments.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INT-001 | Internal Voice triggers mid-combat | In combat, ~30 seconds into room | Wait for trigger | Dialogue box appears with archetype voice text, 1.5s timer starts, vinyl scratch audio plays |
| INT-002 | Successful skill check | Internal Voice active | Press correct input within 1.5s | Success feedback (harmonic sound), +2 Insight, 3-5s combat buff, narrative fragment displayed |
| INT-003 | Failed skill check | Internal Voice active | Miss input window OR press wrong input | Failure feedback (dissonant buzz), -5-10% HP psychic damage, distorted narrative fragment |
| INT-004 | Internal Voice timing window scales with difficulty | Standard difficulty | Trigger check | Window is 1.5s; Hard difficulty reduces to 1.0s, Detective to 0.6s |
| INT-005 | Multiple Internal Voices in boss room | Boss fight | Complete fight | 2-3 voices trigger at appropriate moments (mid-combo, after elite kill, during phase transition) |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INT-006 | Internal Voice during dodge | Mid-dodge animation | Voice triggers | Voice waits until dodge completes OR triggers during dodge (define intended), player can respond |
| INT-007 | Internal Voice during death animation | Player at 1 HP, taking fatal damage | Voice triggers on same frame | Voice cancels OR completes (psychic damage applies to corpse?), run ends cleanly |
| INT-008 | Spam input during voice window | Voice active | Mash all buttons | Only correct input registers OR wrong inputs count as failure |
| INT-009 | Voice triggers when sub-skill is inactive | Empathy Tier 0 build | Empathy voice triggers | Auto-fail (as designed), psychic damage applies, distorted fragment |
| INT-010 | Voice narrative fragment is empty | Debug: dialogue text is missing | Voice triggers | Game logs error, displays fallback text OR skips text display |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| INT-011 | 100+ voice checks in one run | Debug: force voice trigger every 5 seconds | Complete run | No memory leak, no performance degradation, all checks resolve correctly |
| INT-012 | Voice trigger during another voice | First voice still active | Second voice attempts to trigger | Second voice queues OR is suppressed (no overlap) |
| INT-013 | Alt-tab during voice window | Voice active, 0.5s remaining | Alt-tab game window | Timer pauses OR continues (define for PC; Switch can't alt-tab), no unfair failure |
| INT-014 | Voice timing at 30 FPS vs 60 FPS | Switch (30 FPS) vs PC (60 FPS) | Trigger voice, measure window | Delta-time ensures 1.5s is 1.5s on both platforms, feels consistent |
| INT-015 | Voice check during screen transition | End of room, door opening | Voice triggers | Voice completes OR cancels cleanly (no carryover to next room) |
| INT-016 | Voice narrative fragment contains injection | Debug: insert HTML/script in dialogue text | Voice triggers | Text is sanitized OR renders as plain text (no code execution) |

#### Edge Cases

- Voice triggers frame 1 of combat (before player can react)? (Delay first voice by 5s minimum?)
- Voice buff stacks with another buff? (Define stacking rules: additive? multiplicative? exclusive?)
- Voice success grants +2 Insight, but counter is at max? (Define Insight cap OR allow overflow)
- Voice triggers during pause menu? (Pause should freeze all gameplay, including voices)

**Risk Areas:**
1. **Internal Voices feel like annoying QTEs** — players resent interruptions, don't read narrative text
2. **Timing window is inconsistent** — feels unfair at 30 FPS, too easy at 60 FPS
3. **Voice frequency is wrong** — too frequent (every 10s, exhausting) or too rare (every 5 minutes, forgettable)
4. **Narrative fragments are ignored** — players just mash button, don't engage with text

**Pass Criteria:**
- Voice timing window is delta-time based, feels identical at 30 FPS and 60 FPS (blind A/B test)
- Voice frequency is ~1 per room (verified across 50 runs)
- QA survey: 70%+ of testers report voices "add to experience" rather than "disrupt flow"
- Narrative text is readable within window (max 15 words per voice text)

**Playtest Question:**
- Do players read the Internal Voice text, or do they just react to the mechanic? If they're not reading, the Disco Elysium half is failing. Monitor via eye-tracking or post-playtest survey.

---

### 2.7 District Generation & World

**Responsibility:** Assemble districts from room prefabs, populate enemies/evidence, ensure case-relevant content.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIS-001 | District generates with 4-6 rooms | Start District 1 | Complete district | 4-6 combat rooms + 1 debrief room, all rooms connected |
| DIS-002 | Enemy count scales with district number | District 1 vs District 5 | Count enemies per room | District 1: 3-4 enemies, District 5: 7-8 enemies |
| DIS-003 | Evidence appears in rooms | Authority Tier 2 build, enter room | Check for visible evidence | At least 1 Authority-gated evidence is present |
| DIS-004 | Case-relevant evidence guaranteed | Any build, District 1 | Complete district | 1-2 psyche-visible evidence nodes appear (DistrictGenerator ensures this) |
| DIS-005 | Safe room (debrief) is always last | District 1-5 | Play through | Final room is always debrief (Insight shop, witness/suspect, path choice) |
| DIS-006 | Room layouts do not repeat | Play 20 rooms | Observe layouts | Room prefabs recombine, no exact room appears twice in same run (or rarely) |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIS-007 | Evidence spawn point inside wall | Debug: force bad spawn | Enter room | Evidence is inaccessible OR snaps to nearest valid tile OR logs error (define intended) |
| DIS-008 | Enemy spawn point overlaps player spawn | Debug: force overlap | Enter room | Player takes immediate damage OR enemy is repositioned OR player spawns safely |
| DIS-009 | Room has 0 enemy spawn points | Debug: room prefab missing spawn points | Enter room | Room is empty (valid?) OR game logs error and spawns enemies at fallback positions |
| DIS-010 | District generation times out | Debug: force generation loop to run 10s+ | Start district | Loading screen shows progress OR game logs error and generates fallback district |
| DIS-011 | Evidence database is empty | Debug: delete all evidence nodes | Generate district | Rooms have no evidence (valid if no evidence is available), game doesn't crash |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIS-012 | 1000 consecutive districts generated | Debug: auto-complete runs | Generate districts | No memory leak, generation time stays consistent, no repeated room sequences |
| DIS-013 | Save/load during district load | District loading screen active | Force quit | Next launch resumes at precinct hub (district generation restarts) OR crash is graceful |
| DIS-014 | Room prefab is corrupted | Debug: delete nodes from a room scene | District generation includes that room | Game skips corrupted room with error log OR crashes gracefully |
| DIS-015 | All room prefabs are identical | Debug: force single room prefab | Generate district | District is 4-6 copies of same room (boring but valid) OR game detects and adds variety |
| DIS-016 | Evidence filtering returns 0 visible nodes | Dump stat build, all evidence gated by dominant archetype | Generate district | Room places no evidence (intended?) OR spawns universal evidence |

#### Edge Cases

- District generation during low RAM conditions (Switch at memory cap)? (Generation may fail — need fallback)
- Room exit door is blocked by spawned enemy? (Door hitbox should be clear OR enemies can't spawn near exits)
- Evidence and enemy spawn at exact same position? (Evidence should render above enemy OR spawn points should have exclusion radius)
- Path choice at debrief presents 3 identical districts? (Shouldn't happen — districts should differ by difficulty/content)

**Risk Areas:**
1. **Procedural generation creates unfair rooms** — player spawns surrounded by enemies, no escape
2. **Evidence distribution is broken** — some builds see 0 evidence in entire district
3. **Room variety feels low** — same 5 rooms repeat, layout memorization trivializes combat
4. **District generation is slow** — loading screen >5s, breaks roguelite flow

**Pass Criteria:**
- District generation completes in <0.5s on target hardware (PC and Switch)
- 100% of generated districts have at least 1 psyche-visible evidence per build type (verified with 50 runs × 4 archetypes)
- Room prefab pool is large enough that exact repeats are <10% per run
- No unfair spawns (player surrounded, evidence inaccessible) in 100 generated districts

---

### 2.8 Dialogue System

**Responsibility:** Branching dialogue trees, psyche-gated options, Insight costs, NPC state persistence.

#### Happy Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIA-001 | Dialogue starts with witness | Debrief room, witness present | Interact with witness | Dialogue UI appears, first node displays speaker name + text |
| DIA-002 | Choice presents multiple options | Node with 3 choices | View choices | 3 options displayed with text + requirements (sub-skill, Insight cost) |
| DIA-003 | Psyche-gated option is available | Authority Tier 1+, choice requires Intimidation | View choices | "[Intimidation] You're lying. Tell me the truth." is unlocked and selectable |
| DIA-004 | Psyche-gated option is locked | Authority Tier 0, choice requires Intimidation | View choices | "[Intimidation] ..." is greyed out with tooltip "Requires Intimidation" |
| DIA-005 | Insight-gated option is available | 10 Insight, choice costs 7 | View choices | Choice is unlocked and shows cost |
| DIA-006 | Insight-gated option is locked | 5 Insight, choice costs 7 | View choices | Choice is greyed out with "Not enough Insight" |
| DIA-007 | Dialogue advances to next node | Select choice | Click/press button | Next node displays, dialogue continues |
| DIA-008 | Dialogue ends at terminal node | Reach terminal node | View UI | Dialogue UI closes, returns to debrief room, evidence/Insight changes persist |

#### Sad Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIA-009 | Node with 0 choices (auto-advance) | Linear node, no choices | View node | After 2s, dialogue auto-advances OR player presses button to continue |
| DIA-010 | All choices are locked | 3 choices, all require sub-skills player doesn't have | View choices | At least 1 fallback "neutral" choice is available OR dialogue ends |
| DIA-011 | Dialogue JSON is missing next_node_id | Debug: break dialogue tree | Advance to broken node | Game logs error, ends dialogue OR shows error text |
| DIA-012 | Choice text is excessively long | Debug: 500-character choice text | View choice | Text truncates OR wraps cleanly in UI, doesn't overflow |
| DIA-013 | Speaker name is empty | Debug: speaker = "" | View node | Displays "Unknown" OR no speaker label |

#### Evil Path Tests

| Test ID | Test Case | Preconditions | Steps | Expected Result |
|---------|-----------|---------------|-------|-----------------|
| DIA-014 | Dialogue tree with 100+ nodes | Debug: long branching tree | Play through entire tree | No slowdown, all nodes display correctly, no stack overflow |
| DIA-015 | Rapid choice selection | 10 choices in sequence | Spam select button at max speed | All choices register, dialogue advances correctly, no skipped nodes |
| DIA-016 | Dialogue during combat | Debug: force dialogue trigger mid-fight | Start dialogue | Combat pauses OR dialogue is blocked (define intended), no overlap |
| DIA-017 | Circular dialogue tree | Debug: Node A → Node B → Node A | Play through | Player can loop OR game detects cycle and breaks it |
| DIA-018 | Dialogue text contains special characters | Debug: unicode, emoji, newlines | View text | Text renders correctly OR sanitizes safely |
| DIA-019 | Save/load mid-dialogue | Dialogue open, 3 nodes deep | Save and quit, reload | Dialogue resumes at start OR ends (define), NPC state persists |

#### Edge Cases

- Dialogue triggers during Internal Voice? (Dialogue should wait OR voice should be suppressed)
- NPC dialogue interrupted by player death (debrief room, unlikely but possible)? (Dialogue ends, run ends)
- Dialogue choice spends last Insight, player has 0 Insight mid-tree? (Later Insight-gated choices are now locked)
- Dialogue tree references evidence player hasn't collected? (Choice is locked OR greyed out)

**Risk Areas:**
1. **Psyche gates feel opaque** — players don't understand why choices are locked
2. **Dialogue trees are brittle** — missing nodes cause crashes or softlocks
3. **Insight costs are imbalanced** — some dialogues are trivial, others are prohibitively expensive
4. **Dialogue is skippable accidentally** — players mash button, skip important narrative

**Pass Criteria:**
- All dialogue trees load without errors (validated on 100% of authored trees)
- Psyche/Insight gate logic is 100% accurate (no false locks/unlocks)
- Dialogue UI is readable on all platforms (PC monitors, Switch handheld)
- Players can re-read dialogue text (scrollback OR persistent log)

---

## 3. Feature-Specific Test Plans

### 3.1 Roguelite Run Structure

**Scope:** Run start → district loop → death/conclusion → hub → reshuffle → next run.

#### Test Cases

| Test ID | Description | Steps | Expected Result |
|---------|-------------|-------|-----------------|
| ROG-001 | Complete full run (Districts 1-5) | Start run, clear all districts, reach case close | Run logs to meta-case board, Psyche Echo drops (1-2), psyche reshuffles, precinct hub loads |
| ROG-002 | Die in District 1 | Start run, die in first room | Death screen displays, evidence logged at 50% confidence, psyche reshuffles, hub loads |
| ROG-003 | Die in District 3 (mid-run) | Clear Districts 1-2, die in District 3 | Partial evidence logged, hub loads, player can start new run |
| ROG-004 | Abandon run (quit to menu) | Mid-district, pause menu → quit | Next launch: run is forfeit (no evidence saved) OR run resumes (define) |
| ROG-005 | 10 consecutive runs | Complete 10 runs end-to-end | All 10 runs log correctly, no slowdown, meta-case progresses |
| ROG-006 | Run length timing | Start run, complete without deaths | Run completes in 20-40 minutes (design target) |

**Edge Cases:**
- What happens if player quits during psyche reshuffle animation? (Animation completes on next launch OR restarts?)
- What happens if Districts 1-4 are completed, player dies in District 5 boss? (Death penalty applies OR completion bonus applies?)

**Pass Criteria:**
- 100 runs completed without softlock or crash
- Average run length is 20-40 minutes (verified with 20 full-clear runs)
- Psyche reshuffle never generates invalid build
- Meta-case board progresses consistently (Layer 1 by Run 3-4, Layer 2 by Run 10-15)

---

### 3.2 Archetype Balance

**Scope:** All 4 archetypes feel distinct, viable, and balanced in combat effectiveness and case access.

#### Test Matrix

| Archetype | Combat Difficulty | Narrative Access | Insight Efficiency | Playtest Viability (Districts 1-3) |
|-----------|-------------------|------------------|--------------------|------------------------------------|
| Authority | Easy (high HP/damage) | Moderate | Low (brute force) | Should clear reliably |
| Empathy | Easy (high evasion) | High | High (charm bypasses) | Should clear reliably |
| Logic | Moderate (setup-dependent) | Moderate | Highest (traps) | Should clear with strategy |
| Electrochemistry | Hard (glass cannon) | Low (niche) | Moderate (fast clears) | Requires skill, high risk |

#### Test Protocol

1. **Combat Viability Test:**
   - QA tester with 10 hours experience plays 10 runs per archetype (40 total)
   - Record: districts cleared, deaths, time to complete
   - Target: All archetypes can clear Districts 1-3 reliably (70%+ success rate)

2. **Narrative Access Test:**
   - 10 runs per archetype, record evidence collected and conclusions reached
   - Target: Authority/Logic reach 3+ conclusions, Empathy reaches 5+ conclusions, Electrochemistry reaches 2+ conclusions (by design)

3. **Subjective Feel Test:**
   - Blind playtest: 10 testers, each plays 1 hour of each archetype
   - Survey: "Which archetype feels most fun? Most challenging? Most distinct?"
   - Target: No archetype is unanimously "worst" or "best" — preference varies

**Edge Cases:**
- Hybrid builds (Authority 7 / Empathy 6): Do they feel distinct or muddled?
- Dump stat builds (Authority 12 / others at 4/4/4): Is dominant archetype overpowering?
- Balanced builds (6/6/6/6): Does game assign dominant correctly?

**Risk Areas:**
1. **Empathy trivializes combat** — telegraph reading + i-frames = invincible
2. **Electrochemistry is unfun** — combo reset on damage feels too punishing
3. **Logic feels passive** — trap setup is boring compared to Authority brawling
4. **Archetypes feel samey** — attack animations are too similar

**Pass Criteria:**
- All archetypes clear Districts 1-3 with 70%+ success (QA tester, 10 hrs experience)
- Subjective survey: "Archetypes feel distinct" — 80%+ agree
- No archetype has <10% pick rate in open beta (implies imbalance)

---

### 3.3 Insight Economy Balance

**Scope:** Validate that Insight scarcity creates tension without being punishing.

#### Test Protocol

1. **Insight Budget Validation:**
   - 50 full runs (Districts 1-5 clear), record Insight earned per district
   - Target: Total run Insight = 50-66 (design spec)
   - Variance: <15% from expected (no RNG outliers)

2. **Spending Tension Test:**
   - 20 runs, record debrief choices (combat, narrative, split)
   - Survey QA testers: "Did you agonize over Insight spend?"
   - Target: 70%+ report "yes, difficult choices"

3. **Starvation Test:**
   - 10 runs where player ONLY spends on narrative
   - 10 runs where player ONLY spends on combat
   - Result: Both paths are viable (can reach case close, can survive) but suboptimal

4. **Generosity Test:**
   - If players consistently have 10+ unspent Insight at run end, economy is too generous
   - Target: <5 unspent Insight at run end (players spent nearly everything)

**Edge Cases:**
- Player skips all Insight spending (hoarding)? (Run is harder but not impossible)
- Player dies with 30 unspent Insight? (Wasted potential — intended consequence)

**Risk Areas:**
1. **Economy is too tight** — players feel forced into "always combat" or "always narrative"
2. **Economy is too loose** — players can afford everything, no tension
3. **Drop rates feel random** — one run drops 80 Insight, next run drops 30

**Pass Criteria:**
- 50 runs: Insight budget is 50-66 with <15% variance
- Debrief tension survey: 70%+ report agonizing over spend
- No "dominant strategy" emerges (always combat OR always narrative)

---

### 3.4 Meta-Case Pacing

**Scope:** Conspiracy layers unlock at correct cadence, connections appear at intended rate.

#### Test Protocol

1. **Layer 1 Unlock Timing:**
   - 50 fresh playthroughs, record when first connection appears
   - Target: Run 3-4 (design spec)
   - Variance: ±1 run acceptable

2. **Layer 2-5 Unlock Timing:**
   - Continue 20 playthroughs to Layer 5
   - Record unlock timings:
     - Layer 1: Run 3-4
     - Layer 2: Run 6-15
     - Layer 3: Run 16-25
     - Layer 4: Run 26-35
     - Layer 5: Run 36+

3. **Connection Density Test:**
   - After 10 runs, count evidence connections on board
   - Target: 5-10 connections (enough to feel revelatory, not overwhelming)

4. **Dead End Test:**
   - Play 20 runs with deliberate "bad" archetype choices (always skip case-relevant evidence)
   - Result: Player should still see SOME connections (universal evidence provides fallback)

**Edge Cases:**
- Player focuses only on one archetype (10 Authority runs in a row)? (Stalls at Layer 2, needs other archetypes for progression — intended)
- Player reaches Layer 5 in 20 runs (speedrun)? (Possible with optimal evidence farming — acceptable)

**Risk Areas:**
1. **Layer 1 unlocks too late** — players churn before experiencing hook
2. **Connections are invisible** — board shows fragments but no threads, players feel stuck
3. **Meta-case feels grindy** — requires 50+ runs to see progression

**Pass Criteria:**
- Layer 1 unlocks by Run 3-4 in 90%+ of playthroughs
- Layer 2 unlocks by Run 15 in 90%+ of playthroughs
- Playtest survey: "Meta-case feels rewarding" — 80%+ agree

---

## 4. Platform-Specific Testing

### 4.1 PC (Steam)

#### Input Testing

| Test ID | Description | Controllers | Expected Result |
|---------|-------------|------------|-----------------|
| PC-001 | Keyboard + mouse controls | WASD + mouse | Movement, attacks, UI navigation all functional |
| PC-002 | Xbox controller | Xbox One / Series controller | Full gamepad support, button prompts correct |
| PC-003 | PlayStation controller | PS4 / PS5 DualSense | Full support, button prompts correct (Cross = A, Circle = B) |
| PC-004 | Generic gamepad | Third-party controller | Basic support OR graceful fallback to keyboard prompts |
| PC-005 | Hot-swap input | Start with keyboard, plug in controller mid-game | Input switches seamlessly, prompts update |

#### Graphics Testing

| Test ID | Description | Hardware | Expected Result |
|---------|-------------|----------|-----------------|
| PC-006 | Min spec performance | GTX 1050, 8GB RAM | 60 FPS in combat, <50ms frame time |
| PC-007 | High spec performance | RTX 3070, 16GB RAM | 60 FPS locked, <10ms frame time |
| PC-008 | Resolution scaling | 1080p, 1440p, 4K | UI scales correctly, text readable, no distortion |
| PC-009 | Ultrawide support | 21:9 monitor | No stretching, UI elements positioned correctly |
| PC-010 | Multi-monitor | 2-3 monitors | Game runs on primary, doesn't break UI |

#### Steam Integration

| Test ID | Description | Expected Result |
|---------|-------------|-----------------|
| PC-011 | Cloud saves | Save on PC A, load on PC B | Save syncs, meta-case board intact |
| PC-012 | Achievements | Trigger achievement condition | Steam achievement unlocks, notification appears |
| PC-013 | Overlay | Open Steam overlay mid-game | Game pauses, overlay functional, no crash |
| PC-014 | Big Picture mode | Launch via Big Picture | Controller input works, UI scales for TV |

**Edge Cases:**
- Alt-tab during combat? (Game pauses OR continues — define)
- Windows key pressed mid-run? (Minimize gracefully, no crash)
- Steam offline mode? (Game launches, cloud saves disabled)

**Pass Criteria:**
- 60 FPS locked on min spec hardware (GTX 1050)
- All input methods functional (keyboard, Xbox, PS, generic)
- Steam features (cloud saves, achievements) work 100%

---

### 4.2 Nintendo Switch

#### Performance Testing

| Test ID | Description | Mode | Expected Result |
|---------|-------------|------|-----------------|
| SWI-001 | Combat performance | Handheld (720p) | 30 FPS minimum, 60 FPS target |
| SWI-002 | Combat performance | Docked (1080p) | 60 FPS target, no drops below 50 |
| SWI-003 | District load time | Any mode | <3 seconds from debrief to next district |
| SWI-004 | Memory usage | Any mode | <1.5GB runtime (OS reserves ~1GB) |
| SWI-005 | Battery life | Handheld | 3+ hours on full charge |

#### Input Testing

| Test ID | Description | Controllers | Expected Result |
|---------|-------------|------------|-----------------|
| SWI-006 | Joy-Con (handheld) | Both Joy-Cons attached | Full control, no drift issues (if drift exists, compensate) |
| SWI-007 | Joy-Con (detached) | Wireless Joy-Cons | Full control, reconnect seamlessly if disconnected |
| SWI-008 | Pro Controller | Switch Pro Controller | Full control, HD rumble functional (if implemented) |
| SWI-009 | Controller disconnect | Disconnect controller mid-combat | Game pauses, "Reconnect controller" prompt, resumes cleanly |

#### Switch-Specific Features

| Test ID | Description | Expected Result |
|---------|-------------|-----------------|
| SWI-010 | Sleep mode | Put Switch to sleep mid-run, wake after 1 hour | Game resumes exactly where it paused, no data loss |
| SWI-011 | Home menu | Press Home mid-combat | Game pauses, returns to exact state on resume |
| SWI-012 | Screenshot | Press capture button | Screenshot saves, game continues (no hitch) |
| SWI-013 | Multiple users | User A plays, switches to User B | Save data is per-user, no cross-contamination |

#### Lotcheck Compliance

| Requirement | Status | Notes |
|-------------|--------|-------|
| ESRB Rating | T (Teen) | Violence, mild language, thematic elements |
| Suspend/Resume | Pass | Must resume cleanly from sleep |
| User switching | Pass | Save data per user |
| Error handling | Pass | No crashes, graceful error messages |
| Controller support | Pass | All official controllers supported |

**Edge Cases:**
- Battery dies mid-save? (Save completes OR next boot recovers)
- Switch overheats (rare but possible in summer)? (Game throttles OR OS force-closes)
- eShop download interrupted? (Redownload works, no corruption)

**Pass Criteria:**
- 30 FPS minimum in all scenarios (handheld and docked)
- No crashes in 100-hour stress test
- Sleep/resume works 100% (critical Lotcheck requirement)
- Lotcheck submission passes on first attempt (or define fix timeline)

---

## 5. Regression Testing

**When:** After every major bug fix, before each milestone, before launch.

**Scope:** Re-run all critical path tests to ensure fixes didn't break existing functionality.

### 5.1 Regression Test Suite

**Core Systems (Run on Every Build):**
- Psyche generation (PSY-001 to PSY-004)
- Combat loop (COM-001 to COM-006)
- Insight economy (INS-001 to INS-006)
- Save/load (MET-001, MET-005)
- Evidence collection (CRE-001, CRE-003, CRE-004)

**Full Suite (Run Weekly, Before Milestones):**
- All Happy Path tests
- All Sad Path tests (prioritized by risk)
- Platform-specific tests (PC and Switch)

**Regression Checklist Template:**

```
Build: [version]
Date: [date]
Tester: [name]

CORE SYSTEMS:
[ ] Psyche generation works
[ ] Combat is responsive
[ ] Insight economy is balanced
[ ] Save/load works
[ ] Evidence collection works

KNOWN ISSUES (fixed this build):
[ ] [Bug ID] - [Description] - VERIFIED FIXED / REGRESSED

NEW ISSUES FOUND:
- [List any new bugs discovered during regression]

PASS / FAIL: [overall result]
```

**Regression Failure Protocol:**
- If ANY core system fails regression, build is BLOCKED
- Fix must be prioritized, new build tested
- No milestone sign-off until regression passes

---

## 6. Risk Assessment

### 6.1 Critical Risks (Could Kill the Game)

**Risk 1: Save Corruption**
- **Likelihood:** Low (if save system is well-tested)
- **Impact:** FATAL (players lose 30+ hours, 1-star reviews, reputation damage)
- **Mitigation:**
  - Save/load stress test: 1000 iterations
  - Power loss simulation (force quit during save)
  - Corrupted save recovery path (backup saves, graceful degradation)
  - Beta test: monitor save-related crash reports with highest priority
- **Test Priority:** 1 (test first, test most)

**Risk 2: Combat Feels Unresponsive**
- **Likelihood:** Medium (tight frame budget, complex state machine)
- **Impact:** High (core loop fails, players refund)
- **Mitigation:**
  - Profile combat update loop on min spec hardware
  - Input lag <100ms (measured with high-speed camera)
  - Animation canceling is consistent (dodge always interrupts)
  - 60 FPS locked on PC, 30 FPS minimum on Switch
- **Test Priority:** 1

**Risk 3: Case Refraction Feels Random**
- **Likelihood:** High (complex system, subjective feel)
- **Impact:** High (unique selling proposition fails)
- **Mitigation:**
  - Every evidence node has documented "psychological rationale"
  - Playtest survey: "Do you understand why you can/can't see evidence?"
  - UI feedback when evidence is invisible ("Your [Archetype] doesn't perceive this")
  - Tutorial explains Case Refraction explicitly
- **Test Priority:** 2

**Risk 4: Meta-Case Progression Stalls**
- **Likelihood:** Medium (content pacing is hard to tune)
- **Impact:** High (long-term hook fails, players churn)
- **Mitigation:**
  - Verify Layer 1 unlocks by Run 3-4 (50 playthroughs)
  - Telemetry in beta: track when players stop playing (churn at which run count?)
  - Fallback: adjust conspiracy layer unlock thresholds in patch
- **Test Priority:** 2

---

### 6.2 High Risks (Could Hurt the Game)

**Risk 5: Insight Economy Imbalance**
- **Likelihood:** High (difficult to balance)
- **Impact:** Medium (game feels too easy/hard, fixable post-launch)
- **Mitigation:** 50+ runs, record Insight earned/spent, tune drop rates
- **Test Priority:** 3

**Risk 6: Archetype Imbalance**
- **Likelihood:** Medium (4 archetypes with different power curves)
- **Impact:** Medium (players avoid "bad" archetype, reduces variety)
- **Mitigation:** Playtest all archetypes, track clear rates, buff/nerf
- **Test Priority:** 3

**Risk 7: Internal Voices Feel Like QTEs**
- **Likelihood:** Medium (subjective feel)
- **Impact:** Medium (mechanic is resented, not engaged)
- **Mitigation:** Playtest survey, adjust frequency/timing, make narrative text compelling
- **Test Priority:** 3

**Risk 8: Switch Performance <30 FPS**
- **Likelihood:** Medium (2D game should run fine, but complex rooms may drop frames)
- **Impact:** Medium (bad reviews on Switch, fixable with optimization)
- **Mitigation:** Profile early, reduce enemy count/particles on Switch, 30 FPS cap if needed
- **Test Priority:** 3

---

### 6.3 Medium Risks (Annoying but Manageable)

**Risk 9: Dialogue Trees are Brittle**
- **Mitigation:** Automated JSON validation, editor tool with error checking
- **Test Priority:** 4

**Risk 10: Evidence Spawns Inside Walls**
- **Mitigation:** Spawn point collision checks, manual QA pass on all rooms
- **Test Priority:** 4

**Risk 11: UI Doesn't Scale on Switch Handheld**
- **Mitigation:** Test all UI screens on Switch handheld (720p), adjust font sizes
- **Test Priority:** 4

---

## 7. Quality Gates (What Must Pass Before Shipping)

### 7.1 Milestone Quality Gates

**M3: Vertical Slice (Month 6-9)**
- Core loop (30-second, 5-minute, session) is functional
- 1 full run (5 districts, case close) completes without crash
- Combat feels responsive (subjective, team vote)
- Meta-case board displays evidence correctly

**M6: Content Complete (Month 12-15)**
- All 4 archetypes playable, distinct, viable
- Case Refraction shows 10+ distinct conclusions across builds
- Insight economy is balanced (QA survey: tension is real)
- 50 runs completed without progression block

**M7: Beta (Month 18-20)**
- Save/load works 100% (1000 save/load cycles, no corruption)
- PC performance: 60 FPS locked on min spec
- Switch performance: 30 FPS minimum in all scenarios
- Closed beta: <10 critical bugs reported, all resolved

**M8: Launch (Month 20-24)**
- Zero known critical bugs (crash, save corruption, progression block)
- <5 known high-priority bugs (annoying but not blocking)
- Platform compliance: Steam launch ready, Switch Lotcheck passed
- All regression tests pass

---

### 7.2 Launch Quality Gate

**BLOCKER Bugs (Must Fix Before Launch):**
- Any crash that is reproducible
- Save corruption under any circumstance
- Progression block (cannot complete run, cannot unlock Layer 1)
- Combat softlock (player/enemy stuck, cannot move/attack)
- Performance <60 FPS on min spec PC OR <30 FPS on Switch

**HIGH Priority (Fix Before Launch OR Day 1 Patch):**
- Visual bugs (missing textures, broken animations)
- Audio bugs (missing sounds, music doesn't loop)
- Exploits (Insight duplication, infinite combo)
- Balance issues (one archetype is 2x stronger than others)

**MEDIUM Priority (Can Ship, Fix in Patch):**
- Minor UI issues (text overflow, button misalignment)
- Rare edge case bugs (<1% repro rate)
- Localization errors (if non-English languages are supported)

**LOW Priority (Polish, Post-Launch):**
- Quality-of-life features (dialogue skip, run statistics screen)
- Cosmetic improvements (particle effects, screen shake)

---

## 8. Test Data & Tooling

### 8.1 Test Save Files

**Pre-Generated Saves for QA:**
- `fresh_save.dat` — Run 0, blank board, 0 Echoes
- `early_game.dat` — Run 5, Layer 1 unlocked, 10 Echoes
- `mid_game.dat` — Run 15, Layer 2-3 unlocked, 25 Echoes
- `late_game.dat` — Run 30, Layer 4 unlocked, 50 Echoes
- `endgame.dat` — Run 50, Layer 5 complete, 100 Echoes
- `corrupted_save.dat` — Intentionally broken JSON (for recovery testing)

**Save File Generation Script:**
```python
# generate_test_saves.py
# Automates creation of test save files with specific run counts, evidence, etc.
```

---

### 8.2 Debug Tools (In-Game, Dev Builds Only)

**Cheat Menu (F12 Key):**
- Instant run completion (skip to case close)
- Set Insight to any value
- Set Psyche Echoes to any value
- Force specific psyche build (override generation)
- Unlock all conspiracy layers
- God mode (invincible, infinite Insight)
- Spawn specific evidence in room
- Teleport to any district
- Display hitboxes/hurtboxes
- Framerate counter, memory usage overlay

**Console Commands:**
```
/give_insight 100
/set_archetype authority 12
/unlock_layer 3
/spawn_evidence bruises_on_arms
/teleport district_3
/godmode
```

---

### 8.3 Automated Testing

**Unit Tests (GDScript via GUT):**
- `test_psyche_profile.gd` — Validate point distribution, tier calculation
- `test_evidence_database.gd` — Validate evidence loading, filtering
- `test_insight_manager.gd` — Validate spend logic, counter updates
- `test_case_refraction.gd` — Validate conclusion assembly

**Integration Tests:**
- `test_run_lifecycle.gd` — Start run, complete district, end run, verify save
- `test_psyche_reshuffle.gd` — Complete 10 runs, verify no duplicate builds in a row

**Performance Tests:**
- `profile_combat_loop.gd` — Measure frame time with 10 enemies on screen
- `profile_district_generation.gd` — Measure generation time, verify <0.5s

**Run Automated Tests:**
```bash
godot --headless --script res://tests/run_all_tests.gd
```

---

### 8.4 Bug Tracking

**Tool: GitHub Issues (or Jira, Linear, etc.)**

**Bug Report Template:**
```
Title: [Short description]

Severity: BLOCKER / HIGH / MEDIUM / LOW
Component: Psyche / Combat / Case / Insight / Meta-Case / UI / Audio
Platform: PC / Switch / Both

Repro Steps:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Expected Result: [What should happen]
Actual Result: [What actually happens]

Repro Rate: 100% / 50% / Rare (<10%)

Additional Info:
- Build version: [version]
- Save file: [attached if relevant]
- Video/screenshots: [attached]
```

**Bug Triage Process:**
1. **Report** — Tester files bug with template
2. **Triage** — Lead reviews, assigns severity/priority
3. **Assign** — Bug assigned to programmer
4. **Fix** — Programmer fixes, marks "Ready for QA"
5. **Verify** — Tester re-tests, marks "Verified Fixed" or "Reopened"
6. **Close** — After regression pass, bug is closed

---

## 9. Playtesting Protocol

### 9.1 Internal Playtest (Weekly, M3-M8)

**Participants:** Core team (4-5 people)
**Duration:** 1-hour playtest session
**Format:** Everyone plays simultaneously, silent observation, then group feedback

**Feedback Form:**
- What felt good this week?
- What felt broken/frustrating?
- Rate combat responsiveness (1-10)
- Rate Insight tension (1-10)
- Rate clarity of Case Refraction (1-10)
- Any bugs encountered?

**Deliverable:** Bug reports + playtest summary doc

---

### 9.2 External Playtest (Monthly, M6-M8)

**Participants:** Friends, Discord community (10-15 people)
**Duration:** 2-hour playtest, remote
**Format:** Playtest build + feedback survey + optional interview

**Feedback Survey:**
- How many runs did you complete?
- Which archetype did you prefer? Why?
- Did you understand the Insight economy?
- Did Case Refraction feel meaningful or random?
- Did the meta-case hook you?
- Rate overall fun (1-10)
- Would you buy this game? (Yes / Maybe / No)

**Deliverable:** Survey results + interview notes + bug reports

---

### 9.3 Closed Beta (Month 18-20)

**Participants:** 100 players (recruited via mailing list, Discord, Reddit)
**Duration:** 2 weeks
**Format:** Steam beta branch OR itch.io build + feedback form + telemetry

**Telemetry Tracked:**
- Runs completed
- Deaths per run
- Archetype distribution (are all archetypes played equally?)
- Insight spend split (combat vs narrative)
- Run length (average time per run)
- Churn point (which run count do players stop playing?)

**Feedback Survey:**
- Same as external playtest survey
- Additional: "What made you stop playing?" (if they did)

**Deliverable:** Telemetry report + survey analysis + prioritized bug list

---

## 10. Definition of "Works"

Here's what "works" means. These are non-negotiable.

**Combat Works:**
- Input lag <100ms (measured)
- Attack hitboxes are accurate (95%+ visual match)
- Dodge i-frames are consistent (100% invuln during window)
- Enemy AI doesn't get stuck (0% stuck rate in 100 rooms)
- 60 FPS on PC min spec, 30 FPS on Switch

**Case Refraction Works:**
- Evidence visibility matches archetype requirements (100% accuracy)
- Every archetype build sees 3+ evidence per district (100 runs tested)
- Case conclusions are reachable (all 10 conclusions reached in testing)
- Meta-case connections appear correctly (shared meta_tags create threads)

**Insight Economy Works:**
- Run budget is 50-66 Insight (verified with 50 runs)
- Players report tension in 70%+ of debriefs (playtest survey)
- No dominant strategy (combat-only OR narrative-only is suboptimal)

**Save System Works:**
- Save/load 1000 times, no corruption
- Power loss during save doesn't corrupt file
- Meta-case board persists correctly across sessions

**Meta-Case Works:**
- Layer 1 unlocks by Run 3-4 (90%+ of playthroughs)
- Evidence threads appear when tags match (100% accuracy)
- Conspiracy layers unlock at design cadence (verified with 20 full playthroughs)

**Performance Works:**
- PC: 60 FPS locked on GTX 1050, 8GB RAM
- Switch: 30 FPS minimum in handheld and docked
- District load time <3 seconds
- Memory usage <2GB PC, <1.5GB Switch

**Polish Works:**
- UI is readable on Switch handheld (720p)
- Audio never cuts out or loops incorrectly
- Animations are smooth (no jitter, no frame skips)
- Tutorial explains core mechanics clearly (playtest: 80%+ understand after tutorial)

Define "works." Then test until it does. Ship when it works. Not before.

---

## 11. Post-Launch Support Plan

**Week 1 Hotfix:**
- Monitor crash reports, prioritize any new crashes
- Monitor save corruption reports (highest priority)
- Monitor Steam reviews for blockers

**Month 1 Patch:**
- Balance adjustments (archetype buffs/nerfs, Insight tuning)
- Bug fixes (high-priority bugs that slipped through)
- QOL improvements (based on player feedback)

**Month 3 Patch:**
- Content additions (stretch goals: Psyche Blending, Partner System)
- More balance tuning
- Platform-specific optimizations (if needed)

---

## 12. Final QA Checklist (Before Launch)

**Critical Path:**
- [ ] Fresh save → Run 1 → Run 5 → Run 10 → Run 20 completes without crash
- [ ] All 4 archetypes are playable and distinct
- [ ] Save/load works 100% (1000 iterations tested)
- [ ] Combat feels responsive (team consensus)
- [ ] Case Refraction feels meaningful (playtest survey: 70%+ agree)
- [ ] Meta-case Layer 1 unlocks by Run 3-4

**Platform:**
- [ ] PC: 60 FPS on min spec, all input methods work
- [ ] Switch: 30 FPS minimum, sleep/resume works, Lotcheck passed

**Content:**
- [ ] All evidence nodes are authored and tested
- [ ] All dialogue trees load without errors
- [ ] All case conclusions are reachable
- [ ] All conspiracy layers unlock correctly

**Bugs:**
- [ ] Zero known BLOCKER bugs
- [ ] <5 known HIGH bugs (all documented, fix planned for Day 1 OR acceptable to ship)

**Regression:**
- [ ] All core system tests pass
- [ ] No regressions from last milestone

**Polish:**
- [ ] UI is readable on all platforms
- [ ] Audio is balanced and loops correctly
- [ ] Animations are smooth
- [ ] Tutorial is clear

**Sign-Off:**
- [ ] CRASH (QA Lead): Approved
- [ ] REED (Game Designer): Approved
- [ ] BYTE (Lead Programmer): Approved
- [ ] CLOCK (Producer): Approved

---

**Once this checklist is complete, the game ships.**

**Not before.**

---

**CRASH, QA Lead**
**2026-02-07**

*Define "works." Test until it does. Ship when it works.*
