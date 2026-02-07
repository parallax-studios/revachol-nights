# REVACHOL NIGHTS — Level Design Document

**Document Owner**: GRID (Level Designer)
**Version**: 1.0
**Status**: Foundation Complete — Ready for Blockout
**Date**: 2026-02-07

---

## I. CORE SPATIAL PHILOSOPHY

### Design Thesis

**A level is not geometry. A level is a conversation between the player's eye, the player's body, and the player's understanding.**

Revachol Nights is a game where your psyche determines what you see. That means level design cannot be static architecture. It must be *reactive architecture* — spaces that reveal different information, different paths, different meanings depending on which version of you walks through them.

Where does the player LOOK? That depends on who they are this run.

Every district is designed with four simultaneous reads:
- **Authority Read**: Power structures, territorial markers, chokepoints, defensible positions
- **Empathy Read**: Traces of habitation, emotional residue, signs of relationships, safe spaces
- **Logic Read**: Structural integrity, environmental hazards, system vulnerabilities, optimal paths
- **Electrochemistry Read**: Sensory overload zones, substance traces, high-stimulus routes, visceral shortcuts

The same room. Four different levels. That's not a metaphor. That's the design mandate.

### Movement Philosophy

The detective moves differently depending on psyche build. Level design must support this:

- **Authority**: Forward momentum, space control, room-to-room dominance. Levels teach: "You walk through obstacles, not around them."
- **Empathy**: Evasion-first, circulation priority, escape route clarity. Levels teach: "Every space has a way out. Find it before you need it."
- **Logic**: Setup zones, trap placement opportunities, environmental interaction nodes. Levels teach: "The room is a tool. Use it before enemies do."
- **Electrochemistry**: Speed lanes, risky shortcuts, high-risk/high-reward paths. Levels teach: "The fastest route is through the danger."

If a room layout forces an Empathy player to fight like Authority or a Logic player to move like Electrochemistry, the level has failed. Combat is the player's responsibility. Movement opportunity is ours.

### The Golden Rules

1. **Every room teaches before it tests.** New enemy type? First encounter is scripted easy. New hazard? First exposure has generous recovery. Never surprise-kill the player with a mechanic they haven't seen.

2. **Sight lines are breadcrumbs.** Where the camera can see, the player will go. Where light falls, attention follows. Never rely on UI waypoints. The level IS the waypoint.

3. **Pacing is spatial, not temporal.** Tension is not a timer. Tension is a narrow corridor. Release is not a cutscene. Release is an open room with light and height.

4. **Negative space teaches as much as positive space.** An empty room after a combat gauntlet says "breathe." A locked door says "come back later." A dark hallway says "something is waiting." The absence is the message.

5. **The level remembers, even when the player doesn't.** Between runs, psyche shuffles. District layouts persist. A player on run five should recognize Martinaise's waterfront geometry even if they're seeing it through new eyes. Spatial memory is the only memory that survives the reshuffle.

---

## II. DISTRICT DESIGN — THE FIVE ZONES

### DISTRICT 1: JAMROCK QUARTER (Hub / Tutorial)

**Purpose**: Orientation, safety, meta-progression home base. The place you leave from and return to.

**Emotional Beat**: Institutional melancholy. The feeling of a space that was designed for function and has achieved it at the cost of everything else.

**Spatial Identity**: Brutalist interior architecture. Long, straight corridors with fluorescent lighting. Right angles. No organic curves. Everything is beige, grey, or institutional green. The space resists beauty the way a system resists deviation.

#### Key Spaces

**THE PRECINCT OFFICE (Safe Room)**

```
                NORTH WALL: Case Board
                     |
    [File      [Detective's   [Coffee     [Exit to
   Cabinets]     Desk]        Station]    Streets]
        |          |             |            |
        +----------+-------------+------------+
                         |
                  SOUTH WALL: Windows
              (rain-streaked, neon beyond)
```

**Where does the player LOOK?**
- First: The case board (meta-progression visualization, always visible, always pulling focus)
- Second: The detective's desk (run initiation point, psyche reveal cinematic triggers here)
- Third: The exit (the promise of the field, the districts, the case)

**Pacing**: Zero combat. This is sacred decompression space. The player's heartrate drops here. The music shifts to ambient. This room teaches: "You are safe. For now."

**Breadcrumbing**: Light sources guide in sequence: dim fluorescents over the file cabinets, brighter desk lamp on the detective's workspace, harsh backlight on the case board (making it visible from anywhere in the room), neon glow from the street beyond the exit. The player's eye travels the intended path without instruction.

**Psyche-Specific Reads**:
- Authority: Sees the desk as a command post. Notes the sightline to the door (who enters, who leaves).
- Empathy: Sees Jean's coat draped over a chair, a cold coffee cup on the file cabinet. Someone was here recently. Someone is tired.
- Logic: Sees the case board's organization pattern. Red thread connections. Contradictions flagged. A system under strain.
- Electrochemistry: Hears the fluorescent hum. Smells burnt coffee and old cigarettes. Feels the static charge of too many hours under artificial light.

**Metrics to Track**:
- Time spent at case board per run (should increase as meta-case complexity grows)
- Player path on first entry (do they go to board, desk, or exit first? Reveals player priority)
- Frequency of voluntary returns mid-run (if players return to hub before death, something is wrong with district pacing)

---

**THE PRECINCT HALLWAY (Tutorial Combat Zone)**

```
    [Precinct Office] ----  LONG CORRIDOR ---- [Evidence Lock-Up]
                               |    |    |
                            [Door] [Door] [Door]
                          (locked)(locked) [Interrogation Room]
                                              (accessible)
```

**Length**: 40 meters. Long enough that running the full distance feels like a commitment.

**Width**: 4 meters. Wide enough for Authority's swings. Narrow enough that Empathy must be intentional with dodge direction.

**Purpose**: Teach the 30-second loop in a controlled environment. First Internal Voice. First combat encounter (manifestation of the detective's own psyche — a sparring partner, not a threat).

**Enemy Placement**: Single enemy, mid-hallway. Scripted to be passive until player approaches within 10 meters. Telegraph is generous (2.0 seconds). This encounter exists to teach "you can fight" not "you might die."

**Sight Line**: The full hallway is visible from the precinct office door. The player sees the enemy before engaging. No ambush. The lesson is mechanics, not threat assessment.

**Pacing**: Slow build. Walking the hallway is a 6-second commitment. First combat is 15-20 seconds. Total time in space: 30-40 seconds. This is the metronome. Every future room is measured against this baseline.

**Breadcrumbing**: The Interrogation Room door is lit (practical light source visible through door window). The Evidence Lock-Up is dark. The path is obvious.

**Tutorial Density**: The hallway teaches:
1. Movement (WASD / stick input)
2. Combat initiation (approach enemy)
3. Basic attack (primary combat verb for current psyche)
4. Dodge (enemy telegraph is generous, punish is light)
5. Internal Voice (first pop-up during combat, window is 2.0 seconds)

After this hallway, the player knows the loop. We never tutorial again. We test, we combine, we escalate. Never re-teach.

**Metrics to Track**:
- Death rate in tutorial hallway (should be <1%, if higher, enemy is overtuned)
- Internal Voice success rate (target: 40-60% on first encounter, teaches that failure is acceptable)
- Time to complete hallway (baseline for pacing comparison in later districts)

---

**THE INTERROGATION ROOM (First Debrief Space)**

```
         MIRROR (one-way glass)
               |
    [Table] [Chair] [Chair]
       |       |       |
    [Evidence    Detective    Witness]
     Folder]   (player)      (NPC)
```

**Size**: 3m x 4m. Claustrophobic by design. Interrogations are pressure chambers.

**Lighting**: Single overhead light, harsh and unflattering. Shadows pool in corners. The mirror reflects the player's character (psyche-specific posture: Authority leans back, Empathy leans forward, Logic takes notes, Electrochemistry fidgets).

**Purpose**: First Insight spend decision. The witness (a low-level informant, non-hostile) has information. Unlocking it costs 3 Insight. The player just earned ~5 Insight from the hallway combat. The choice is real but not punishing.

**Narrative Function**: Witness provides first evidence fragment about Lena Hargate. What they reveal depends on psyche build:
- Authority: "She was asking questions about the Coalition. Dangerous questions."
- Empathy: "She seemed scared. Like she knew something was coming."
- Logic: "She had documents. Technical stuff. I didn't understand it."
- Electrochemistry: "She wasn't sleeping. I could tell. You can always tell."

**Pacing**: Full stop. Dialogue pace. The player's heartrate drops further. Combat -> Debrief -> Spend -> Decide. This is the 5-minute loop in miniature.

**Breadcrumbing**: After the interrogation, the exit door unlocks (audible click, light above door shifts from red to green). The path forward is gated by engagement with narrative. You cannot skip the story.

**Metrics to Track**:
- Percentage of players who spend Insight on first interrogation (target: 60-80%, if lower, players don't understand value)
- Dialogue skip rate (if players are skipping, narrative density is wrong)
- Time spent in room (baseline for future debrief pacing)

---

### DISTRICT 2: MARTINAISE (The Waterfront)

**Purpose**: Introduce environmental storytelling, faction dynamics (Hardy Boys), and the Whirling-in-Rags murder scene. The case becomes real here.

**Emotional Beat**: Melancholy with an undercurrent of threat. The docks remember the commune. The people remember defeat. The architecture is crumbling grandeur.

**Spatial Identity**: Rust, salt, fog. Shipping containers as architecture. Cranes as landmarks. Water as negative space — you see it, you move toward it, but you never reach it. The sea is always one district away.

**Color Palette**: Rust orange, tarnished brass, grey concrete, oily water reflections. Neon signs bleed through fog (reds and ambers, no blues — this is a warm-toned decay).

**Dominant Verticality**: Low. Most spaces are 1-2 stories. The cranes reach higher, but they're background. Martinaise teaches: "This is a place that once reached upward and gave up."

#### Flow Diagram (Top-Down)

```
    [Jamrock Exit]
         |
    DOCKSIDE APPROACH
    (open, 3 containers
     as cover, 2 enemies,
     distant crane visible)
         |
    +----+----+
    |         |
CONTAINER  UNION
  MAZE     HALL
(4 rooms,  (safe room,
 enemies,  Evrart,
 tight)    Insight spend)
    |         |
    +----+----+
         |
    WHIRLING-IN-RAGS
    (murder scene, 6 rooms,
     boss: Memory of Violence,
     evidence-heavy)
         |
   [Exit to Capeside
    or Valley — player
    choice branches here]
```

**Total Room Count**: 12 combat rooms, 2 safe rooms, 1 boss room.
**Estimated Clear Time**: 8-12 minutes depending on build and skill.
**Insight Budget**: 10-14 drops across district.

---

#### DOCKSIDE APPROACH (Entry Room)

**Purpose**: Establish Martinaise's aesthetic and threat level. First multi-enemy encounter. Teach cover mechanics for Logic builds.

**Layout**:

```
         FOG (visual boundary, not physical)
              |
   [Crane     |        Crane
   Silhouette]|     Silhouette]
        ===========WATER==========
              |
    DOCK PLATFORM (20m x 15m)
              |
    Container  Container  Container
    (solid)    (open, can (solid)
                enter)
         E1         E2
       (melee)  (ranged)
              |
         [Player Entry]
```

**Where does the player LOOK?**
- First: The cranes (landmark, orientation, tells you "this is the docks")
- Second: Movement (enemies patrol, telegraphing threat before engagement)
- Third: The open container (visual interest, promise of exploration, actual cover if player thinks spatially)

**Enemy Design**:
- E1 (Dockworker Enforcer): Slow, heavy. Authority-type enemy. Teaches "some enemies fight like you might fight."
- E2 (Hardy Boys Lookout): Ranged, evasive. Stays at distance. Teaches "positioning matters."

**Pacing**: Moderate tension. Two enemies is escalation from tutorial's one, but the space is generous. This is not a trap. This is a test of spatial thinking.

**Psyche-Specific Approaches**:
- Authority: Walk forward, engage E1 in melee, tank E2's ranged attacks, clear through aggression.
- Empathy: Use container cover, bait E1 into overextending, dodge E2's shots using i-frames, pick off one at a time.
- Logic: Enter the open container, use it as chokepoint, exploit sightline advantage, force enemies to approach into trap.
- Electrochemistry: Rush E2 first (high threat, low HP), build combo, use speed to avoid E1's slow swings.

All four approaches work. The level supports all four. That's the design test.

**Breadcrumbing**:
- The open container glows faintly (interior has a work light still on).
- The path forward (to Container Maze or Union Hall branch) is marked by neon sign visible through fog: "HARDY BOYS LOCAL 428."
- Fog limits visual distance to 30 meters, creating natural boundaries without walls.

**Metrics to Track**:
- Enemy kill order (do players prioritize ranged or melee? Reveals threat assessment)
- Cover usage rate (if Logic players aren't using containers, cover affordance is unclear)
- Death rate (target: <10% on Standard difficulty)

---

#### CONTAINER MAZE (Combat Gauntlet)

**Purpose**: Tight, oppressive combat. Teach that not all spaces are generous. Reward spatial memory (layout persists across runs).

**Layout**:

```
    [Entry from Dockside]
            |
         ROOM 1
    Container Container
         L-shaped path
         Enemy x2
            |
         ROOM 2
    Container Container Container
      Narrow chokepoint
         Enemy x1 (elite)
            |
         ROOM 3
    Container (open, contains
       Insight pickup +3)
    Container Container
         Enemy x2
            |
         ROOM 4
    Container Container
      Opens to Union Hall
         Enemy x1 (fast)
            |
    [Exit to Union Hall]
```

**Total Path Length**: 60 meters, not counting combat backtracking.
**Width Variance**: 2-5 meters (tight to moderate).
**Visibility**: Each room visible only when entered (containers block sightlines).

**Pacing**: Rising tension. Room 1 is manageable. Room 2 introduces elite (higher HP, unique attack pattern). Room 3 offers reward but demands risk (Insight pickup guarded by two enemies). Room 4 is final push before safe room.

**Tension Curve**:

```
Tension
  ^
  |                    ROOM 3
  |                   (risk/reward)
  |        ROOM 2        |
  |       (elite)        |      ROOM 4
  |         |            |      (exhaust)
  | ROOM 1  |            |        |
  | (intro) |            |        |
  +----+----+------------+--------+----> Time
       2min     4min      6min    8min
```

**Why this structure works**: Peaks and valleys. Room 1 teaches the space. Room 2 tests. Room 3 offers choice (engage for Insight or skip to conserve HP). Room 4 is cleanup before rest. The player never plateaus.

**Psyche-Specific Challenges**:
- Authority: Tight spaces limit heavy swings. Must learn to commit to attacks despite reduced room to maneuver.
- Empathy: Generous dodge but limited escape routes. Must use i-frames precisely, not just reactively.
- Logic: Trap placement opportunities are limited by narrow paths. Must adapt setup-heavy playstyle to on-the-move tactics.
- Electrochemistry: Ideal space for speed builds. Narrow corridors = guaranteed enemy contact for combo building. High risk, high reward.

**Breadcrumbing**:
- Room 2's elite enemy is audible before visible (heavy footsteps, distinct from standard enemies).
- Room 3's Insight pickup glows (warm orange light inside open container, visible from room entry).
- Room 4's exit shows distant interior light from Union Hall (safety is visible, motivation to push through).

**Environmental Storytelling**:
- Containers have faded communist murals (commune-era art, barely visible under rust).
- Scattered dockworker equipment (hard hats, clipboards, a thermos still sitting on a container edge).
- Authority sees territorial markers (Hardy Boys tags, boundary lines).
- Empathy sees habitation signs (sleeping bag in one container, old photographs taped to walls).
- Logic sees structural failure (containers stacked unsafely, rust compromising integrity).
- Electrochemistry sees substance traces (discarded bottles, pill blister packs, evidence of self-medication).

**Metrics to Track**:
- Room 3 engagement rate (do players take the risk for Insight?)
- Death location heatmap (which room kills most? Should be Room 2 or 3)
- Clear time per psyche build (are tight spaces unfairly punishing to specific builds?)

---

#### UNION HALL (Safe Room / Evrart Encounter)

**Purpose**: Debrief, Insight allocation, faction introduction, first major Insight tension moment.

**Layout**:

```
         STAGE (union podium, unused)
              |
     [Long Table] (Evrart sits at head)
              |
    Chair  Chair  Chair  Chair
    (empty across from Evrart)
              |
         DETECTIVE
         (player)
              |
         [Entry Door]

    WEST WALL: Union flag, faded
    EAST WALL: Windows facing water (fog obscures view)
```

**Size**: 10m x 12m. Large enough to feel important. Small enough that Evrart dominates.

**Lighting**: Warm overhead (bare bulbs, industrial). Evrart is backlit by window light. His face is partially shadowed. Intentional — he controls what you see.

**Pacing**: Full stop. This is the district's first debrief. Player has cleared 5 rooms, spent ~6-8 minutes in combat. Heartrate is elevated. This room forces decompression.

**Narrative Beat**: Evrart has information about Lena Hargate. She was seen in Martinaise days before the murder. Evrart's testimony is valuable. It is also expensive.

**Insight Spend Structure**:

| Option | Insight Cost | What You Learn | Psyche Gate |
|--------|-------------|----------------|-------------|
| "What did Lena want here?" | 5 | Lena was asking about Pale-thin spots in the docks | None |
| "Who did she meet?" | 6 | She met with union members (names provided) | Authority 3+ OR Logic 3+ |
| "Why do you care about this case?" | 4 | Evrart reveals personal connection (Edgar's death site is near Whirling-in-Rags) | Empathy 3+ |
| "What are you not telling me?" | 8 | Evrart admits Hardy Boys have Pale-adjacent smuggling operation | Logic 5+ OR Authority 6+ (intimidate) |

**The Tension**: Player has earned ~10-14 Insight by this point. Evrart's full testimony costs 15-23 Insight (if player unlocks all available options). They cannot afford everything. They also have not yet allocated Insight to combat upgrades. This is the first real economic pressure.

**Design Intent**: Teach that narrative unlocks are expensive and valuable. Teach that some information is gated behind psyche builds (not all paths are always available). Teach that Evrart is not an enemy but not an ally — he is a force with his own gravity.

**Psyche-Specific Dialogue**:
- Authority: Can attempt to intimidate Evrart. He laughs. "You think you're the first cop who tried that? Sit down, friend. We'll talk like adults."
- Empathy: Can read Evrart's grief about Edgar. Unlocks additional dialogue branch that costs no Insight but yields emotional context, not evidence.
- Logic: Can point out contradictions in Evrart's statements. He respects this. Slight Insight discount (5 becomes 4, etc.).
- Electrochemistry: Can recognize signs of Evrart's own substance dependencies. Unlocks dialogue about the pharmaceutical supplements (ties into Valley of the Dogs meta-thread).

**Breadcrumbing**: After Evrart dialogue, two paths become visible:
1. West door: Leads to Whirling-in-Rags (murder scene, high difficulty, high evidence value).
2. East door: Leads to back alley route (skips Whirling, lower difficulty, lower evidence, faster district exit).

Both doors are lit. Neither is "correct." The player chooses based on current HP, Insight reserves, and investigation priority.

**Metrics to Track**:
- Insight spend distribution (which questions do players prioritize?)
- Path choice after Evrart (Whirling vs. skip route — reveals player risk tolerance)
- Dialogue skip rate per psyche build (does Authority skip more? Does Empathy read everything?)

---

#### WHIRLING-IN-RAGS (Murder Scene / Boss Arena)

**Purpose**: The case becomes real. Highest evidence density in Martinaise. Boss encounter that is mechanically challenging AND narratively loaded.

**Layout**:

```
            ROOF ACCESS
           (locked until
            Layer 3 meta)
                |
         THIRD FLOOR
         Room 208 (murder scene)
         Lena's belongings
         Evidence fragments x4
                |
         SECOND FLOOR
    Hallway: 4 rooms (enemies x2 each)
    L-shaped, tight corners
                |
         FIRST FLOOR
    Lobby (boss arena)
    Open space, 15m x 15m
         |          |
    [Front Door]  [Back Alley]
    (from Union)  (skip route)
```

**Total Rooms**: 6 (lobby, 4 hallway rooms, Room 208).
**Enemy Count**: 8 standard, 1 boss.
**Evidence Fragments**: 6 total (2 in hallway rooms, 4 in Room 208).

**Vertical Progression**: Ground to third floor. Climbing creates natural pacing (combat -> stairs -> combat -> stairs -> evidence). The player earns Room 208.

**Pacing Structure**:

```
Tension
  ^
  |                          ROOM 208
  |                        (revelation,
  |                         evidence)
  |                            |
  |              2ND FLOOR     |
  |              (combat       |
  |               gauntlet)    |
  |                 |          |
  |    BOSS         |          |
  |   (lobby)       |          |
  +-----+-----------+----------+----> Time
      2min        6min       10min
```

Boss at the START of the dungeon, not the end. Why? Because the boss is not the reward. The evidence is. The player fights to earn the right to investigate. This inverts standard level design and makes narrative the mechanical goal.

---

**FIRST FLOOR: LOBBY (Boss Arena)**

**Size**: 15m x 15m, open plan.
**Furniture**: Reception desk (can be used as cover by Logic), scattered chairs (can be thrown/destroyed by Authority), large mirror on west wall (cracks during boss fight, reflects psyche-specific imagery).

**Boss: MEMORY OF VIOLENCE**

A psychic manifestation of the murder itself. Not a literal ghost. A trauma echo. The Pale-thin spot in the Whirling has made the violence linger.

**Boss Mechanics** (vary by player psyche):

- **vs. Authority**: Boss is a large, armored figure. Heavy attacks, territorial. Fight is about space control. Teach: "Dominance is not invincibility."
- **vs. Empathy**: Boss is fast, erratic, desperate. Attacks have long telegraphs but unusual patterns. Fight is about reading and adapting. Teach: "Empathy feels pain, including the enemy's."
- **vs. Logic**: Boss has predictable phase transitions and environmental vulnerabilities (can be lured into furniture traps). Fight is about setup and execution. Teach: "Knowledge is preparation."
- **vs. Electrochemistry**: Boss is aggressive but fragile. High damage, low HP. Fight is a DPS race. Teach: "Speed is survival."

**Narrative Integration**: Mid-fight, an Internal Voice fires (unavoidable, scripted). The voice whispers a fragment of Lena's last words. What the player hears depends on psyche:
- Authority: "You can't stop this."
- Empathy: "I'm sorry. I tried."
- Logic: "The numbers were right. Why didn't they listen?"
- Electrochemistry: "I can't feel my hands."

The boss fight is not just a combat encounter. It is the first direct contact with Lena Hargate's death. The player is not fighting an enemy. They are fighting the memory of what happened here.

**Victory Condition**: Boss HP to zero. On defeat, boss dissolves into light (Pale visual effect: grey-white, entropic). The mirror on the west wall shatters. A key drops (Room 208 access).

**Pacing**: 2-3 minute fight for skilled players, 4-5 for new players. Not a long fight. A sharp one.

**Breadcrumbing**: After boss defeat:
- Stairs to second floor illuminate (practical lights on stairwell flicker on).
- Faint sound from above (wind through broken window in Room 208, audible now that combat noise has stopped).

**Metrics to Track**:
- Boss clear rate per psyche build (are any builds significantly harder?)
- Death count on boss (target: 20-30% of players die at least once)
- Internal Voice success rate during boss (high-pressure timing window — target: 30-40% success)

---

**SECOND FLOOR: HALLWAY GAUNTLET**

```
    [Stairs Up to Room 208]
            |
         ROOM 4
    (2 enemies, Evidence +1)
            |
    L-TURN (90 degrees)
            |
         ROOM 3
    (2 enemies, tight space)
            |
         ROOM 2
    (2 enemies, Evidence +1)
            |
    L-TURN (90 degrees)
            |
         ROOM 1
    (2 enemies, closest to stairs)
            |
    [Stairs from Lobby]
```

**Design Intent**: Sustained pressure. Four rooms, eight enemies, two evidence pickups. The player has just spent resources on the boss. Do they push forward or retreat to Union Hall to spend Insight on healing?

The L-shaped hallway prevents the player from seeing the full gauntlet. Each corner is a small relief (you cleared a section) and a small dread (there's more).

**Width**: 3 meters. Tighter than Dockside, more generous than Container Maze. Goldilocks width — everyone can function, no one is optimized.

**Enemy Composition**: Standard Whirling Residents (psyche-damaged civilians, hostile but not trained fighters). Lower HP than dockworkers, more erratic movement patterns. These enemies teach: "The Pale damages minds. Even the victims are dangerous."

**Evidence Fragments** (in Rooms 2 and 4):
- Room 2: Lena's research notes (coffee-stained, tucked under a radiator). Fragment reveals: "Pale expansion is not natural."
- Room 4: Witness statement (recorded on a handheld recorder, left in a guest room). Fragment reveals: "Someone visited Lena the night she died."

Both fragments are optional (player can skip rooms via risky jumps between hallway sections if they find the geometry). Evidence requires engagement. Always.

**Pacing**: Linear escalation. Room 1 is warmup. Room 2 adds evidence tension (fight while protecting pickups). Room 3 is tightest space, highest pressure. Room 4 is final push before reward (Room 208).

**Breadcrumbing**:
- Room 208's door is visible from the top of the second-floor stairs. It is lit (warm light leaking under door).
- The player sees the goal before the final combat section. This is motivation to push through.

**Metrics to Track**:
- Evidence pickup rate per room (do players skip evidence to conserve HP?)
- Damage taken per room (which room is hardest?)
- Retreat rate (do players leave Whirling mid-gauntlet to heal? If >20%, pacing is too punishing)

---

**THIRD FLOOR: ROOM 208 (The Murder Scene)**

**Purpose**: Payoff. The player has fought through 9 combat encounters (boss + 8 standard). They have earned this.

**Layout**:

```
    WINDOW (broken, fog visible outside)
        |
    BED (unmade, suitcase open on it)
        |        |        |
    EVIDENCE  EVIDENCE  EVIDENCE
      #1        #2        #3
   (on desk) (in bath) (under bed)
        |
    DOOR (entry, now behind player)
```

**Size**: 4m x 5m. Small. Intimate. The space where someone died.

**Lighting**: Cold. Blue-grey dawn light through broken window. No neon here. The city's color stops at this threshold.

**Pacing**: Full stop. Zero combat. This is a reward room, but the reward is not loot. It is understanding.

**Evidence Fragments** (4 total, highest density in the game):

1. **Lena's Suitcase** (on bed): Contains personal effects. Psyche-gated reveals:
   - Authority 3+: Finds encrypted Coalition documents hidden in lining.
   - Empathy 3+: Finds photographs of Lena with family (emotional context, no hard evidence).
   - Logic 3+: Finds Pale measurement equipment (scientific instruments, high-value evidence).
   - Electrochemistry 3+: Finds pharmaceutical supplements (links to Valley of the Dogs).

2. **The Desk** (Lena's notes): Handwritten research. Fragment reveals: "The Pale is being fed. Source is in Revachol." Available to all builds.

3. **The Bathroom** (trace evidence): Chemical residue in sink. Fragment reveals: "Lena was drugged before death." Requires Logic 2+ OR Empathy 4+ (Logic sees chemical traces, Empathy notices behavioral evidence in how the scene is arranged).

4. **Under the Bed** (hidden): Lena's personal journal. Fragment reveals: "She was working with someone. A collaborator. Initial: A." (This is Annette. Meta-case thread to La Delta.)

**Narrative Beat**: After collecting evidence, an Internal Voice fires (calm, not combat-pressure). The detective's dominant psyche offers an interpretation:
- Authority: "She was a threat. Someone eliminated a threat."
- Empathy: "She was alone here. She died afraid and alone."
- Logic: "Premeditation. Evidence suggests planning, not impulse."
- Electrochemistry: "She didn't fight back. The drugs were already working."

The player leaves Room 208 with 4-6 evidence fragments (depending on psyche build and thoroughness). This is the richest single space in Martinaise. The case is real now.

**Breadcrumbing**:
- Window can be interacted with. Looking out shows the cranes of Martinaise in fog. A moment of environmental beauty in a crime scene. Breathing room.
- Exit door glows faintly (the path forward, to Capeside or Valley choice).

**Metrics to Track**:
- Evidence collection rate (do players find all fragments? Are any too hidden?)
- Time spent in room (should be 2-3 minutes; if less, players are rushing; if more, navigation is unclear)
- Psyche-gated evidence access (are players frustrated by gates or intrigued by what they're missing?)

---

### DISTRICT 3: CAPESIDE PROMENADE (Cultural Decay)

**Purpose**: Tonal shift from Martinaise's melancholy to Capeside's architectural tragedy. Introduce verticality, parkour-adjacent movement, and ultraliberal faction enemies.

**Emotional Beat**: Lost beauty. The feeling of walking through a museum where every exhibit has been sold off and replaced with a gift shop.

**Spatial Identity**: Art-nouveau facades converted to commercial use. Grand theaters now warehouses. Gallery spaces now pawnshops. The bones are beautiful. The skin is cheap.

**Color Palette**: Faded gold, tarnished brass, dirty glass, neon pink and cyan (garish against the old architecture). The new lights insult the old walls.

**Dominant Verticality**: High. This is the first district with significant vertical gameplay. 2-4 story buildings, accessible rooftops, parkour routes for Empathy/Electrochemistry builds.

#### Flow Diagram (Top-Down)

```
    [Entry from Martinaise or Jamrock]
            |
       THE PROMENADE STREET
       (open, 3 paths visible)
            |
      +-----+-----+
      |     |     |
   GALLERY THEATER CONCERT
    PAWN   WAREHOUSE HALL
    (tight, (vertical, (boss,
   enemies, platforming, evidence,
   Insight) enemies) debrief)
      |     |     |
      +-----+-----+
            |
      ROOFTOP ROUTE
      (optional, high-risk,
       high-reward shortcut)
            |
    [Exit to Valley or back to Jamrock]
```

**Total Room Count**: 10 combat rooms, 2 safe rooms, 1 boss room, 1 optional secret route.
**Estimated Clear Time**: 10-14 minutes.
**Insight Budget**: 12-16 drops.

---

#### THE PROMENADE STREET (Entry Room)

**Purpose**: Establish Capeside's aesthetic. Offer player choice (three paths, all converge). Teach that Revachol has layers.

**Layout**:

```
         ART-NOUVEAU ARCH (landmark)
                  |
    [Pawnshop]  STREET  [Theater]   [Concert Hall]
    (ground level, wide, 40m long)
         |         |         |
       Path A    Path B    Path C
```

**Size**: 40m x 12m. The most open space since Dockside Approach. After Whirling's tight corridors, this is relief.

**Enemy Count**: 4 (corporate security, patrolling). Avoidable if player uses stealth/evasion. Engageable if player wants Insight.

**Lighting**: Neon signs (bright, modern, clashing with architecture). Streetlights (old, ornate, many are broken). The light sources tell the district's story without words.

**Where does the player LOOK?**
- First: The arch (landmark, beautiful, frames the view).
- Second: The three visible paths (choice, agency, route planning).
- Third: Enemy patrols (threat assessment, stealth possibility).

**Psyche-Specific Reads**:
- Authority: Sees patrol patterns, territorial control. "Corporate security. They're organized. That means they're dangerous."
- Empathy: Sees the contrast between old beauty and new function. "This place used to mean something. Now it's just property."
- Logic: Sees structural details. "The arch is load-bearing. Original construction, pre-Revolution. Everything else is retrofit."
- Electrochemistry: Sees neon, hears distant music (from Concert Hall), feels the city's pulse. "This is where the night lives. Or lived. Or pretends to."

**Breadcrumbing**:
- Gallery Pawn: Ground level, door is open, interior visible (tight space, high enemy density, evidence visible inside).
- Theater Warehouse: Second floor entrance accessed via external stairs (vertical path, platforming required).
- Concert Hall: Straight ahead, main doors (grandest entrance, highest difficulty, boss inside).

All three paths converge after their respective sections. Player cannot get lost. Player CAN choose difficulty and playstyle.

**Metrics to Track**:
- Path choice distribution (which path do players prefer? Reveals risk tolerance and spatial confidence)
- Enemy engagement rate (do players fight or evade?)
- Time spent observing before engaging (patient players scout; aggressive players charge)

---

#### GALLERY PAWN (Path A: Tight Combat)

**Purpose**: High-density combat in confined space. Rewards Authority/Electrochemistry (builds that thrive in close quarters). Tests Empathy/Logic (builds that prefer space).

**Layout**:

```
    [Entry from Street]
         |
      FRONT ROOM
    (3 enemies, shelves as
     obstacles, tight)
         |
      BACK ROOM
    (2 enemies, 1 elite,
     evidence fragment x2)
         |
    [Exit to Convergence Point]
```

**Room Size**: 6m x 8m (front), 5m x 6m (back). Smallest combat spaces since Container Maze.

**Obstacles**: Shelves full of pawned goods. Can be destroyed (Authority), used as cover (Logic), or navigated around (Empathy/Electrochemistry).

**Enemy Type**: Corporate Security (mid-tier HP, defensive stance, prefer formation fighting).

**Pacing**: Sharp, focused. 5 enemies across 2 rooms. High density, short duration. For players who want intense combat and quick Insight.

**Evidence Fragments**:
- Fragment 1: Receipt from Wild Pines Group (buying Capeside property). Links to corporate conspiracy thread.
- Fragment 2: Witness statement (pawnshop owner saw Lena selling research equipment). "She needed money. She was desperate."

**Psyche-Specific Challenges**:
- Authority: Ideal space. Heavy attacks destroy shelves, creating more room to maneuver.
- Empathy: Tight dodge windows. Must use i-frames precisely. High skill ceiling.
- Logic: Can use shelves as chokepoints but limited trap placement space.
- Electrochemistry: High risk (tight = easy to get hit, combo resets). High reward (enemy density = fast combo building).

**Breadcrumbing**: Back room exit is blocked by elite enemy. Defeating elite unlocks path forward (door behind them).

**Metrics to Track**:
- Clear time vs. other paths (is this path faster or slower than Theater/Concert?)
- Damage taken (tight spaces should be high-damage but short duration)
- Path abandonment rate (do players enter and retreat? If >15%, space is too punishing)

---

#### THEATER WAREHOUSE (Path B: Vertical Platforming)

**Purpose**: Introduce verticality as core mechanic. Reward Empathy/Logic (builds with mobility/spatial thinking). Test Authority/Electrochemistry (less vertical mobility).

**Layout**:

```
        CATWALKS (4th floor)
        Evidence fragment x1
             |
        STAGE LEVEL (3rd floor)
        Enemy x2 (ranged)
             |
        SEATING AREA (2nd floor)
        Enemy x3, platforming required
             |
        LOBBY (1st floor, entry)
        Enemy x2
             |
        [Entry from Street]
```

**Vertical Range**: 15 meters ground to catwalks.
**Platforming Elements**: Collapsed seating, broken stage rigging, catwalk sections (some stable, some not).

**Pacing**: Slow build. Vertical spaces feel larger than they are. Climbing creates pacing breaks between combat encounters.

**Enemy Composition**: Mix of melee (stage level) and ranged (catwalks). Forces player to think vertically about threat.

**Evidence Fragment** (on catwalks): Theater records. Shows that Lena attended a presentation here about Pale research (links to Annette's church, La Delta thread).

**Psyche-Specific Approaches**:
- Authority: Hardest path for this build. Vertical mobility is limited. Must take ground-floor route (longer, more enemies).
- Empathy: Best path. High mobility, generous dodge, can navigate catwalks easily.
- Logic: Can use verticality for ranged advantage (if Logic build has ranged capability). Trap placement on stairs/catwalks is highly effective.
- Electrochemistry: Fast enough to speed-climb but risky (falling damage, missed jumps break combos).

**Breadcrumbing**:
- Catwalks have safety lights (dim red, industrial).
- Stable platforms are visually distinct from unstable (color-coded: grey = safe, rust-orange = dangerous).
- Path forward (to convergence) is visible from catwalks (looking down shows exit door).

**Environmental Storytelling**:
- Old theater posters on walls (pre-Revolution cultural events, faded but legible).
- Warehouse inventory crates (modern, stamped with Wild Pines logo).
- The contrast is architectural: the theater's beauty is still visible under the warehouse's function.

**Metrics to Track**:
- Platforming failure rate (do players fall? Where? Are danger platforms clear enough?)
- Path clear time vs. other routes
- Psyche build distribution on this path (is it Empathy-dominated? Should be)

---

#### CONCERT HALL (Path C: Boss Fight + Evidence Payoff)

**Purpose**: Highest difficulty path. Greatest evidence reward. Boss encounter with narrative and mechanical weight.

**Layout**:

```
        STAGE (boss arena)
        15m x 20m, open
             |
        AUDITORIUM
        (4 enemies, can be
         avoided via side paths)
             |
        GRAND LOBBY
        (3 enemies, chandelier
         hazard)
             |
        [Entry from Street]
```

**Total Enemies**: 7 standard + 1 boss.
**Evidence Fragments**: 3 (highest single-path yield in Capeside).

**Boss: THE MAESTRO** (Pale-Touched Conductor)

A former concert hall conductor who stayed after the hall was sold. Pale exposure from prolonged isolation in a Pale-thin spot. Now hostile, erratic, believes they are still conducting performances.

**Boss Mechanics**:
- **Musical Phases**: Boss attacks sync to rhythm (3/4 time signature). Learning the rhythm allows prediction.
- **Environmental Hazard**: Concert hall organ is functional. Boss activates organ pipes that create sound-wave AoE attacks.
- **Psyche-Specific Variations**:
  - vs. Authority: Boss is aggressive, challenges player's dominance of space.
  - vs. Empathy: Boss telegraphs attacks musically (audio cues are earlier than visual cues).
  - vs. Logic: Boss has predictable phase pattern (3 attacks -> organ activation -> repeat).
  - vs. Electrochemistry: Boss tempo increases with player combo counter (adapts to player aggression).

**Narrative Integration**: Mid-fight Internal Voice fires. The Maestro's thoughts bleed through:
- "The music never stops. Even when the audience leaves. Even when the walls sell. The music never stops."

This is the Pale's effect made human. The player is not fighting a monster. They are fighting what the Pale does to someone who stays too long in a thin spot.

**Victory**: Boss collapses. Organ stops. Silence. A moment of environmental audio (just wind through broken windows, distant city ambience). Then loot drops.

**Evidence Fragments** (post-boss):
1. Concert hall program (Lena attended event here, same night as theater presentation). Timeline fragment.
2. Maestro's journal (incoherent but contains Pale measurements that match Lena's research). Scientific evidence.
3. Backstage pass (links Lena to Annette — both attended same event). Meta-case thread.

**Pacing**: Longest path. 15-18 minutes if player engages all enemies. 10-12 if player uses stealth/evasion before boss. High commitment, high reward.

**Breadcrumbing**: Stage is visible from lobby. Boss is visible (pacing on stage) from auditorium entry. Player sees the challenge before committing.

**Metrics to Track**:
- Boss clear rate (target: 60-70%, harder than Whirling boss)
- Evidence collection rate (all 3 fragments, or do players miss backstage area?)
- Path choice rate (is Concert Hall chosen by experienced players or avoided by new players?)

---

#### ROOFTOP ROUTE (Optional Secret Path)

**Purpose**: Reward exploration. Offer high-risk shortcut. Provide Insight bonus for skilled players.

**Access**: From Theater Warehouse catwalks, a broken window leads to rooftops. Easy to miss (no explicit marker). Empathy 5+ OR Electrochemistry 4+ builds notice it (psyche-gated environmental awareness).

**Layout**:

```
    [Concert Hall Roof]
         |
    ROOFTOP GAP (jump required,
     3m distance, fall = death)
         |
    [Theater Roof]
         |
    ROOFTOP GAP (jump required)
         |
    [Pawnshop Roof]
         |
    [Convergence Point, bypasses
     all ground-level content]
```

**Challenge**: Three jumps. Miss any jump = death (fall damage is lethal). No enemies. Pure platforming challenge.

**Reward**:
- Insight cache (+5 Insight, highest single pickup in Capeside).
- Evidence fragment (Lena's route map, shows she used rooftops to avoid being followed — paranoia evidence).
- Time saved (skips 60% of district combat if player entered via Theater or Pawn paths).

**Design Intent**: Hardcore option. Not for new players. Not mandatory. Exists to reward mastery and exploration.

**Psyche Build Viability**:
- Authority: Cannot access (too low mobility).
- Empathy: Ideal build (longest dodge = easiest jumps).
- Logic: Can access but risky (no safety net if puzzle-solving fails).
- Electrochemistry: Can access, high risk (speed helps jumps but one mistake = death).

**Metrics to Track**:
- Discovery rate (what % of players find this route?)
- Death rate on route (should be 40-50%, this is meant to be hard)
- Insight spend pattern of players who succeed (do they spend the bonus Insight differently?)

---

### DISTRICT 4: VALLEY OF THE DOGS (Industrial Horror)

**Purpose**: Shift from cultural decay to systemic violence. Introduce pharmaceutical conspiracy thread. Darkest emotional beat in the game.

**Emotional Beat**: Compliance. The feeling of a place where people have agreed to harm themselves because the alternative is starvation.

**Spatial Identity**: Factory floors. Assembly lines (still running). Pharmaceutical production. Clean, bright, and deeply wrong. This is not abandoned decay (Martinaise) or sold-off beauty (Capeside). This is *functional* horror.

**Color Palette**: Sterile white, industrial yellow, chemical blue. Bright fluorescents. No shadows. The light hides nothing because there is nothing to hide. The violence is policy.

**Dominant Verticality**: Medium. Factories have 2-3 floors (production floor, catwalks, storage). Vertical space is utilitarian, not aesthetic.

#### Flow Diagram (Top-Down)

```
    [Entry from Capeside or Jamrock]
         |
    FACTORY ENTRANCE
    (security checkpoint,
     4 enemies, intimidation optional)
         |
      +--+--+
      |     |
   PRODUCTION ASSEMBLY
    FLOOR    LINE
   (enemies, (moving hazard,
    evidence, platforming,
    worker NPCs) enemies)
      |     |
      +--+--+
         |
    PHARMACEUTICAL LAB
    (boss: Viktor Hardie,
     narrative climax,
     evidence payoff)
         |
    [Exit to La Delta or Jamrock]
```

**Total Room Count**: 8 combat rooms, 1 safe room, 1 boss room.
**Estimated Clear Time**: 12-16 minutes.
**Insight Budget**: 14-18 drops (highest in game, but evidence is darkest).

---

#### FACTORY ENTRANCE (Checkpoint)

**Purpose**: Establish tone. Offer moral choice (intimidate past or fight through). Introduce Viktor Hardie (visible but not yet engageable).

**Layout**:

```
        GUARD STATION
    [Security] [Security]
         |         |
    METAL DETECTOR (functional)
    Alarm triggers if player
    carries "evidence" (from
    previous districts)
         |
    LOBBY (corporate aesthetic,
     Wild Pines branding)
         |
    [Entry from Street]
```

**Enemy Count**: 4 (corporate security, better equipped than Capeside guards).

**Moral Choice Mechanic**:
- Authority 6+ OR Logic 5+ can bypass combat via dialogue (intimidate or forge clearance).
- Empathy builds cannot bypass (no social engineering option against trained security).
- Electrochemistry builds can attempt distraction (low success rate, high comedy value).

**Viktor Hardie Sighting**: Visible through office window (second floor, behind glass). He is on a phone call. He sees the detective. He does not react. He finishes his call. This is power. He is not afraid.

**Pacing**: Moderate tension. This is not an ambush. This is a threshold. The detective is entering corporate space. The rules are different here.

**Breadcrumbing**:
- Production Floor entrance: Heavy door, industrial signage ("AUTHORIZED PERSONNEL ONLY").
- Office corridor: Visible through glass wall, leads to Viktor (locked, inaccessible until later).

**Environmental Storytelling**:
- Corporate safety posters (bright, cheerful, in stark contrast to the armed guards).
- Worker time-clock station (punch cards, names listed — humanizes the NPCs the player will see on production floor).
- Pharmaceutical supplement dispensary (locked cabinet, visible through glass — foreshadowing).

**Metrics to Track**:
- Bypass rate (what % use dialogue vs. combat?)
- Alarm trigger rate (do players understand the metal detector mechanic?)
- Viktor sighting reaction (do players try to reach him immediately? Track attempted routes)

---

#### PRODUCTION FLOOR (Worker NPC Space)

**Purpose**: Moral weight. Enemies here are not criminals or psychic manifestations. They are workers, augmented by supplements, defending their workplace because they have been told to.

**Layout**:

```
    ASSEMBLY STATIONS (6 total)
    Workers at stations (non-hostile unless player approaches)
         |         |         |
      CATWALK (above, security patrols)
         |
    EVIDENCE LOCKERS (research data)
         |
    [Entry from Checkpoint]
```

**Enemy Count**: 6 workers (conditional hostility) + 3 security (always hostile).

**NPC Worker Behavior**:
- Workers continue working unless player enters their "territory" (3m radius around station).
- Workers fight reluctantly (dialogue triggers: "I need this job." "Please, just leave.").
- Workers have low HP but high damage (supplement augmentation).

**Design Intent**: Make the player feel bad. These are not enemies. These are victims who have been turned into obstacles. The violence here is systemic, not personal.

**Psyche-Specific Reactions**:
- Authority: Can order workers to stand down (50% success rate, depends on intimidation presence).
- Empathy: Hears workers' dialogue, sees their fear. Internal Voice fires: "They're terrified. Of you. Of losing this. Of everything."
- Logic: Analyzes supplement augmentation patterns. Identifies which workers are most affected (targeting information).
- Electrochemistry: Recognizes supplement chemistry (same compounds as evidence from Martinaise). Meta-thread connection.

**Evidence Fragments**:
- Worker medical records (locked in office, requires Logic 4+ to access). Shows neurological side effects. Viktor's signature on approval forms.
- Supplement formula (in evidence locker). Matches Pale-adjacent chemical signatures from Lena's research.

**Pacing**: Slow, heavy. This is not a fun combat section. This is a necessary one. The player should feel the weight of what this place is doing.

**Breadcrumbing**: Assembly Line entrance is at far end of floor (visible, marked by active machinery sounds).

**Metrics to Track**:
- Worker engagement rate (do players avoid or fight?)
- Dialogue skip rate (are players reading the workers' lines?)
- Empathy players' behavior (do high-Empathy builds play differently here? They should)

---

#### ASSEMBLY LINE (Moving Hazard Platforming)

**Purpose**: Environmental hazard as primary challenge. Teach that not all threats are enemies.

**Layout**:

```
    CONVEYOR BELTS (moving, 3 lanes)
         |         |         |
    STAMPING PRESS (periodic hazard)
         |
    CHEMICAL VATS (fall = death)
         |
    ENEMIES (2 augmented workers,
     patrol the belts)
         |
    [Entry from Production Floor]
```

**Challenge**: Navigate moving platforms + avoid stamping press (1-shot kill if player is under press during activation) + fight 2 enemies.

**Timing**: Press activates every 8 seconds (audio cue 2 seconds before: hydraulic hiss).

**Psyche-Specific Approaches**:
- Authority: Slow movement is liability. Must time press carefully, cannot rely on speed.
- Empathy: Long dodge helps navigate belts. Can i-frame through press activation if timed perfectly (0.2 second window).
- Logic: Can disable press temporarily (electrical panel puzzle, requires Logic 5+). Removes hazard entirely.
- Electrochemistry: Speed allows rushing through hazard windows. High risk (mistimed = death). High reward (fastest clear).

**Pacing**: High tension. Environmental hazard + combat = dual attention demand. Forces player to track multiple threats.

**Evidence Fragment**: Worker's journal (hidden under conveyor belt, requires crouching/exploring). Contains evidence that workers KNOW the supplements are harmful but cannot afford to refuse them. Damning moral evidence against Wild Pines.

**Breadcrumbing**: Lab entrance (Viktor's boss arena) is visible from far end of Assembly Line. Backlit glass door, clean white light beyond. The aesthetic shift from industrial yellow to pharmaceutical white is visible before entering.

**Metrics to Track**:
- Death rate (target: 25-35%, this is a hard section)
- Death cause (press vs. enemies vs. falling — which is primary threat?)
- Logic players' press disable rate (if low, puzzle is too obscure)

---

#### PHARMACEUTICAL LAB (Boss Fight: Viktor Hardie)

**Purpose**: Narrative climax of Valley arc. Viktor is not a monster. He is a man who made a choice and has been justifying it ever since.

**Layout**:

```
        EVIDENCE VAULT (locked,
         post-boss access)
              |
        OBSERVATION WINDOW
        (overlooks Production Floor)
              |
        LAB FLOOR (15m x 12m)
        Clean, white, sterile
        Chemical storage units (cover)
              |
        [Entry from Assembly Line]
```

**Boss: Viktor Hardie**

Not augmented. Not supernatural. A middle-aged corporate security chief with a sidearm, tactical training, and a conscience he has spent years ignoring.

**Boss Mechanics**:
- **Phase 1** (100-70% HP): Ranged combat. Viktor uses cover, fights tactically. Professional.
- **Phase 2** (70-40% HP): Viktor calls reinforcements (2 augmented workers arrive). Tests player's ability to manage multiple threats.
- **Phase 3** (40-0% HP): Viktor fights desperately. Dialogue triggers mid-phase:
  - "You don't understand. If I don't do this, someone else will."
  - "The system doesn't care about my guilt. It cares about productivity."
  - "I know their names. I recite them. What more do you want from me?"

**Psyche-Specific Dialogue Options** (mid-fight, can de-escalate):

| Psyche Build | Dialogue Option | Viktor's Response | Outcome |
|--------------|----------------|-------------------|---------|
| Authority 7+ | "You're done. Surrender." | Viktor stands down (if HP >40%) | Partial de-escalation, fight ends |
| Empathy 6+ | "You don't have to keep doing this." | Viktor breaks down | Full de-escalation, boss yields |
| Logic 6+ | "I have the evidence. You've already lost." | Viktor calculates, realizes truth | Partial de-escalation, boss yields but takes cyanide capsule (suicide) |
| Electrochemistry 5+ | "You're as trapped as the workers." | Viktor laughs bitterly, fights harder | No de-escalation, fight continues |

**Design Intent**: Not all bosses are beaten with violence. Some are beaten with truth. The player can choose to kill Viktor or break him. Both options yield evidence. The moral weight is on the player.

**Victory Loot**:
- **If defeated in combat**: Viktor's security clearance (access to Evidence Vault).
- **If de-escalated**: Viktor provides clearance + testimony (additional evidence fragment about Coalition's knowledge of supplement side effects).

**Evidence Vault Contents** (post-boss):
1. Pharmaceutical trial data (shows 15% neurological damage rate, deliberately suppressed).
2. Correspondence between Viktor and Coalition liaisons (proving Coalition knew and allowed program to continue).
3. Lena Hargate's confiscated research (Viktor seized her work when she tried to publish about Pale-pharmaceutical links).

This is the smoking gun. This is why Lena had to die. She had proof that the supplements were accelerating Pale exposure in workers.

**Pacing**: Long fight (4-6 minutes if full combat). Shorter if de-escalated (2-3 minutes). Emotional, not mechanical, challenge.

**Breadcrumbing**: After boss, exit unlocks (to La Delta or Jamrock). Also unlocks access to Evidence Vault (door that was locked pre-fight).

**Metrics to Track**:
- De-escalation rate (what % of players talk Viktor down vs. kill him?)
- De-escalation method (which psyche build succeeds most?)
- Evidence Vault access rate (do players find it post-fight? If <80%, signposting needs improvement)

---

### DISTRICT 5: LA DELTA (The Old Quarter / Endgame)

**Purpose**: Deepest lore. Pale Rift access. Annette encounter. The place where science and faith converge.

**Emotional Beat**: Mystical dread. The feeling that you are approaching something the world was not meant to understand and understanding it anyway.

**Spatial Identity**: Ancient architecture (pre-Revolution). Narrow streets, esoteric bookshops, church spires, and beneath it all, the Pale Rift — a physical tear in reality.

**Color Palette**: Deep blue shadows, candlelight gold, Pale grey-white (entropic, wrong). The old world's colors infected by the Pale's non-color.

**Dominant Verticality**: Extreme. La Delta has both the highest points (church bell tower) and the lowest (Pale Rift, underground). Vertical range of 30+ meters.

#### Flow Diagram (Top-Down)

```
            CHURCH BELL TOWER
            (Annette encounter,
             lore fragments,
             overlook of full district)
                  |
            CHURCH NAVE
            (safe room, debrief,
             faith-based Insight spend)
                  |
    [OLD QUARTER STREETS] (entry)
       |         |         |
   BOOKSHOP  FORTUNE  CULT
   (evidence, TELLER  HIDEOUT
    Logic)   (Empathy) (combat)
       |         |         |
       +----+----+---------+
                  |
            PALE RIFT ENTRANCE
            (descending, underground)
                  |
            THE RIFT
            (final boss, revelation,
             meta-case convergence)
                  |
    [Exit to Precinct (run ends here)]
```

**Total Room Count**: 12 combat rooms, 2 safe rooms, 1 final boss arena.
**Estimated Clear Time**: 15-20 minutes (longest district).
**Insight Budget**: 16-20 drops (highest total, but heavily narrative-gated).

---

#### OLD QUARTER STREETS (Entry)

**Purpose**: Establish mystical tone. Offer three exploration paths (Bookshop, Fortune Teller, Cult Hideout). Converge at Church.

**Layout**:

```
         CHURCH (visible landmark,
          distant, up hill)
              |
    NARROW STREETS (3m wide,
     winding, no straight sightlines)
       |      |      |
   [Path A][Path B][Path C]
       |      |      |
   [Entry from Valley or Jamrock]
```

**Aesthetic**:
- Cobblestones (uneven, affect movement — slightly slower than modern streets).
- Gas lamps (period lighting, warm and dim).
- Architecture: stone, gargoyles, stained glass windows.
- The modern city's neon does not reach here. La Delta refuses the future.

**Enemy Type**: Cultists (Innocentic extremists, not affiliated with Annette's official church). Low HP, high damage, erratic behavior (Pale exposure symptoms).

**Where does the player LOOK?**
- First: The church (uphill, illuminated, visible from entry — the destination).
- Second: The three paths (choice, exploration, route planning).
- Third: Environmental details (books in shop windows, tarot signs, strange symbols on walls).

**Pacing**: Slow exploration. La Delta is not a combat gauntlet. It is an investigation site. The player should feel like they are *discovering*, not *fighting*.

**Breadcrumbing**: Church is always visible (via verticality and sightlines). The player cannot get lost. The paths diverge but the destination is clear.

**Metrics to Track**:
- Path choice distribution
- Time spent in exploration vs. combat (should be 60/40 exploration-heavy)
- Enemy engagement rate (are players avoiding combat to focus on exploration?)

---

#### BOOKSHOP PATH (Logic Evidence Route)

**Purpose**: Deliver scientific evidence about the Pale. Logic-focused environmental puzzle.

**Layout**:

```
    RARE BOOKS SECTION
    (puzzle: find correct book
     via Dewey Decimal-style clues)
         |
    MAIN FLOOR
    (1 enemy, can be avoided
     via stealth)
         |
    [Entry from Street]
```

**Puzzle**: Five bookshelves. One contains Lena Hargate's hidden research (she stashed a copy here before going to Whirling-in-Rags). Clues are in the environment:
- Receipt on counter (book title partially visible).
- Dewey Decimal number written on detective's hand (Internal Voice provides this if Logic 4+).
- Shelf labels (faded but legible).

**Reward**: Lena's full research paper (co-authored with Annette). Proof that Pale expansion is being accelerated by industrial chemical runoff (Valley pharmaceuticals) interacting with Pale-thin spots. This is the scientific half of the game's central revelation.

**Enemy**: Single bookshop keeper (Pale-touched, non-hostile unless player steals books without solving puzzle).

**Pacing**: Slow puzzle-solving. Combat optional. For players who want to think, not fight.

**Psyche-Specific Access**:
- Logic 4+: Puzzle is solvable.
- Empathy 5+: Can talk to bookshop keeper, who provides direct clues (social solution to Logic puzzle).
- Authority/Electrochemistry: No shortcut. Must solve puzzle or skip entirely.

**Metrics to Track**:
- Puzzle solve rate
- Time spent in bookshop (if >5 minutes, puzzle is too obscure)
- Evidence discovery rate (does every player find Lena's research, or is it missable?)

---

#### FORTUNE TELLER PATH (Empathy Lore Route)

**Purpose**: Deliver mystical context for the Pale. Empathy-focused dialogue encounter.

**Layout**:

```
    READING ROOM
    (Fortune Teller NPC,
     tarot reading mechanic)
         |
    WAITING ROOM
    (atmospheric, no combat,
     candles, incense)
         |
    [Entry from Street]
```

**NPC**: The Fortune Teller (Pale-sensitive, not Pale-damaged). She reads tarot for clients, but what she actually reads is Pale resonance. She knows things she should not know.

**Mechanic**: Tarot reading (narrative, not mechanical). Player draws three cards:
1. **The Past**: The Revolution. "You carry the weight of a city's broken heart."
2. **The Present**: The Fragmented Detective. "You are many. You have always been many. The Pale shows what was already true."
3. **The Future**: The Choice. "The Rift will offer you an ending. Whether you take it determines who you become."

**Reward**: Lore fragments about the Pale Rift (it is not expanding — it has always been there, beneath La Delta, predating the city). Contextualizes the entire meta-case.

**Cost**: 6 Insight (Fortune Teller's reading is expensive but yields no hard evidence, only understanding).

**Psyche-Specific Readings**:
- Empathy 5+: Fortune Teller offers additional reading (about the detective's past, heavily implied they are a Pale echo).
- Logic 3+: Can challenge the Fortune Teller's methods (she admits the tarot is metaphor, but the Pale resonance is real).

**Pacing**: Full stop. Dialogue-heavy. Emotional beat, not mechanical.

**Metrics to Track**:
- Visit rate (what % of players choose this path?)
- Insight spend rate (do players pay for the reading?)
- Dialogue skip rate (are players engaged or impatient?)

---

#### CULT HIDEOUT PATH (Combat Gauntlet)

**Purpose**: Highest combat density in La Delta. For players who want Insight and are willing to fight for it.

**Layout**:

```
    RITUAL CHAMBER
    (3 enemies, 1 elite,
     evidence fragment)
         |
    HALLWAY
    (2 enemies, tight)
         |
    ENTRY ROOM
    (2 enemies, altar as
     environmental hazard)
         |
    [Entry from Street]
```

**Enemy Type**: Innocentic Cultists (extremists, high damage, low HP, Pale-touched).

**Environmental Hazard**: Ritual altar (if activated by player or enemy, releases Pale energy burst — AoE damage, affects everyone).

**Pacing**: High tension. 7 enemies across 3 rooms. Highest combat density since Whirling hallway gauntlet.

**Evidence Fragment**: Cult's manifesto (they believe accelerating the Pale will bring about a spiritual reckoning — they are INTENTIONALLY feeding the Rift).

**Reward**: High Insight yield (12-14 total from all enemies and evidence).

**Psyche-Specific Challenges**:
- Authority: Straightforward combat. Authority builds thrive here.
- Empathy: Cultists are erratic (Pale exposure). Telegraphs are unreliable. High difficulty.
- Logic: Altar can be turned into a trap (lure enemies near, activate, retreat).
- Electrochemistry: Narrow spaces + high enemy count = ideal combo-building environment.

**Metrics to Track**:
- Path choice rate (is this the least or most chosen path?)
- Death rate (should be highest of the three La Delta paths)
- Altar interaction rate (do players use it as a tool or avoid it as a hazard?)

---

#### CHURCH NAVE (Safe Room / Annette Encounter)

**Purpose**: Emotional center of La Delta. Annette provides the faith-based interpretation of the Pale. Debrief and Insight spend.

**Layout**:

```
         ALTAR (Innocentic symbols)
              |
         PEWS (empty, dust-covered)
              |
    ANNETTE (standing at altar,
     waiting)
              |
         [Entry from three paths]
```

**Size**: 20m x 30m. Largest interior space in the game. High ceilings (15m). Stained glass windows (depicting the Pale as divine light, not entropy).

**Lighting**: Candles, stained glass filtered light (blue, gold, red). Warm despite the subject matter.

**Pacing**: Full stop. Longest debrief in the game. Annette has the most dialogue of any NPC.

**Narrative Beat**: Annette reveals her collaboration with Lena. They were writing a joint paper: science and faith converging on the same truth. Lena provided measurements. Annette provided interpretation. Together, they proved the Pale Rift is being fed.

**Insight Spend Options**:

| Question | Insight Cost | What You Learn | Psyche Gate |
|----------|-------------|----------------|-------------|
| "What is the Pale?" | 4 | Annette's theological explanation (the Pale is accumulated sorrow, not void) | None |
| "What happened to Lena?" | 6 | Annette admits she was with Lena the night before the murder (provides alibi evidence for some suspects, incriminates others) | Empathy 4+ |
| "What's in the Rift?" | 8 | Annette describes her vision (the Rift is a threshold, not a wound) | Logic 5+ OR Empathy 6+ |
| "Why didn't you stop her?" | 5 | Annette's guilt (she knew Lena was in danger, did not intervene, has been grieving since) | Empathy 5+ |

**Total Potential Cost**: 23 Insight (player cannot afford all questions unless they cleared all three paths).

**Annette's Function**: She is not a suspect here (though she was in earlier districts, depending on psyche build). Here, she is a guide. She provides the map to the Pale Rift (literal: a hand-drawn schematic of the underground entrance).

**Breadcrumbing**: After Annette dialogue, two paths unlock:
1. Bell Tower (optional, lore reward, no combat).
2. Pale Rift Entrance (final boss, meta-case resolution).

**Metrics to Track**:
- Insight spend distribution (which questions do players prioritize?)
- Annette dialogue completion rate (do players exhaust all dialogue or skip to Rift?)
- Path choice post-Annette (Bell Tower exploration vs. immediate Rift descent)

---

#### CHURCH BELL TOWER (Optional Lore Space)

**Purpose**: Reward exploration with environmental storytelling and a moment of beauty before the Rift's horror.

**Layout**:

```
    BELL (climbable, can be rung)
         |
    OVERLOOK PLATFORM
    (360-degree view of Revachol)
         |
    SPIRAL STAIRS (narrow, 20m climb)
         |
    [Entry from Nave]
```

**Reward**:
- **Visual**: The player sees all previous districts from above (Martinaise docks, Capeside rooftops, Valley factories). The city is beautiful from here. The rain and neon create a painting.
- **Audio**: If player rings the bell, a musical tone echoes across the city. A moment of grace.
- **Lore Fragment**: Inscriptions on the bell (pre-Revolution, religious, about hope and resurrection). Thematically ties to the detective's own cycle of death and return.

**Pacing**: Slow. Contemplative. This is the exhale before the final dive.

**Metrics to Track**:
- Exploration rate (what % of players climb the tower?)
- Bell ring rate (do players interact with the bell?)
- Time spent at overlook (are players taking in the view or rushing?)

---

#### PALE RIFT (Final Boss / Meta-Case Revelation)

**Purpose**: The truth. All of it. The place where timelines converge, where the detective confronts the nature of their own existence, where the meta-case resolves.

**Layout**:

```
         THE RIFT (center)
         Grey-white void,
         reality dissolving,
         multiple timelines visible
              |
         PLATFORM (stone, ancient,
          predates Revachol)
              |
         DESCENT (spiral path,
          underground, 15m down)
              |
         [Entry from Church basement]
```

**Environmental Description**: The Rift is not a place. It is an *unplace*. The architecture is wrong — stairs lead nowhere, walls curve into themselves, gravity feels negotiable. Visually: grey-white entropy, like TV static made spatial. Auditorily: whispers in the detective's own voice, echoes of previous runs' conclusions.

**Enemy: THE CONVERGENCE**

Not a person. Not a creature. A manifestation of the Pale Rift itself. The Convergence is the detective's previous psyche builds, all at once, all fighting for dominance.

**Boss Mechanics** (unique, unlike any previous fight):

- **Phase 1**: The Convergence takes the form of the player's dump stat archetype (the psyche facet they are LEAST dominant in this run). Forces player to fight their opposite.
  - If player is Authority-dominant, fights Empathy-form (fast, evasive, reads player's attacks).
  - If player is Empathy-dominant, fights Authority-form (heavy, aggressive, controls space).
  - Etc.

- **Phase 2**: The Convergence splits into TWO forms (player's two weakest archetypes). 2v1 fight. Tests multi-threat management.

- **Phase 3**: The Convergence becomes a mirror (all four archetypes present, shifting). Attacks mimic the player's own combat patterns. The player is fighting themselves.

**Narrative Integration**:
- Mid-Phase 1: Internal Voice fires. All four psyche facets speak at once (overlapping dialogue, cacophony). Success = the detective integrates the input without breaking. Failure = psychic damage + disorientation effect.
- Mid-Phase 2: The Rift shows visions (previous runs' case conclusions, all contradictory, all true).
- Mid-Phase 3: The detective realizes the truth: **they are not solving a murder. They are experiencing a murder from every possible perspective simultaneously. The Rift has made them the instrument of total perception.**

**Victory Condition**: The Convergence dissolves. The Rift stabilizes. The player stands in the center of a space where all timelines overlap.

**The Final Choice** (dialogue, not combat):

The Rift offers a vision: **Who killed Lena Hargate?**

The player is presented with EVERY suspect they have identified across ALL runs (via meta-case board). They choose one to accuse. The accusation is final. The run ends.

**The Twist**: The accusation the player makes is not "correct" or "incorrect." It is simply the truth *from this detective's accumulated perspective*. The game does not tell the player if they were right. It shows them the consequence:

- **The meta-case board** gains a new thread (the accusation connects to existing evidence in specific ways).
- **The precinct hub** shows Jean's reaction (varies based on accusation and accumulated psyche dominance across runs).
- **The next run begins** (psyche reshuffles, but now the player has seen the Rift — future runs have access to new dialogue options and evidence).

**Design Intent**: There is no canon answer. The final accusation is the player declaring "this is the truth I have built from my journey." Every player's answer is different because every player's journey is different.

**Pacing**:
- Descent to Rift: 2-3 minutes (slow, building dread).
- Boss fight: 5-8 minutes (longest fight in game).
- Final Choice: 2-4 minutes (dialogue, reflection).
- Total: 10-15 minutes for district climax.

**Metrics to Track**:
- Boss clear rate (target: 50-60%, this is HARD)
- Most common accusation (which suspect do players choose most? Does it correlate with psyche dominance trends?)
- Internal Voice success rate in Phase 1 cacophony (target: <30%, this is meant to be overwhelming)
- Player deaths per phase (which phase is hardest?)

---

## III. PACING ACROSS THE FULL GAME

### Run Pacing Curve (Single Run, 20-40 Minutes)

```
Tension
  ^
  |                          LA DELTA
  |                         (Pale Rift,
  |                          final boss,
  |                          revelation)
  |                             /\
  |                            /  \
  |              VALLEY       /    \
  |             (Viktor,     /      \
  |              moral      /        \
  |              weight)   /          \
  |                 /\    /            \
  |                /  \  /              \
  |    CAPESIDE   /    \/                \
  |   (verticality,    CHURCH             \
  |    beauty-decay)  (Annette,            \
  |       /\          debrief)              \
  |      /  \        /                       \
  | MARTINAISE      /                         \
  |(Whirling,      /                           \
  | boss,         /                             \
  | evidence)    /                               \
  |    /\       /                                 \
  |   /  \     /                                   \
  |  /    \   /                                     \
  | /  CONTAINER  PRODUCTION                         \
  |/ MAZE         FLOOR                               \
  |  (tight)     (moral weight)                        \
  +-+----+----+----+----+----+----+----+----+----+----+-> Time
    2   4    6    8   10   12   14   16   18   20   22min
    |         |         |         |         |
  JAMROCK  SAFE RM  SAFE RM   SAFE RM   FINAL
  (tutorial) (Union) (Church)  (various) CHOICE
```

**Design Intent**: Peaks and valleys. Never flat. Safe rooms are valleys (decompression). Boss fights are peaks (maximum tension). The final peak (Pale Rift) is the highest because it is earned.

**Key Observations**:
- First 5 minutes are low tension (Jamrock tutorial + Dockside entry). This teaches without punishing.
- Minutes 5-10 escalate steadily (Container Maze -> Whirling). First major peak.
- Minutes 10-15 vary by path (Capeside offers player-determined difficulty via path choice).
- Minutes 15-18 are the moral weight section (Valley production floor, Viktor). Not mechanically hardest, but emotionally heaviest.
- Minutes 18-22+ are endgame (La Delta, Pale Rift). Highest mechanical AND narrative tension.

**Difficulty Scaling Across Districts**:

| District | Mechanical Difficulty | Narrative Complexity | Emotional Weight |
|----------|----------------------|---------------------|------------------|
| Jamrock | 1/10 (tutorial) | 2/10 (intro) | 3/10 (institutional) |
| Martinaise | 4/10 (moderate) | 6/10 (case intro) | 6/10 (melancholy) |
| Capeside | 5/10 (player choice) | 5/10 (faction lore) | 4/10 (aesthetic tragedy) |
| Valley | 6/10 (high) | 7/10 (conspiracy) | 9/10 (moral horror) |
| La Delta | 8/10 (highest) | 10/10 (revelation) | 10/10 (existential) |

The game does not scale linearly. It scales *holistically* — later districts are harder mechanically, narratively, and emotionally.

---

### Meta-Progression Pacing (Across 30+ Runs)

```
Meta-Case
Understanding
  ^
  |                                    LAYER 5
  |                                  (Final Accusation,
  |                                   integrated build,
  |                                   full perspective)
  |                              .....
  |                         .....
  |                    .....  LAYER 4
  |               .....      (Detective's
  |          .....            connection to
  |     .....   LAYER 3       conspiracy)
  |.....       (Conspiracy      |
  |           revealed)          |
  |   LAYER 2     |              |
  |  (Connections  |              |
  |   between      |              |
  |   suspects)    |              |
  |      LAYER 1   |              |
  |     (Surface   |              |
  |      case)     |              |
  +------+----+----+----+----+----+----+-----> Runs
         5   10   15   20   25   30   35+
```

**Layer Unlocks**:
- **Layer 1** (Runs 1-5): Who killed Lena? (Four contradictory answers emerge.)
- **Layer 2** (Runs 6-15): Why do all four answers connect to the same organizations? (Hardy Boys, Wild Pines, Coalition, Church.)
- **Layer 3** (Runs 16-25): The conspiracy. (Pale Rift is being fed. Lena discovered proof. She was silenced.)
- **Layer 4** (Runs 26-35): The detective's role. (They are Pale-touched. Their fragmentation is not incidental. They were chosen.)
- **Layer 5** (Run 36+): The final accusation. (Armed with all perspectives, choose the truth you believe.)

**Pacing Intent**: The first 5 runs feel like replaying the same case. Runs 6-15 feel like peeling an onion (each layer reveals another). Runs 16-25 feel like conspiracy investigation (connecting distant threads). Runs 26+ feel like self-discovery (the case is about the detective).

**Metrics to Track Across Runs**:
- Meta-case board fill rate (what % of total evidence nodes are discovered by run 10? 20? 30?)
- Layer unlock timing (does Layer 2 unlock at intended run count, or earlier/later?)
- Player churn rate (at which run count do players stop playing? Target: <10% churn before Layer 3)

---

## IV. BREADCRUMBING & WAYFINDING STRATEGY

### Core Principle

**The level is the UI. The player's eye is the cursor.**

No minimap. No waypoint markers. No objective arrows. The player navigates via:
1. **Light** (where light falls, the path lies)
2. **Sight lines** (what you can see, you can reach)
3. **Audio** (sound sources guide attention)
4. **Architecture** (doors, stairs, landmarks)

### Light as Language

**Warm light = safety.** Safe rooms, debrief spaces, friendly NPCs — all lit with warm tones (amber, gold, orange).

**Cool light = investigation.** Evidence, crime scenes, lore spaces — all lit with cool tones (blue, white, grey).

**Neon = the city's voice.** Faction presence, commercial zones, modern intrusions into old spaces — marked by neon (reds, pinks, cyans).

**Flickering light = danger.** Combat zones, boss arenas, hazard areas — unstable lighting telegraphs threat.

**No light = unknown.** Unvisited areas, locked paths, secrets — darkness is promise and warning.

### Sight Line Design Rules

1. **Landmarks are always visible.** The crane in Martinaise. The church in La Delta. The factory stacks in Valley. From any outdoor space, the player sees the district's identity.

2. **Goals are visible before gates.** Room 208 is visible before the Whirling boss fight. Viktor's office is visible before the Assembly Line. The player sees the reward, commits to the challenge.

3. **Danger is telegraphed spatially.** Narrow corridors signal tight combat. Open arenas signal bosses. Vertical spaces signal platforming. The geometry warns the player.

4. **Negative space is readable.** Fog limits Martinaise sight lines (teaches caution). Bright fluorescents eliminate shadows in Valley (teaches "nowhere to hide"). Architecture communicates rules.

### Audio Breadcrumbing

**Enemy audio**: Distinct per type. Dockworker Enforcers have heavy footsteps. Corporate Security has radio chatter. Cultists have whispered prayers. The player hears threats before seeing them.

**Environmental audio**: Water lapping (Martinaise waterfront direction). Machinery hum (Valley production floor). Wind through broken windows (Whirling upper floors). The soundscape is a map.

**Music as pacing**: Combat music is reactive (intensity scales with enemy count + player HP). Safe room music is ambient (low tension, decompression). Boss music is signature (unique per boss, teaches "this is special").

**Silence as signal**: After boss defeat, 3-5 seconds of silence before victory music. After finding key evidence, audio duck (background noise reduces, focuses attention on discovery). Silence is as communicative as sound.

### Psyche-Specific Wayfinding

Different psyche builds notice different environmental cues:

- **Authority**: Territorial markers (graffiti, faction tags), power structures (who controls this space?), defensible positions (where would I make a stand?).
- **Empathy**: Habitation traces (someone lived here), emotional residue (this place was important to someone), safe spaces (where would a frightened person hide?).
- **Logic**: Structural details (load-bearing walls, weak points), system vulnerabilities (electrical panels, trap opportunities), optimal paths (shortest route calculated visually).
- **Electrochemistry**: Sensory details (textures, smells, temperature shifts), substance traces (chemical residue, drug paraphernalia), high-stimulus routes (where is the action?).

**Implementation**: Environmental highlights (subtle glow, outline, or particle effect) appear on psyche-relevant objects. Authority sees red glow on chokepoints. Empathy sees blue glow on personal effects. Logic sees gold glow on interactive systems. Electrochemistry sees green glow on sensory-rich elements.

The level does not change. The *perception* of the level changes. Same room, four reads.

---

## V. ENCOUNTER DESIGN PRINCIPLES

### Every Room is a Lesson

**Room purpose hierarchy**:
1. **Tutorial Room**: Teach one mechanic in isolation. (Example: Jamrock hallway teaches dodge.)
2. **Test Room**: Test that mechanic in context. (Example: Dockside Approach tests dodge + positioning.)
3. **Combination Room**: Combine two mechanics. (Example: Assembly Line tests dodge + environmental hazard.)
4. **Mastery Room**: All mechanics in high-pressure context. (Example: Pale Rift boss.)

**Introduction cadence**: Introduce -> Test (within 2 rooms) -> Combine (within 1 district) -> Master (within 2 districts).

**New mechanics are never introduced after District 3.** Valley and La Delta are combination and mastery zones only.

### Enemy Design Per District

| District | Enemy Type | Behavioral Theme | What They Teach |
|----------|-----------|------------------|----------------|
| Jamrock | Psyche Manifestation | Passive until engaged, generous telegraphs | "You can fight." |
| Martinaise | Dockworkers, Hardy Boys | Territorial, formation-based | "Positioning matters." |
| Capeside | Corporate Security | Defensive, cover-using | "Enemies have tactics." |
| Valley | Augmented Workers | Reluctant, high damage, low HP | "Violence has a cost." |
| La Delta | Cultists, Pale-Touched | Erratic, unpredictable telegraphs | "The Pale damages minds." |

**Design Intent**: Enemies are not just obstacles. They are worldbuilding. How they fight tells you who they are.

### Boss Design Philosophy

**Every boss teaches and tests simultaneously.**

- **Memory of Violence** (Whirling): Teaches that psyche build determines boss behavior. Tests player's understanding of their current build's strengths.
- **The Maestro** (Capeside): Teaches rhythm-based combat. Tests audio-visual pattern recognition.
- **Viktor Hardie** (Valley): Teaches that not all bosses are beaten with violence. Tests moral decision-making under pressure.
- **The Convergence** (Pale Rift): Teaches that the player is their own greatest enemy. Tests mastery of all four archetypes.

**Boss health scaling**: Bosses have 3-5x standard enemy HP. Long enough to test pattern recognition. Short enough to avoid tedium. Target fight duration: 2-5 minutes.

**Boss phases**: All bosses have 2-3 phases (mechanical shifts at 70% HP and 40% HP). Phases prevent pattern stagnation and test adaptation.

**Narrative integration**: Every boss has mid-fight dialogue or Internal Voice moments. The fight is not just mechanical. It is a conversation.

---

## VI. DIFFICULTY VARIANTS & ACCESSIBILITY

### Difficulty Settings (Impact on Level Design)

**TRAINEE** (Easy):
- Enemy count reduced by 20% per room.
- Hazard timing windows increased by 30% (stamping press, Assembly Line).
- Platforming failure = damage, not death (Rooftop Route, Theater catwalks).
- Internal Voice window: 2.0 seconds (baseline).

**DETECTIVE** (Standard):
- All values at baseline.
- Internal Voice window: 1.5 seconds.

**SPECIAL CRIMES** (Hard):
- Enemy count increased by 15%.
- Hazard timing windows reduced by 20%.
- No checkpoint saves within districts (death = restart district).
- Internal Voice window: 1.0 second.

**MORALIST** (Challenge Mode):
- Enemy count increased by 30%.
- All enemies gain one elite behavior (faster, smarter).
- Environmental hazards deal 2x damage.
- Platforming failure = always death.
- Internal Voice window: 0.6 seconds.
- Psyche shuffle is fully random (no guaranteed dominant archetype).

**Design Intent**: Difficulty affects density and timing, not geometry. The level layout is identical across difficulties. Only the encounter composition changes.

### Accessibility Considerations

**Movement Accessibility**:
- Optional: "Auto-navigate" to visible objectives (player marks a visible door, character paths to it). Does NOT work in combat.
- Optional: Adjustable dodge i-frame window (0.1-0.3 second variance).

**Combat Accessibility**:
- Optional: "Slow-motion aiming" for ranged attacks (Logic builds).
- Optional: "Auto-dodge" when telegraphed attack lands during Internal Voice window (compensates for dual attention demand).

**Narrative Accessibility**:
- Optional: Text-to-speech for all dialogue.
- Optional: Dyslexia-friendly font.
- Optional: Colorblind modes (psyche color-coding shifts to patterns + colors).

**Design Philosophy**: Accessibility options do not reduce challenge for players who do not need them. They level the playing field for players who do.

---

## VII. METRICS TO TRACK IN PLAYTESTING

### Spatial Metrics

**Heatmaps** (where do players spend time?):
- Combat heatmaps (where do fights happen? Are players using intended space, or clustering in corners?).
- Death heatmaps (where do players die? Reveals overtuned encounters or unclear hazards).
- Evidence discovery heatmaps (which evidence nodes are found? Which are missed?).

**Pathfinding Metrics**:
- Time to objective (how long does it take player to find the next required space?).
- Backtracking frequency (do players get lost and retrace steps?).
- Path choice distribution (which routes do players prefer?).

**Engagement Metrics**:
- Combat engagement rate (do players fight or evade enemies?).
- Optional content discovery rate (secrets, lore spaces, alternate routes).
- Evidence collection rate (what % of available evidence does the player gather?).

### Pacing Metrics

**Tension Curve Validation**:
- Player heartrate tracking (if available via biometric playtest tools). Does measured tension match intended curve?
- Self-reported tension (post-run survey: "Rate tension at each district, 1-10").

**Decompression Validation**:
- Time spent in safe rooms (are players using debrief spaces, or rushing through?).
- Dialogue skip rate per NPC (are players reading, or skipping?).

**Difficulty Curve Validation**:
- Death rate per district (should increase from Jamrock -> La Delta).
- Clear time per district (should increase due to complexity, not confusion).

### Narrative Metrics

**Case Refraction Validation**:
- Evidence node visibility per psyche build (are players seeing intended evidence?).
- Psyche-gated content access rate (are gates too restrictive?).
- Meta-case board fill rate across runs (is progression pacing correct?).

**Emotional Response**:
- Post-run survey: "Did the Valley production floor feel morally heavy?" (Target: >70% yes.)
- Post-run survey: "Did the Pale Rift feel revelatory?" (Target: >80% yes.)

### Insight Economy Metrics

**Spending Patterns**:
- Combat vs. narrative spend ratio (target: 50/50 across all players, but individual variance is expected).
- Regret rate (post-run survey: "Did you regret any Insight spend?" — if >40%, economy is too punishing).

**Scarcity Validation**:
- "Insight starvation" rate (players who reach debrief with <3 Insight). Target: <10%.
- "Insight overflow" rate (players who reach district end with >15 unspent Insight). Target: <5%.

---

## VIII. OPEN QUESTIONS FOR PLAYTESTING

These are questions that design docs cannot answer. Only players can.

### Spatial Questions

1. **Do players naturally navigate via light, or do they demand UI waypoints?** If >30% request waypoints, breadcrumbing has failed.

2. **Does the psyche-specific environmental highlighting feel like revelation or cheating?** Are players excited to see different things, or do they feel manipulated?

3. **Is verticality readable?** Specifically: Do players understand that Theater catwalks and Rooftop Routes are optional, or do they assume they're mandatory and get frustrated?

4. **Does the Pale Rift's impossible geometry read as "mystical" or "broken"?** There's a thin line between intentional spatial wrongness and perceived bug.

### Pacing Questions

5. **Where do players voluntarily retreat to safe rooms?** If they retreat during Container Maze, it's too hard. If they never retreat, safe rooms are unnecessary.

6. **Does the Valley production floor's moral weight land, or do players disengage?** Are they reading worker dialogue, or skipping and fighting?

7. **Is the final run (post-Pale-Rift, with integrated build) exciting or exhausting?** Does having access to all four archetypes feel like power, or like cognitive overload?

### Difficulty Questions

8. **What's the average death count per run?** Target: 1-2 deaths on Standard difficulty. If 0, too easy. If 3+, too hard.

9. **Do players feel that psyche shuffle is fair randomness or punishing randomness?** "I got a bad shuffle" is acceptable. "The shuffle system is broken" is not.

10. **Are boss de-escalation options discovered?** Specifically Viktor. If <40% of players attempt dialogue, the option is not telegraphed clearly enough.

### Narrative Questions

11. **When does the meta-case "click"?** At what run number do players realize they're building a larger picture? Target: Run 3-5.

12. **Do players trust the Case Refraction system, or do they think it's random?** If players say "the game just picks a random killer," the psyche-evidence mapping is not clear.

13. **Does the final accusation feel meaningful, or arbitrary?** Post-game survey: "Did your final accusation feel earned?" Target: >75% yes.

---

## IX. BLOCKOUT PRIORITIES

### Phase 1: Core Loop Validation (Weeks 1-2)

**Build**:
- Jamrock precinct office (hub)
- Jamrock hallway (tutorial combat)
- Dockside Approach (first real combat)
- Union Hall (first debrief)

**Test**:
- 30-second loop (enter room, fight, collect, exit)
- 5-minute loop (district -> debrief -> Insight spend)
- Breadcrumbing (do players find Union Hall without UI prompts?)
- Psyche build feel (does Authority FEEL different from Empathy in movement and combat?)

**Success Criteria**: Players complete Jamrock -> Dockside -> Union in 8-12 minutes. 80%+ can do so without getting lost. Psyche builds feel distinct.

---

### Phase 2: Vertical Slice (Weeks 3-6)

**Build**:
- Full Martinaise district (Dockside -> Container Maze -> Whirling-in-Rags)
- Precinct hub with meta-case board (basic functionality)

**Test**:
- Full session loop (run start -> district clear -> debrief -> psyche reshuffle -> next run)
- Boss fight (Memory of Violence)
- Evidence discovery (Room 208)
- Meta-case board (does first thread connection feel revelatory?)

**Success Criteria**: Players complete 3 full runs of Martinaise. Meta-case connections appear by Run 2-3. Boss clear rate >60%. Players report "wanting to run it again."

---

### Phase 3: Full Game Blockout (Weeks 7-12)

**Build**:
- All 5 districts (greybox geometry, placeholder art)
- All boss fights
- Full meta-case board (all 5 layers)

**Test**:
- Full progression (Run 1 -> Run 30+)
- Pacing curve across full game
- Difficulty scaling per district
- Narrative clarity (does Layer 4 revelation land?)

**Success Criteria**: Playtesters complete 10+ runs without churn. Meta-case unlocks at intended run counts. Pale Rift revelation is reported as "emotionally impactful" by >75%.

---

## X. FINAL THOUGHTS — WHERE DOES THE PLAYER LOOK?

Every room in Revachol Nights is designed with a single question at its center:

**What does the player SEE, and what does that seeing TEACH them about who they are?**

Authority sees power structures. Empathy sees pain. Logic sees systems. Electrochemistry sees sensation. The levels do not change. The player changes. And in that change, the case changes. And in that case change, the truth changes.

The level is not a container for the game. The level IS the game. Movement is investigation. Sight lines are evidence. The architecture is the argument.

Where does the player look? Wherever we point the light. And the light changes every time they die and return as someone new.

What's the pacing here? It is the rhythm of understanding: slow at first, then faster, then fractal. The more you see, the more there is to see.

Every room teaches something. And the final room teaches this: you were never solving a murder. You were solving the question of what it means to see the world through a thousand pairs of eyes and still call yourself one person.

The level design is done. The space is ready. Now we find out if the player is brave enough to walk through it and become someone new on the other side.

---

*This document was written by GRID, Level Designer. The levels are not done — they are never done — but the structure is sound, the flow is real, and every sight line has been walked with the player's body in mind. Now we build it. Now we break it. Now we find out what we missed. That's the work. That's always the work.*

--- GRID
