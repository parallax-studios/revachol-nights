# REVACHOL NIGHTS -- Game Design Document

**Author**: REED, Game Designer
**Status**: Complete First Pass -- Ready for Prototyping
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Player Fantasy

### Fantasy Statement

**"I am a fractured detective piecing together a murder that changes shape depending on which version of me is doing the looking -- and every version is telling the truth."**

The player fantasy operates on two simultaneous axes. The first is the **detective power fantasy**: I am sharp, I am dangerous, I am closing in on the truth. The second is the **identity vertigo fantasy**: I am not one person, I am many, and the truth bends around whoever I am this time. Most detective games deliver the first axis. Most experimental narrative games deliver the second. Revachol Nights delivers both in the same 30-second window -- you are swinging a baton through a corrupt cop's guard AND realizing that the evidence you just found only exists because you have the psychological profile to perceive it.

What's the loop? The loop is this: I fight, I discover, I interpret, I conclude, I die, I become someone else, and the discovery changes. The fantasy is not "I solve the case." The fantasy is "I solve myself, and the case follows."

### What This Feels Like

- **Hour 1**: Confusion wrapped in kinetic pleasure. The combat feels great. The case is a fog. You don't understand Case Refraction yet -- you just know something strange is happening when the evidence doesn't match your last run.
- **Hour 5**: The first click. You realize that your Empathy-dominant run literally showed you evidence your Logic-dominant run could not see. You start thinking about psyche builds as investigative tools, not just combat loadouts.
- **Hour 20**: Mastery territory. You read a psyche shuffle and immediately know which meta-case threads this build can pursue. You optimize Insight spending not for survival but for narrative access. You stop fighting the reshuffle and start *reading* it. How does this feel at hour 20? It feels like becoming a better detective by becoming a better player.
- **Hour 50+**: The meta-case is nearly complete. You are selecting which evidence to pursue with surgical precision. Every run is a targeted investigation. The combat is second nature; the real game is the conspiracy board.

---

## 2. Core Loop Architecture

### 2.1 The 30-Second Loop (Moment-to-Moment)

```
                    +------------------+
                    |   ENTER ROOM     |
                    +--------+---------+
                             |
                    +--------v---------+
                    |  READ ENCOUNTER  |
                    | (enemies, layout,|
                    |  environmental   |
                    |  objects)         |
                    +--------+---------+
                             |
              +--------------+--------------+
              |                             |
     +--------v---------+         +--------v---------+
     |     FIGHT         |         |  INTERNAL VOICE  |
     | (archetype-       |<------->|  INTERRUPTION     |
     |  specific combat  |         | (skill check pop- |
     |  verbs)           |         |  up: pass/fail)   |
     +--------+---------+         +--------+---------+
              |                             |
              +--------------+--------------+
                             |
                    +--------v---------+
                    |  COLLECT DROPS   |
                    | - Insight        |
                    | - Evidence frag  |
                    | - Psyche echo    |
                    +--------+---------+
                             |
                    +--------v---------+
                    |  NEXT ROOM       |
                    +------------------+
```

**What the player DOES in 30 seconds**: Enter a room. Identify threats. Execute combat using their psyche-determined kit (Authority smashes, Empathy evades and reads, Logic traps, Electrochemistry blitzes). Mid-combat, an Internal Voice fires -- a 1.5-second skill check window that demands a snap decision. Clear the room. Pick up Insight and evidence fragments. Move to the next room.

**Why this works**: The combat is the Dead Cells axis -- tight, responsive, learnable. The Internal Voice interruptions are the Disco Elysium axis -- your fractured psyche intruding on the action. The 30-second loop is not "fight then talk." It is "fight WHILE your brain talks to you." That simultaneity is the core feel.

### 2.2 The 5-Minute Loop (District Cycle)

```
     +------------------+
     |  CLEAR DISTRICT  |
     | (4-6 rooms)      |
     +--------+---------+
              |
     +--------v---------+
     |  DISTRICT DEBRIEF |
     | Safe room with:   |
     | - Witness/suspect |
     | - Insight shop    |
     | - Case board node |
     +--------+---------+
              |
     +--------v---------+       +-------------------+
     |  SPEND INSIGHT    +------>  COMBAT UPGRADE   |
     |  (THE TENSION)    |       | (survive better)  |
     |                   +------>+-------------------+
     |                   |
     |                   +------>+-------------------+
     |                   |       | NARRATIVE UNLOCK  |
     +--------+---------+       | (interrogate,     |
              |                  |  examine evidence) |
              |                  +-------------------+
     +--------v---------+
     |  CHOOSE PATH      |
     | (2-3 branching    |
     |  districts, each  |
     |  with different   |
     |  difficulty AND    |
     |  case content)    |
     +--------+---------+
              |
     +--------v---------+
     |  NEXT DISTRICT    |
     +------------------+
```

**What the player DOES in 5 minutes**: Complete a district of 4-6 rooms. Enter the safe room. Encounter a witness or suspect -- but dialogue options are gated behind both Insight spending and psyche build. Decide: do I spend Insight to unlock that witness's testimony (advancing the case) or upgrade my combat kit (surviving the next district)? Choose which district to enter next, knowing that harder districts contain higher-value evidence but tougher fights.

**The Insight tension in practice**: A typical district drops 8-12 Insight. A meaningful combat upgrade costs 6-8. A meaningful narrative unlock costs 5-10. You cannot afford both. Every debrief room is a gut-check: am I a detective or a survivor? This single resource split is the strategic heart of the game. Where's the depth? Right here. An optimal player learns to read which narrative unlocks connect to their current meta-case threads and skips the rest, freeing Insight for combat. A new player agonizes. Both experiences are valid.

### 2.3 The Session Loop (20-40 Minutes)

```
     +------------------+
     |   RUN BEGINS     |
     | Psyche shuffle   |
     | Archetype reveal |
     +--------+---------+
              |
     +--------v---------+
     | DISTRICTS 1-5    |
     | (escalating      |
     |  difficulty)     |
     +--------+---------+
              |
         +----+----+
         |         |
    +----v---+ +---v----+
    | DEATH  | | CASE   |
    | (fail) | | CLOSE  |
    +----+---+ +---+----+
         |         |
         +----+----+
              |
     +--------v---------+
     |  PRECINCT HUB    |
     | - Meta-case board |
     | - Evidence pinned |
     | - Contradiction   |
     |   flagged         |
     +--------+---------+
              |
     +--------v---------+
     | PSYCHE RESHUFFLE |
     | New archetype    |
     | weights assigned  |
     +--------+---------+
              |
     +--------v---------+
     |   NEXT RUN       |
     +------------------+
```

**What the player DOES in a session**: Begin a run with a shuffled psyche build. Fight through 4-5 escalating districts, making Insight allocation decisions at each debrief. Either die or reach a case conclusion (accuse a suspect based on accumulated evidence). Return to the precinct hub. Pin new evidence to the meta-case board. Observe contradictions with previous runs. Receive a new psyche shuffle. Begin again.

**Why death works**: Death is not failure. Death is information. You saw 3 of 5 districts. You gathered partial evidence. That evidence still pins to the meta-case board (at reduced value). The reshuffle gives you a new lens. The player who dies in District 3 still progresses -- they just progress slower than the player who reached a case close. This is the Hades model: death is a narrative beat, not a punishment.

---

## 3. Core Mechanics -- Full Specification

### 3.1 Psyche Build System

**Player verb**: Discover who you are this run and adapt your playstyle accordingly.

**System description**: At run start, the game generates a psyche profile by distributing 24 points across 4 archetypes (Authority, Empathy, Logic, Electrochemistry). Distribution is weighted random, with a guaranteed dominant archetype (8-12 points) and a guaranteed dump stat (1-3 points). The remaining points spread across the other two.

Each archetype has 6 sub-skills. Sub-skills activate at thresholds:

| Threshold | Points in Archetype | Effect |
|-----------|-------------------|--------|
| Tier 0 | 0-2 | Sub-skills inactive. No access to archetype combat verbs. |
| Tier 1 | 3-5 | 2 sub-skills active. Basic combat verb available. |
| Tier 2 | 6-8 | 4 sub-skills active. Advanced combat verb unlocked. |
| Tier 3 | 9-12 | All 6 sub-skills active. Signature ability unlocked. |

**The Four Archetypes in Combat**:

**AUTHORITY** (The Hammer)
- Movement: Slow, heavy, forward-committed. Short dodge with armor frames.
- Primary verb: Heavy melee strikes with wide arcs. Stagger-focused.
- Advanced verb: Crowd control slams that create knockback zones.
- Signature: COMMANDING PRESENCE -- a shout that stuns all enemies in range for 2 seconds and forces the nearest enemy to attack their allies for 4 seconds.
- Sub-skills: Intimidation (stagger bonus), Endurance (HP pool), Composure (poise during attacks), Volition (death-defiance proc), Esprit de Corps (ally phantom summons at Tier 2+), Rhetoric (dialogue stagger -- some enemies can be mid-combat intimidated into fleeing).
- Feel: Kratos. Every hit has weight. You walk through rooms, not around them.

**EMPATHY** (The Ghost)
- Movement: Fast, fluid, generous i-frames on dodge. Longest dodge range.
- Primary verb: Light, quick strikes. Low damage per hit but high hit count.
- Advanced verb: Enemy telegraph reading -- empathy-dominant players see attack wind-up indicators 0.3 seconds earlier than other builds.
- Signature: PSYCHIC RESONANCE -- for 6 seconds, every enemy's next attack is telegraphed with a full-body glow AND dodging through an attack heals the player for 5% max HP.
- Sub-skills: Perception (telegraph visibility), Suggestion (charm short CC), Drama (decoy projections), Conceptualization (environmental interaction radius), Inland Empire (psychic damage aura at close range), Shivers (precognition -- brief future-sight showing enemy patrol paths).
- Feel: Hollow Knight's nail arts meet Celeste's dash. Precise, rewarding, dance-like.

**LOGIC** (The Architect)
- Movement: Medium speed, medium dodge. Unique: can place traps during dodge animation.
- Primary verb: Ranged attacks (thrown deduction darts -- flavored as "pinning down" the enemy with logical conclusions made physical).
- Advanced verb: Environmental exploitation -- Logic-dominant players can interact with stage hazards (electrified floors, collapsing structures, locked doors that crush enemies).
- Signature: RECONSTRUCTION -- freeze all enemies for 3 seconds while a wireframe "crime scene reconstruction" plays over the room, then deal damage to all enemies based on how many environmental hazards are in the room.
- Sub-skills: Encyclopedia (weak point identification), Visual Calculus (trajectory prediction for ranged), Interfacing (trap placement), Reaction Speed (parry window expansion), Savoir Faire (critical hit on environmental kills), Conceptualization (shared with Empathy -- if both are Tier 1+, unlocks unique hybrid environmental puzzles).
- Feel: Stealth-action hybrid. You set up the room, then execute. The chessplayer archetype.

**ELECTROCHEMISTRY** (The Maniac)
- Movement: Fastest base speed. Shortest dodge but with a damage-on-contact property. No i-frames -- you dodge INTO things.
- Primary verb: Rapid, erratic melee. Attack speed scales with combo counter. Damage increases per consecutive hit but resets on taking damage.
- Advanced verb: RUSH state -- after 10 consecutive hits without taking damage, enter a berserker mode with +50% speed and +30% damage for 5 seconds.
- Signature: CHEMICAL OVERLOAD -- consume 30% of current HP to deal 200% of that amount as AoE damage in a burst around the player, then gain 3 seconds of invulnerability. High risk. Absurd reward.
- Sub-skills: Physical Instrument (raw damage scaling), Half Light (fight-or-flight: damage boost when below 30% HP), Electrochemistry (combo speed), Pain Threshold (reduced damage from first hit in any encounter), Authority Bleed (shared with Authority -- if both Tier 1+, heavy attacks gain combo counter contribution), Inland Empire Bleed (shared with Empathy -- if both Tier 1+, psychic damage aura scales with combo counter).
- Feel: Devil May Cry's Dante. Aggressive, stylish, always on the edge. You are rewarded for recklessness.

**Hybrid builds**: Because point distribution is random, most runs produce hybrid builds. A run with Authority 9 / Electrochemistry 5 / Logic 6 / Empathy 4 yields a bruiser with trap access and basic telegraph reading. The sub-skill bleed system (where certain sub-skills are shared between archetypes) means that specific hybrid combinations unlock unique abilities that pure builds cannot access. This is where the depth ceiling lives. A player at hour 50 sees "Authority 7 / Empathy 6" and thinks "that's the Composure-Drama hybrid -- I get armored dodge with decoy projections."

**Feedback**: Archetype reveal at run start is a 3-second cinematic: the four archetype icons arrange themselves with visual weight indicating distribution. The dominant archetype's color washes over the HUD. Combat verbs are immediately available -- no tutorial gate. The player feels different within 5 seconds of starting a new run.

### 3.2 Insight Economy

**Player verb**: Choose between understanding the case and surviving the city.

**System description**: Insight is a single fungible resource that drops from combat encounters, environmental discovery, and Internal Voice successes. It has two spending channels:

**Combat Channel**:
- Tier 1 upgrades (6 Insight): +15% damage, +10% HP, +1 sub-skill activation
- Tier 2 upgrades (10 Insight): Weapon variant unlock, dodge modifier, passive ability
- Tier 3 upgrades (15 Insight): Signature ability enhancement, archetype-specific ultimate

**Narrative Channel**:
- Witness interrogation (5-8 Insight): Unlock dialogue tree with key NPC. Yields 1-3 evidence fragments.
- Evidence examination (3-5 Insight): Analyze a physical clue. Yields 1 evidence fragment + potential meta-case connection.
- Scene reconstruction (8-12 Insight): Full crime scene analysis. Yields 2-4 evidence fragments + guaranteed meta-case thread.

**Drop rates and budget per run**:
- District 1: 8-10 Insight dropped
- District 2: 10-14 Insight dropped
- District 3: 12-16 Insight dropped
- District 4: 14-18 Insight dropped
- District 5 (boss): 6-8 Insight dropped (reduced -- pressure the final decision)
- Total run budget (if full clear): 50-66 Insight
- Total cost to max combat: ~45 Insight
- Total cost to unlock all narrative nodes: ~55 Insight
- Therefore: A full-clear run can afford ~70-80% of total available upgrades + narrative. Most runs (with death around District 3-4) afford ~40-50%. The tension is real and persistent.

**Feedback**: Insight pickups trigger a brief audio chime and a particle effect in the archetype's dominant color. The HUD counter pulses. Spending Insight at debrief rooms uses a physical metaphor: combat upgrades are visualized as the detective loading a weapon or adjusting their coat; narrative unlocks are visualized as the detective pinning a photo to a board or leaning forward in an interrogation chair. The player feels the weight of the choice.

**Depth**: Expert players discover that certain narrative unlocks provide indirect combat value. Interrogating a witness about a suspect's fighting style can reveal enemy attack patterns for later districts. Examining evidence in a crime scene can reveal hidden rooms with bonus Insight. The two channels are not strictly separate -- they bleed into each other at high mastery. This rewards the player who treats the economy as a unified system rather than a binary choice.

### 3.3 Case Refraction

**Player verb**: Investigate a murder that changes shape depending on your psychological profile.

**System description**: The murder of Lena Hargate has a fixed event structure (she is dead, in the Whirling-in-Rags, on a specific date) but a refracted evidence layer. Evidence nodes are tagged with psyche requirements:

| Evidence Node | Required Archetype | What It Reveals |
|---|---|---|
| Bruises on victim's arms | Authority Tier 1+ | Signs of a struggle -- power-based motive |
| Micro-expressions on hotel CCTV | Empathy Tier 2+ | The victim was afraid of someone she knew |
| Chemical residue on windowsill | Logic Tier 1+ | Trace evidence suggesting premeditation |
| Track marks on victim's ankle | Electrochemistry Tier 1+ | The victim had a substance dependency |
| Witness breaks down crying | Empathy Tier 1+ | Emotional testimony about a relationship |
| Witness contradicts own statement | Logic Tier 2+ | Logical inconsistency revealing a cover-up |
| Witness is physically intimidated | Authority Tier 2+ | They're protecting someone powerful |
| Witness is high and rambling | Electrochemistry Tier 2+ | Seemingly incoherent testimony contains a real clue |

Each run, based on your psyche profile, you can perceive approximately 40-60% of total evidence nodes. No single run reveals everything. The case conclusion screen presents 3-4 possible suspects; the evidence you've gathered determines which accusations are available and which feel supported.

**Authored case branches**: There are 4 primary case conclusions (one per dominant archetype) and 6 hybrid conclusions (for specific archetype combinations). Total: 10 distinct authored endings per case, each with unique suspect, motive, and resolution. All 10 are "true" within their psychological frame. The meta-case layer eventually reveals why all 10 can coexist.

**Feedback**: When you encounter evidence your psyche can perceive, it glows in your archetype color and a brief Internal Voice line fires ("Your AUTHORITY recognizes the marks of someone used to giving orders"). When you encounter evidence you CANNOT perceive, it appears as a greyed-out smudge with a tooltip: "Something is here, but you can't see it." This is critical -- the player must know that they are missing things. The absence is as important as the presence.

**Depth**: At high mastery, players begin to intentionally pursue specific psyche shuffles to access specific evidence chains they know connect to their meta-case. A player who needs the Empathy Tier 2 CCTV evidence will approach an Empathy-dominant shuffle with specific Insight allocation plans. The case refraction system transforms the psyche shuffle from a random constraint into a strategic opportunity.

### 3.4 Internal Voices

**Player verb**: Respond to your own fragmenting psyche in the heat of combat.

**System description**: During combat, non-dominant psyche facets fire "voice interruptions" -- brief 1.5-second windows where a dialogue box appears with a skill check. The check is a simple binary: succeed (by pressing the correct input within the window) or fail.

**Trigger frequency**: One Internal Voice fires per room, on average. In boss rooms, 2-3 fire. They are timed to moments of tactical pressure -- mid-dodge, mid-combo, after taking a hit.

**Success effects**:
- Temporary combat buff (3-5 seconds) themed to the voice's archetype
- A narrative fragment -- one sentence that connects to the case
- +2 Insight bonus

**Failure effects**:
- Psychic damage (5-10% max HP)
- A distorted narrative fragment -- misleading case information
- No Insight

**The design intention**: Internal Voices exist to create micro-moments of Disco Elysium inside the Dead Cells combat. They are deliberately disruptive -- they break flow just enough to remind the player that this is not a normal combat game. The detective's mind is fractured. The fracture intrudes. But skilled players learn to anticipate voice timing and fold the response into their combat rhythm, treating the skill check as another combat verb rather than an interruption.

**Difficulty scaling**: Internal Voice timing windows scale with difficulty. On Standard, the window is 1.5 seconds. On Hard, 1.0 second. On Detective, 0.6 seconds. The window never goes below 0.5 seconds -- this is a design floor to prevent the mechanic from becoming pure reflex noise.

**Feedback**: Voice interruptions have a distinctive audio sting (a vinyl-scratch sound -- the "needle skipping" metaphor for a disrupted thought). The screen edges briefly tint in the voice's archetype color. Success plays a harmonic resolution; failure plays a dissonant buzz. The player's body learns the sounds before their conscious mind processes the mechanic.

### 3.5 Meta-Case Board

**Player verb**: Build a conspiracy board across dozens of runs that slowly reveals the full truth.

**System description**: The precinct hub contains a physical conspiracy board. After each run, the player pins evidence fragments, case conclusions, and witness statements to the board. The board has a hidden connection graph: when two evidence fragments from different runs share a meta-tag, a thread appears connecting them.

**Progression structure**:
- **Layer 1** (Runs 1-5): The surface case. Who killed Lena Hargate? Four contradictory answers.
- **Layer 2** (Runs 6-15): The connections. Why do all four answers implicate the same organization?
- **Layer 3** (Runs 16-25): The conspiracy. What is that organization doing in Revachol, and why did Lena have to die?
- **Layer 4** (Runs 26-35): The revelation. The detective themselves is connected to the conspiracy. The psyche shuffles are not random -- they are the result of something done to the detective.
- **Layer 5** (Runs 36+): The choice. Armed with the full picture, the player makes a final accusation that locks in a permanent ending. This ending is informed by EVERY conclusion from EVERY previous run.

**Persistence rules**:
- Evidence from completed runs pins at full value
- Evidence from death-ended runs pins at 50% value (greyed out, marked as "unconfirmed")
- Contradictory evidence is flagged with a red thread (these contradictions are themselves clues)
- The board cannot be rearranged by the player -- it auto-organizes, reflecting the detective's subconscious pattern recognition

**Feedback**: Each time a new connection thread appears on the board, a musical sting plays and the camera slowly zooms to the connection. This is a moment of revelation -- the game's equivalent of a level-up. The player is progressing not in power but in understanding.

---

## 4. Systems Interaction Map

```
     +------------------+
     |  PSYCHE BUILD    |
     +--------+---------+
              |
     Determines combat kit
     Determines visible evidence
     Determines dialogue options
              |
   +----------+----------+----------+
   |          |          |          |
+--v---+  +--v---+  +--v---+  +--v---+
|COMBAT|  |CASE  |  |INTER-|  |META- |
|SYSTEM|  |REFRAC|  |NAL   |  |CASE  |
|      |  |TION  |  |VOICES|  |BOARD |
+--+---+  +--+---+  +--+---+  +--+---+
   |          |          |          |
   +----+-----+    +-----+    +----+
        |          |          |
   +----v----------v----------v----+
   |         INSIGHT ECONOMY       |
   | (single resource, dual spend) |
   +-------------------------------+
```

### Positive Feedback Loops (Snowball Effects)

1. **Skill-Knowledge Spiral**: Better combat skill means surviving to later districts, which contain higher-value evidence, which fills the meta-case board faster, which gives the player more strategic information for future runs.

2. **Build Literacy Snowball**: Understanding psyche builds improves Insight allocation, which improves both combat performance AND narrative access, which teaches the player more about how builds work. Knowledge compounds.

3. **Internal Voice Mastery**: As players learn to consistently pass Internal Voice checks, they gain more Insight per run AND more narrative fragments, accelerating both combat and case progression simultaneously.

### Negative Feedback Loops (Rubber Banding)

1. **Insight Scarcity Ceiling**: No matter how skilled the player becomes at combat, total Insight per run is capped by district count. You cannot grind Insight within a run. This prevents over-investment in either channel from trivializing the other.

2. **Psyche Shuffle Equalization**: The random reshuffle prevents any single build mastery from dominating. A player who has perfected Authority combat will eventually get an Empathy-dominant shuffle and must adapt. Mastery is breadth, not depth in any single archetype.

3. **Meta-Case Diminishing Returns**: Later meta-case layers require evidence from specific archetype perspectives. A player who has only completed Authority runs will stall at Layer 2 until they gather Empathy, Logic, or Electrochemistry evidence. The game forces perspective diversity.

4. **Death Evidence Penalty**: Dying yields evidence at 50% value. This prevents "suicide run" strategies where players intentionally die early to farm specific evidence without engaging with combat.

### Emergent Possibilities

- **Deliberate Dump-Stat Play**: Advanced players may discover that the dump stat's Internal Voice failures produce distorted narrative fragments that, when cross-referenced on the meta-case board, reveal hidden connections. Failure becomes a tool.
- **Hybrid Build Hunting**: Players may develop preferred hybrid combinations and learn to partially manipulate the shuffle through meta-case board progression (Layer 4 reveals that certain board states influence the shuffle algorithm).
- **Pacifist Routing**: A high-Empathy player who maxes Suggestion and Drama sub-skills can theoretically charm or decoy past 60-70% of combat encounters, reaching case conclusions with minimal fighting. This is an intentional alternative playstyle that sacrifices Insight income for speed.

---

## 5. Progression Curves

### 5.1 Player Skill Progression

```
Skill
 ^
 |                                          .............. Mastery plateau
 |                                    .....
 |                               ....
 |                          ....   <- Build literacy phase
 |                     ....        (understanding hybrid synergies)
 |                ....
 |           ....   <- Combat fluency phase
 |      ....        (reliable district clears)
 |  ...   <- Orientation phase
 | .      (learning base mechanics)
 +----------------------------------------> Hours
 0    5    10    15    20    25    30    50
```

**Orientation phase (Hours 0-5)**: Player learns movement, combat verbs for 2-3 archetypes, the Insight economy basics, and encounters their first case conclusion. Internal Voices feel disruptive. Deaths are frequent and occur in Districts 1-3.

**Combat fluency phase (Hours 5-15)**: Player can reliably clear Districts 1-4 with most builds. Insight allocation becomes strategic rather than instinctive. Internal Voices are integrated into combat rhythm. First meta-case connections appear on the board.

**Build literacy phase (Hours 15-30)**: Player understands hybrid synergies, sub-skill bleed mechanics, and the relationship between psyche profiles and evidence access. Runs are targeted investigations. Deaths are rare except on deliberately risky routes. Meta-case reaches Layers 2-3.

**Mastery plateau (Hours 30-50+)**: Player reads a psyche shuffle and knows the run plan within 10 seconds. Combat is expressive rather than survival-focused. Narrative choices are optimized for meta-case progression. The game becomes a meditation on perspective and truth rather than a mechanical challenge.

### 5.2 Content Unlocks and Pacing

| Run Count | Unlocked Content | Design Intent |
|-----------|-----------------|---------------|
| Run 1 | Tutorial district, simplified psyche (2 archetypes only) | Reduce overwhelm |
| Run 2-3 | Full 4-archetype shuffle, all districts available | Core experience |
| Run 5 | Meta-case board tutorial, first thread connections | Long-term hook reveal |
| Run 8-10 | District variants (alternate room layouts per district) | Environmental freshness |
| Run 12-15 | Internal Voice difficulty increase, new enemy types | Mechanical refresh |
| Run 20 | Meta-case Layer 3, conspiracy evidence type introduced | Narrative escalation |
| Run 25-30 | Boss variants that change with psyche build | Combat endgame |
| Run 35+ | Final accusation available, ending branches | Narrative endgame |

### 5.3 New Mechanic Introduction Cadence

The game follows a strict **introduce-then-test** pattern:

1. **Introduce** a mechanic in a safe or low-stakes context (e.g., Internal Voices first appear in a scripted, easy encounter in Run 1).
2. **Test** the mechanic in an unscripted, stakes-carrying context within 2-3 rooms.
3. **Combine** the mechanic with a previously introduced mechanic within 1-2 districts.
4. **Subvert** the mechanic -- present a situation where the obvious use of the mechanic is wrong (e.g., an Internal Voice check where failing is actually more narratively valuable).

No new core mechanics are introduced after Run 10. Everything after Run 10 is new content, new combinations, and new contexts for existing mechanics. This is a firm design rule. The player should never feel like the game is still teaching them past the midpoint of the meta-case progression.

---

## 6. Economy Design

### 6.1 Insight -- Primary Currency

**Inflow sources**:
| Source | Insight per Occurrence | Frequency per Run |
|--------|----------------------|-------------------|
| Standard enemy kill | 1-2 | 25-35 per run |
| Elite enemy kill | 3-4 | 4-6 per run |
| Environmental discovery | 2-3 | 6-10 per run |
| Internal Voice success | 2 | 4-5 per run |
| District clear bonus | 3 | 4-5 per run |

**Outflow sinks**:
| Sink | Insight Cost | Frequency per Run |
|------|-------------|-------------------|
| Tier 1 combat upgrade | 6-8 | 1-2 per run |
| Tier 2 combat upgrade | 10-12 | 0-1 per run |
| Tier 3 combat upgrade | 15 | 0-1 per run |
| Witness interrogation | 5-8 | 2-3 available per run |
| Evidence examination | 3-5 | 3-5 available per run |
| Scene reconstruction | 8-12 | 1 available per run |

**Target economy feel**: The player should feel like they can afford "most of what they want but not all of it" in a successful run, and "barely enough to survive OR barely enough to investigate" in a struggling run. The economy should never feel generous. It should feel like a noir detective's budget: there's never enough, so every expenditure matters.

### 6.2 Evidence Fragments -- Narrative Currency

Evidence fragments are not fungible. Each fragment has:
- A **type** (physical, testimonial, circumstantial, psychological)
- An **archetype tag** (which psyche build can perceive it)
- A **meta-case tag** (which conspiracy layer it connects to)
- A **confidence value** (100% from completed runs, 50% from death-ended runs)

Fragments cannot be spent. They accumulate on the meta-case board. The board auto-connects fragments with matching meta-case tags. The player's only agency over the board is choosing which fragments to pursue during a run -- the board itself is a read-only system. This prevents the player from "solving" the meta-case through board manipulation alone. You must play to investigate.

### 6.3 Psyche Echoes -- Tertiary Currency

Psyche Echoes are rare drops (1-2 per run) that represent moments of intense self-awareness. They are spent between runs in the precinct hub on:
- **Memory Anchors**: Lock a single sub-skill to persist through the next reshuffle (stretch goal: Psyche Blending). Cost: 3 Echoes.
- **Meditation Focus**: Increase the probability of a specific archetype being dominant in the next shuffle. Cost: 2 Echoes. Not a guarantee -- a weight adjustment.
- **Conspiracy Insight**: Reveal one hidden connection on the meta-case board without the required evidence. Cost: 5 Echoes. This is the "brute force" progression option for players who are stuck.

Psyche Echoes prevent late-game frustration by giving players limited agency over the shuffle system and the meta-case board. They are rare enough that they feel meaningful but common enough that a player will accumulate 10-15 by the meta-case midpoint.

---

## 7. Difficulty and Balance Framework

### 7.1 Difficulty Settings

**TRAINEE** (Easy)
- Enemy HP: 70% of baseline
- Enemy damage: 70% of baseline
- Internal Voice window: 2.0 seconds
- Insight drops: +25%
- Death penalty on evidence: 75% value (instead of 50%)
- Design intent: Accessible to narrative-focused players. You can mostly ignore combat optimization and still reach case conclusions.

**DETECTIVE** (Standard)
- All values at baseline
- Internal Voice window: 1.5 seconds
- Design intent: The intended experience. Combat is tense but fair. Insight is scarce but not punishing.

**SPECIAL CRIMES** (Hard)
- Enemy HP: 130% of baseline
- Enemy damage: 130% of baseline
- Internal Voice window: 1.0 second
- Insight drops: -15%
- New enemy behavior patterns: elites gain combo attacks
- Design intent: For players who have mastered combat fluency and want mechanical challenge. The narrative experience is identical.

**MORALIST** (Challenge Mode -- unlocked after first meta-case Layer 3 completion)
- Enemy HP: 150% of baseline
- Enemy damage: 150% of baseline
- Internal Voice window: 0.6 seconds
- Insight drops: -25%
- Psyche shuffle is fully random (no guaranteed dominant -- possible to get a 6/6/6/6 spread)
- No Psyche Echoes drop
- Design intent: The "true" challenge run. For players who want to prove they can handle anything the shuffle deals them.

### 7.2 Archetype Balance Philosophy

The four archetypes are not balanced for equal combat effectiveness. They are balanced for equal game effectiveness -- meaning each archetype has compensating strengths across combat, narrative access, and Insight efficiency.

| Archetype | Combat Difficulty | Narrative Access | Insight Efficiency |
|-----------|------------------|------------------|-------------------|
| Authority | Easy (high HP, high damage) | Moderate (power-narrative only) | Low (brute force, no shortcuts) |
| Empathy | Easy (high evasion, telegraphs) | High (broadest evidence access) | High (charm bypasses some combat) |
| Logic | Moderate (setup-dependent) | Moderate (environmental focus) | Highest (trap efficiency, env kills give bonus Insight) |
| Electrochemistry | Hard (glass cannon, risk-reward) | Low (niche evidence) | Moderate (fast clears, but frequent deaths reset Insight) |

This creates an implicit difficulty curve within each run: an Electrochemistry-dominant run is inherently harder in combat but may access evidence that no other archetype can see, making it invaluable for specific meta-case threads. The balance is holistic, not per-system.

### 7.3 Tuning Levers

The following variables are exposed for tuning during playtesting:

- **Insight drop rates per enemy type** (primary economy lever)
- **Internal Voice trigger frequency** (pacing lever)
- **Internal Voice window duration** (difficulty lever)
- **Psyche point distribution weights** (build diversity lever)
- **Evidence fragment meta-case tag assignment** (progression pacing lever)
- **District enemy count and composition** (run length lever)
- **Psyche Echo drop rate** (long-term progression lever)

Each lever has a documented "break point" -- a value beyond which the game feel degrades. For example, Insight drop rate below 0.5 per enemy makes the economy feel punishing to the point of hopelessness; above 2.0 per enemy makes it feel trivial. The tuning range is documented for QA.

---

## 8. Risk Assessment

### Critical Risks (Could Kill the Game)

**Risk 1: Case Refraction feels random instead of meaningful.**
- Likelihood: High
- Impact: Fatal -- this is the unique selling proposition
- Mitigation: Every evidence node must have a clear psychological justification for why a specific archetype perceives it. "Authority sees bruises because Authority understands violence" is clear. "Logic sees bruises because... reasons" is not. If the mapping between archetype and evidence feels arbitrary, the entire system collapses into randomness. Each evidence node needs a one-sentence design rationale.
- Playtest priority: 1 (first thing tested)

**Risk 2: Insight tension collapses.**
- Likelihood: Medium
- Impact: High -- if players find an optimal Insight path, the strategic heart dies
- Mitigation: Insight sinks must be tuned so that no single spending pattern dominates. If "always combat" or "always narrative" becomes optimal, the economy has failed. Regular balance passes. Potential dynamic pricing (costs increase slightly based on player's historical spending pattern).
- Playtest priority: 2

**Risk 3: Internal Voices feel annoying rather than characterful.**
- Likelihood: Medium-High
- Impact: High -- players will turn them off or resent them
- Mitigation: Internal Voice frequency must be carefully tuned. The current target of 1 per room may be too high. The mechanic should fire at moments of narrative relevance (near evidence, mid-boss, after an elite kill) rather than on a flat timer. The player must feel that the voice has something to say, not that it's just bothering them.
- Playtest priority: 3

### Moderate Risks (Could Hurt the Game)

**Risk 4: Psyche reshuffle feels punishing.**
- Players who just mastered an Authority build and get shuffled to Empathy may feel robbed. Mitigation: The reshuffle cinematic must make the new build feel exciting, not deflating. The Psyche Echo system gives players limited control. The game must communicate "new lens" not "lost progress."

**Risk 5: Meta-case is too slow.**
- If meaningful meta-case connections don't appear until Run 10+, players may churn before experiencing the hook. Mitigation: Layer 1 connections must appear by Run 3-4. The first "wait, this contradicts my last run" moment must happen within the first 2 hours.

**Risk 6: Combat archetypes don't feel different enough.**
- If Authority and Electrochemistry both feel like "melee but slightly different," the psyche system is decorative rather than structural. Mitigation: Each archetype must have at least one combat verb that no other archetype has access to. Movement speed, dodge characteristics, and attack animations must be visually and kinesthetically distinct. This is an animation budget question as much as a design question.

**Risk 7: The 50% evidence penalty on death discourages experimentation.**
- Players may play overly cautiously to avoid death, which kills the roguelite feel. Mitigation: 50% evidence value is still evidence. The game must communicate that dying is progression, just slower progression. Potential tuning: 65% instead of 50% if playtesting shows excessive risk aversion.

### Low Risks (Manageable)

**Risk 8: Players "solve" the meta-case by reading wikis.**
- Inevitable for any mystery game. Mitigation: The meta-case's final choice depends on which evidence YOU specifically gathered across YOUR runs. Wiki knowledge tells you the conspiracy; it doesn't give you the evidence to make the accusation. The ending is experiential, not informational.

**Risk 9: Archetype balance is off at launch.**
- Expected. Mitigation: Tuning levers are exposed and documented. Post-launch balance passes are planned. The game should launch with archetype balance that is "interesting" (each feels distinct) even if not perfectly "fair."

---

## 9. Open Playtesting Questions

These are questions that cannot be answered by design documents. They require hands-on-controller observation.

### Combat Feel

1. **What's the minimum number of unique attack animations per archetype before they feel distinct?** Current estimate: 5 per archetype (light, heavy, aerial, dodge-attack, signature). Is 5 enough, or does each need 8+?

2. **Does the Logic archetype's trap-based combat feel active enough?** Setting up traps and exploiting the environment is strategically rich but may feel passive compared to Authority's brawling or Electrochemistry's frenzy. Does the Logic player feel like they're playing the same game?

3. **What's the sweet spot for Electrochemistry's risk-reward curve?** If the combo counter reset on damage feels too punishing, players will abandon the archetype. If it's too forgiving, there's no risk. Where's the line?

### Internal Voices

4. **What's the ideal frequency for Internal Voice interruptions?** 1 per room? 1 per 2 rooms? Only during bosses? The design says 1 per room, but playtest data may say otherwise.

5. **Should Internal Voice checks be input-based (press the right button) or timing-based (press anything in the window)?** Input-based adds cognitive load but feels more like a skill check. Timing-based is simpler but may feel like a QTE.

6. **Do players read the narrative text in Internal Voice pop-ups, or do they just react to the mechanic?** If they're not reading the text, the Disco Elysium half of the mechanic is failing.

### Insight Economy

7. **At what Insight drop rate do players stop feeling the tension between combat and narrative spending?** This is the most important tuning number in the game.

8. **Do players naturally discover that narrative unlocks have indirect combat value, or does the game need to teach this?** If players treat the two channels as strictly separate, they're missing a layer of depth.

9. **Is the Psyche Echo system necessary, or does it reduce the beauty of the random shuffle?** Giving players control over the shuffle may undermine the game's thesis about identity being involuntary.

### Meta-Case Pacing

10. **How many runs before the first "aha" connection on the meta-case board?** Target: 3-4 runs. If it takes longer, we lose players. If it happens sooner, it feels cheap.

11. **Does the meta-case board's auto-organization feel like revelation or loss of agency?** Players who want to arrange the board themselves will be frustrated. Is the read-only design defensible?

12. **When does the meta-case stop feeling like discovery and start feeling like a checklist?** At some point, players will know which evidence they need and runs become targeted farming. Is this acceptable, or does the game need mechanics to prevent it?

### Run Structure

13. **Is 20-40 minutes the right run length?** Shorter runs mean more shuffles and faster meta-case progression but less time to develop a relationship with each psyche build. Longer runs risk commitment fatigue.

14. **Should there be a "quit and resume" system, or must runs be completed in one sitting?** The roguelite tradition says one sitting. The target audience includes 30-somethings with limited play windows.

15. **Does the district branching path choice feel meaningful, or do players just pick the easier route?** If players always choose the path of least resistance, the case evidence attached to harder routes never gets accessed. Potential solution: make harder routes' evidence more narratively valuable without making them mechanically mandatory.

---

## 10. Design Pillars -- Summary

These are the non-negotiable truths of Revachol Nights' design. Every mechanic, system, and content decision must serve at least one of these pillars. If a proposed feature serves none, it is cut.

1. **The psyche IS the build.** Your personality determines your combat, your evidence access, and your truth. This is not metaphorical. It is mechanical.

2. **One resource, two hungers.** Insight is always scarce, always contested. The moment the player stops agonizing over Insight allocation is the moment we've failed.

3. **Death is a lens change, not a failure state.** Every death produces a new perspective. The meta-case needs all perspectives. Dying is mandatory for progress -- the game just doesn't tell you that immediately.

4. **The mystery is real and refracted.** Every case conclusion is authored, intentional, and psychologically coherent. No random generation of case content. No procedural narrative. Every truth is handcrafted.

5. **The 30-second loop carries everything.** If the combat doesn't feel good with the archetype you're dealt, nothing else matters. Frame-perfect responsiveness is non-negotiable. We never figure out the fun later -- the fun is in the first 30 seconds or it's nowhere.

---

*This document was written by REED, Game Designer. The next steps are: (1) paper prototype the Insight economy with two archetype builds and one case node, (2) greybox prototype the 30-second loop for Authority and Empathy archetypes, (3) playtest Internal Voice frequency and input method. The design is not done. It is never done. But the loop is defined, the systems interact, and the depth is real. Now we find out if it's fun.*
