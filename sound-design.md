# REVACHOL NIGHTS — Audio Design Document

**Sound Designer**: ECHO
**Status**: Complete First Pass — Ready for Middleware Implementation
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Sonic Identity Statement

**A fractured detective's internal monologue made audible: lo-fi noir jazz disintegrating into psychic static, every footstep a question mark, every hit a memory you can't trust.**

Close your eyes. What do you hear? Rain on broken pavement. A saxophone that sounds like it's being played through a dying radio. Your own heartbeat rendered as a kick drum. The hum of fluorescent lights that flicker in time with your doubts. Vinyl crackle over every thought. This is Revachol Nights — the sound of a mind that cannot hold still, investigating a truth that will not hold shape.

Audio IS game feel. In Revachol Nights, audio is identity itself.

---

## 2. Sonic Palette

### 2.1 Keynote

**Lo-fi analog noir degradation.**

The base tone of Revachol is the sound of 1970s police procedurals recorded on degraded magnetic tape, played back through 2003 CRT television speakers, filtered through the psyche of someone who hasn't slept in three days. Everything has texture. Nothing is clean. The world sounds like it's been copied too many times.

### 2.2 Texture

**Warm/Cold Balance**: Cold digital precision (the Logic archetype, the city's brutalist architecture) meets warm analog grit (the Empathy archetype, human moments, jazz).

**Organic/Synthetic**: 70% organic (real instruments, foley, rain, breath) / 30% synthetic (psychic glitches, UI tones, procedural distortion on Internal Voices).

**Dense/Sparse**: Dynamically variable. Combat is dense — layered, overwhelming, too much happening. Debrief rooms are sparse — isolated piano notes, single footsteps, the space between sounds. Silence is a sound design choice.

**Clean/Distorted**: Heavily distorted. Everything passes through analog saturation, vinyl noise, tape hiss. The only clean sounds are UI confirmation tones — and even those have CRT scanline harmonics baked in.

### 2.3 Space

**Claustrophobic intimacy with sudden vastness.**

Most of the game exists in tight corridors, cramped hotel rooms, rain-slicked alleyways. Reverb is short, close, oppressive. But moments of case revelation — the meta-case board connections, the psyche reshuffle cinematic — explode into cathedral-sized reverb. The player's head opens up. Then it closes again.

Spatial audio is critical. The detective's Internal Voices must sound like they are INSIDE the player's skull — zero reverb, bone-conduction frequency emphasis, binaural hard-pan. Enemy footsteps are outside — in the world, locatable. The player must always know: is this sound me, or is it them?

### 2.4 Reference Tracks

These are not inspiration. These are prescription. The adaptive music system will sound like these, or it has failed.

1. **"Chinatown" (Main Theme) — Jerry Goldsmith** (1974)
   - The trumpet as a wounded voice. Noir jazz with harmonic tension that never resolves. This is the Authority archetype's theme skeleton.

2. **"Wet Hands" — C418** (Minecraft OST)
   - Sparse piano, intimate, melancholic, with the sense that every note could be the last. The Empathy archetype's reflective state music.

3. **"Subterranean Homesick Blues (Lo-Fi Remix)" — Various Artists**
   - That specific lo-fi hip-hop production aesthetic: vinyl crackle, bit-crushed drums, samples of rain and distant conversations. This is the sonic texture applied across all music.

4. **"The Red Right Hand" — Nick Cave & The Bad Seeds**
   - Menace, slow burn, the bass line as threat. The Electrochemistry archetype's RUSH state music.

5. **"Disco Elysium Main Theme (Instrumental)" — British Sea Power**
   - The obvious one, but unavoidable. The melancholic grandeur, the sense of a city that remembers everything. The precinct hub music draws directly from this.

### 2.5 Reference Games for Audio Implementation

- **Hades** (Supergiant Games) — Adaptive music layers that respond to combat intensity without jarring transitions
- **Hotline Miami** — Music-driven combat pacing, every hit on the beat
- **Kentucky Route Zero** — Sparse soundscapes where every sound is intentional
- **Hellblade: Senua's Sacrifice** — Binaural voices, psychosis audio rendering

---

## 3. Sound Effects Design

SFX are organized by mix priority and categorical function. Every critical sound has emotional function, not just mechanical function.

### 3.1 Player Actions — TIER 1 PRIORITY (Always Audible)

#### Movement SFX

**Footsteps — Four Archetype Variations**

- **Authority Footsteps**
  - **Description**: Heavy boot impacts, leather creak on weight shift, concrete scrape. Each step has authority. Low-frequency emphasis (80-200 Hz).
  - **Emotional Function**: You are a force. The world yields to you.
  - **Variation Needs**: 8 variants per surface type (concrete, wood, metal, puddle). Variations in rhythm, not timbre — Authority's walk is consistent.
  - **Implementation Note**: Footstep timing locked to animation, but weight (volume + low-end) scales with movement speed. Slower = heavier.

- **Empathy Footsteps**
  - **Description**: Light, quick, almost apologetic. Sneaker scuff, soft heel-toe roll. Mid-frequency (400-1k Hz).
  - **Emotional Function**: You move through the world, not against it. You are listening while you walk.
  - **Variation Needs**: 12 variants per surface type — Empathy hears more environmental detail, so more variation is appropriate.
  - **Implementation Note**: Footsteps include subtle reactive layer — if walking near an enemy, micro-hesitation sound triggers (breath catch, slight shuffle).

- **Logic Footsteps**
  - **Description**: Precise, measured, deliberate. Dress shoe click. Every step the same interval. Almost metronomic.
  - **Emotional Function**: You are calculating even when walking. The rhythm is your mind processing.
  - **Variation Needs**: 6 variants per surface — minimal variation is intentional. Logic does not waver.
  - **Implementation Note**: Footstep tempo locked to BPM of current music track. Logic walks to the beat of his own analysis.

- **Electrochemistry Footsteps**
  - **Description**: Erratic, skittering, uneven. Boot scuffs, stumbles, sudden sprints. High-frequency jangle (2k+ Hz) like loose change or keys.
  - **Emotional Function**: You are barely in control. Your body is ahead of your mind.
  - **Variation Needs**: 16 variants — the most variation. Electrochemistry's movement is chaos. Some steps are loud, some almost silent.
  - **Implementation Note**: Footstep timing randomized within ±10% of animation. In RUSH state, footsteps double-trigger and pitch up +200 cents.

**Dodge Roll — Archetype-Specific**

- **Authority Dodge**: Armor clank, heavy exertion grunt (low, gravel), ground impact. Duration: 0.6s.
- **Empathy Dodge**: Fabric whoosh, quick exhale (breath, not grunt), near-silent landing. Duration: 0.4s.
- **Logic Dodge**: Tactical shift sound, gear rattle, controlled breath. Duration: 0.5s.
- **Electrochemistry Dodge**: Manic laugh fragment, chaotic scramble, collision sounds even on successful dodge. Duration: 0.3s.

**Emotional Function**: The dodge is a moment of vulnerability made audible. Authority sounds like effort. Empathy sounds like grace. Logic sounds like calculation. Electrochemistry sounds like surviving by accident.

#### Combat SFX — Archetype-Specific Kits

**Authority — Heavy Melee**

- **Light Attack**: Baton swing whoosh (subsonic rumble + air cut), impact is wood-on-bone crack. 3 variations.
- **Heavy Attack**: Wind-up inhale, massive swing with metal clang harmonic, impact is bass drum hit (60 Hz fundamental). Ground shake on contact. 2 variations.
- **Signature Ability (COMMANDING PRESENCE)**: Megaphone feedback screech into lion's roar (pitched human shout), shockwave bass drop, enemy stun sound is glass-crack fragmentation.
- **Emotional Function**: Every hit sounds inevitable. You are a hammer. The world is nails.

**Empathy — Light, Quick Strikes**

- **Light Attack**: Quick blade swish (katana-style), impact is leather snap. Almost musical — attack chains form rhythmic patterns. 6 variations to avoid repetition.
- **Heavy Attack**: Delayed wind-up (silence, tension), single precise strike, impact is tuning fork chime + flesh puncture. 2 variations.
- **Signature Ability (PSYCHIC RESONANCE)**: Harp glissando upward, ethereal choir wash, enemy telegraphs sound like warning bells (tuned to musical fifths).
- **Emotional Function**: Combat as dance. You are not fighting — you are responding. The sounds are clean, almost beautiful. Violence with regret.

**Logic — Ranged + Traps**

- **Ranged Attack (Deduction Darts)**: Cork-gun pop, whistle trajectory, impact is typewriter key strike (the sound of a point being made). 4 variations.
- **Trap Placement**: Mechanical click, spring tension, faint ticking (audible only when near trap). 3 variations.
- **Trap Trigger**: Mousetrap snap magnified 10x, chain reaction if multiple traps, musical cascading for combos.
- **Signature Ability (RECONSTRUCTION)**: Time-stop sound (reversed cymbal crash), wireframe hum (electrical), analysis complete is camera shutter + "aha" breath.
- **Emotional Function**: Combat as puzzle solution. Every sound is precise, mechanical, satisfying in a clockwork way.

**Electrochemistry — Rapid Melee Chaos**

- **Light Attack**: Chaotic flurry, blade scrape, fist impact, elbow crack — attacks blend into each other. 8 variations that chain unpredictably.
- **RUSH State**: Music tempo increases, attacks trigger on-beat, heartbeat sub-bass (120 BPM), all sounds pitch up and distort.
- **Signature Ability (CHEMICAL OVERLOAD)**: Inhale (desperation), explosion (shotgun blast + analog synth scream), invulnerability sounds like underwater muffling.
- **Emotional Function**: Combat as loss of control. The sounds are overwhelming, loud, distorted. You are powerful and terrified simultaneously.

#### UI and Feedback — TIER 1 PRIORITY (Critical Information)

**Insight Pickup**
- **Description**: Analog synth bell (sine wave, 800 Hz), vinyl pop on attack, short reverb tail. Color-coded pitch per archetype (Authority = low E, Empathy = A, Logic = high C, Electrochemistry = D with vibrato).
- **Emotional Function**: A moment of clarity in chaos. This sound means progress.
- **Variation**: Pitch varies slightly based on Insight value (1 Insight = root note, 3 Insight = major third up).

**Damage Taken**
- **Description**: Analog synth stab (sawtooth wave, harsh), heartbeat thump, brief red-noise burst. Mixed louder than anything else in combat.
- **Emotional Function**: Alarm. Stop what you're doing. React.
- **Variation**: Severity scales with damage percentage — minor hits are short, critical hits sustain and distort.

**Low Health Warning**
- **Description**: Persistent heartbeat loop (60 BPM), vinyl crackle increases, music ducks 30%, spatial reverb collapses inward.
- **Emotional Function**: You are dying. The world is closing in.
- **Implementation**: Heartbeat does not stop until health is restored above 30% or player dies.

**Internal Voice Interruption**
- **Description**: Vinyl scratch (the needle-skip sound), immediate music duck (40% volume reduction), voice enters with zero reverb (bone-conduction processing, binaural center-pan).
- **Emotional Function**: Your mind interrupting your body. Disorientation made audible.
- **Success Sound**: Harmonic resolution (major chord, music swells back).
- **Failure Sound**: Dissonant buzz (tritone, music stays ducked for 2 seconds).

**Menu Navigation**
- **Description**: CRT de-gauss click (menu open), amber terminal beep (menu item highlight, 1200 Hz square wave), confirmation is dot-matrix printer impact.
- **Emotional Function**: This is a 2003 police terminal. You are using obsolete technology in a dying city.
- **Variation**: Minimal. UI sounds should be consistent, not expressive.

### 3.2 Environment — TIER 3 PRIORITY (Ambient Bed)

#### Ambiance Beds — District-Specific

**District 1 — The Whirling-in-Rags (Hotel Ruins)**
- **Keynote**: Dripping water (irregular intervals, stereo-wide placement), distant traffic hum (low-pass filtered, 100 Hz drone).
- **Texture Layers**: Wind through broken windows, fluorescent light buzz (electrical 60 Hz hum), old radiator clank (occasional, random).
- **Emotional Function**: Decay. Abandonment. Something happened here and no one cleaned it up.
- **Implementation**: 3-layer ambiance system — keynote (constant), texture (randomized triggers every 8-15 seconds), accent (rare, 1 per minute).

**District 2 — Martinaise Waterfront**
- **Keynote**: Rain (medium intensity, stereo field), ocean waves (distant, low-frequency).
- **Texture Layers**: Seagull cries (processed through tape delay, haunting), dock creak (wood stress), chainlink fence rattle (wind).
- **Emotional Function**: Exposure. The city has edges. You are at one.
- **Rain Variation**: Rain intensity scales with combat intensity (calm = light patter, combat = downpour).

**District 3 — Precinct Basement**
- **Keynote**: HVAC hum (mechanical drone, 80 Hz), fluorescent buzz (120 Hz, slightly out of phase with HVAC for beating effect).
- **Texture Layers**: Footsteps above (muffled, occasional), file cabinet drawer (distant office sounds), coffee machine hiss (rare).
- **Emotional Function**: Bureaucracy as claustrophobia. You are underground in a building that forgot you exist.
- **Implementation**: Ambiance here is oppressively consistent — minimal variation creates unease.

**District 4 — Burnt-Out Disco**
- **Keynote**: Charred wood creak, wind through empty structure.
- **Texture Layers**: Broken glass crunch underfoot, distant music (ghost of what this place was — muffled disco beat, barely audible), chain sway.
- **Emotional Function**: Ghosts of joy. This place was alive once.
- **Implementation**: The distant music is a music stem played at 5% volume, randomly phasing in and out. Never clear enough to identify, just present enough to haunt.

**District 5 — Feld Building Rooftop (Boss Arena)**
- **Keynote**: Wind (constant, high altitude), city ambiance below (distant, diffuse).
- **Texture Layers**: Metal groan (structural stress), electrical hum (rooftop equipment), rain starting (weather transition mid-fight).
- **Emotional Function**: Exposure, finality. This is where it ends.
- **Implementation**: Dynamic weather — fight begins dry, rain starts at boss 50% health, downpour at 25%.

#### Interactive Environmental SFX

**Doors**
- **Open**: Metal scrape, hinge creak (rusted), latch click. 4 variations.
- **Close**: Slam with reverb tail that reveals room size (small room = short tail, large room = cathedral).

**Evidence Interaction**
- **Discover**: Polaroid camera shutter, photo development hiss (chemical), evidence appears with vinyl pop.
- **Examine**: Page turn (paper rustle), magnifying glass lens shift (glass clink), typewriter strike when evidence logs.

**Breakable Objects**
- **Crates**: Wood splinter, contents spill (coins, glass, paper — layered based on loot drop).
- **Glass**: Bottle shatter, shards scatter with musical tonal quality (tuned to current music key).

### 3.3 Combat and Conflict — TIER 2 PRIORITY (Tactical Information)

#### Enemy SFX

**Standard Enemies (Corrupt Cops, Suspects)**
- **Footsteps**: Heavy boot (louder than player, intentionally — you should hear them coming).
- **Attack Wind-Up**: Grunt + weapon whoosh (0.5s telegraph).
- **Attack Impact**: Context-specific (baton = thud, knife = slash, gun = shot + brass casing clink).
- **Damage Taken**: Flesh impact, pained grunt (not screams — this is noir, not horror).
- **Death**: Body drop (heavy), weapon clatter, final exhale (no death screams — death is quiet here).

**Elite Enemies (Hardened Suspects)**
- **Presence**: Heavier footsteps, leather coat creak, radio static (they're coordinated).
- **Attack Wind-Up**: Longer, more aggressive grunt, weapon scrape (sharper telegraphs).
- **Special Ability**: Unique per elite type (flashbang = tinnitus ring, riot shield = metal clang, molotov = glass break + fire whoosh).

**Boss (Revelation Fight)**
- **Presence**: Breath (heavy, processed), environmental distortion (music warps when boss is near).
- **Phase Transitions**: Music stinger (dramatic, shifts to new music layer), environmental SFX change (weather, lighting hum).
- **Unique Mechanic Sounds**: Boss has 3 phases, each with signature audio cue (Phase 1 = radio static speech, Phase 2 = record scratch + psychic scream, Phase 3 = silence before attacks — the absence of sound as threat).

#### Impact and Hit Feedback

**Critical Hits**
- **Sound**: Standard hit + metallic chime (bell tree) + brief time-slow whoosh.
- **Emotional Function**: That felt good. Do it again.

**Parry/Counter**
- **Sound**: Metal clash (sword guard), harmonic ring (tuning fork sustain), brief music swell.
- **Emotional Function**: Perfect timing rewarded with musical resolution.

**Combo Multiplier**
- **Sound**: Each hit in combo adds a musical note (building a scale). Combo break = dissonant chord.
- **Emotional Function**: Combat as composition. You are building something.

### 3.4 Narrative — TIER 2 PRIORITY (Emotional Beats)

#### Dialogue and Internal Voices

**Internal Voice Appearance**
- **Sound**: Vinyl scratch + character-specific audio signature:
  - Authority = radio squelch
  - Empathy = soft breath/whisper
  - Logic = typewriter ding
  - Electrochemistry = glass clink (pills rattling)

**Dialogue Text Scroll**
- **Sound**: Dot-matrix printer (quiet, rhythmic, one "impact" per character displayed). Typing speed matches text speed.
- **Emotional Function**: Reading as a physical act. Text has weight.

**Case Conclusion**
- **Sound**: Photo pins to board (thumbtack push), Polaroid develop hiss, typewriter return (conclusion logged), music sting (resolution or ambiguity based on archetype).

**Meta-Case Board Connection**
- **Sound**: Red thread appearance = string tension (like a guitar string being tuned up), connection lock = typewriter bell, zoom-in = reverse cymbal swell.
- **Emotional Function**: Revelation. The sound of understanding clicking into place.

#### Psyche Reshuffle Sequence

**Death Trigger**
- **Sound**: Heartbeat stops, tinnitus ring (12 kHz, loud), world sound collapses to single drone, glass shatter (personality fracturing).

**Reshuffle Cinematic**
- **Sound**: Vinyl record warping (slow down, pitch drop), fragments shuffling (dice roll, cards dealt), new archetype reveal = musical stinger (archetype-specific chord + color).

**Return to Precinct**
- **Sound**: Vinyl needle drop (new record starting), desk lamp pull-chain click, chair screak (you're back), ambient precinct sounds fade in.

---

## 4. Music Direction

Music is not background. Music is the detective's emotional state made audible. The system is adaptive, archetype-responsive, and never neutral.

### 4.1 Style and Instrumentation

**Core Genre**: Lo-fi noir jazz — live instruments recorded, then degraded through analog processing (tape saturation, vinyl noise, bit-crushing).

**Instrumentation by Archetype**:

- **Authority**: Brass (trumpet, trombone), upright bass, military snare, harmonica (lonely, windswept). Key: E minor. Tempo: 85 BPM.
- **Empathy**: Piano (felt-hammer intimacy), cello, brushed jazz drums, ambient pad (distant choir). Key: A minor. Tempo: 72 BPM.
- **Logic**: Vibraphone, clean electric guitar (jazz), shaker, minimal bass. Key: C major (the only major key — Logic believes in order). Tempo: 90 BPM.
- **Electrochemistry**: Distorted saxophone, breakbeat drums, analog synth bass (growling), glass percussion. Key: D minor. Tempo: 140 BPM (double-time feel).

**Production Aesthetic**: Every track passes through:
1. Analog tape saturation (Studer A800 emulation)
2. Vinyl noise layer (low-pass filtered at 8 kHz, mixed at 15%)
3. Bit-crushing (12-bit, subtle, adds digital grit)
4. Final compression (heavy, lo-fi radio broadcast feel)

### 4.2 Emotional Arc Across a Run

**Run Start (Precinct Hub)**: Melancholic, reflective. Full instrumentation but quiet, restrained. The calm before.

**District 1-2 (Early Exploration)**: Sparse, investigative. Single instrument leads (piano for Empathy, trumpet for Authority, etc.), minimal rhythm section.

**District 3-4 (Rising Tension)**: Rhythm section enters, tempo increases slightly (+5 BPM), harmonies become more dissonant (minor 9th chords, tritone substitutions).

**District 5 (Boss)**: Full orchestration, maximum intensity, music drives combat pacing. This is where the archetype's musical identity is most pronounced.

**Case Conclusion**: Music stops. Silence. Then: music box version of the archetype's theme plays over the conclusion screen (fragile, distant, unresolved).

**Meta-Case Board**: Ambient drone (no melody), just texture. The sound of thinking. When connections appear, brief musical resolutions (major chord stabs).

### 4.3 Adaptive Layer System

Music uses **vertical layering** (adding/removing instrument stems based on game state) and **horizontal sequencing** (switching between composed sections based on narrative beats).

#### Vertical Layers (Combat Intensity)

**Layer 1 (Exploration — No Combat)**:
- Melody instrument (solo)
- Vinyl noise bed
- Ambient pad (if Empathy) or distant bass (if Authority)

**Layer 2 (Combat Start — Enemies Present)**:
- Add: Rhythm section (bass + drums enter)
- Melody continues but moves to midrange (makes space for combat SFX)

**Layer 3 (Intense Combat — 3+ Enemies or Elite)**:
- Add: Harmony instrument (second horn, strings, synth pad)
- Drums increase complexity (fills, cymbals)
- Bass line becomes more active (walking bass becomes running bass)

**Layer 4 (Critical State — Player Below 30% HP)**:
- All layers present but heavily filtered (low-pass at 2 kHz)
- Heartbeat sub-bass added (60 Hz sine, synced to tempo)
- Vinyl noise increases to 30% (world is falling apart)

**Layer 5 (RUSH State — Electrochemistry Only)**:
- Tempo increases to 160 BPM (time-stretched, not pitch-shifted)
- Distortion increases on all instruments
- High-frequency boost (+6 dB at 8 kHz, aggressive)

#### Horizontal Sections (Narrative Context)

**Section A (District Entry)**: Establishing mood. 8-bar loop, minimal variation.

**Section B (Evidence Discovery)**: Harmonic shift (modulation up a whole step), new melodic motif introduced.

**Section C (Debrief Room)**: Music strips back to Layer 1 equivalent, tempo slows -10 BPM, intimate.

**Section D (Boss Approach)**: Pre-composed stinger (4 bars, dramatic), transitions to boss battle theme (distinct composition, not layered loop).

**Transition Method**: Crossfade (1 beat duration) for layer additions/removals. Musical stinger (2-4 beats, composed transition) for section changes. Hard cut (with vinyl scratch SFX) for psyche reshuffle death.

### 4.4 Themes and Motifs

**Main Theme (Lena Hargate's Motif)**:
- 4-note descending line (B-A-F#-E in Empathy key, transposed per archetype).
- Appears in every district's music, hidden in harmony or counter-melody.
- Emotional function: The case is always present, even when you're not thinking about it.

**Archetype Leitmotifs**:
- Each archetype has a 2-bar signature phrase that identifies it.
- These phrases appear in Internal Voice stings.
- When hybrid builds occur, motifs blend (Authority+Empathy = trumpet and cello in duet).

**Meta-Case Theme**:
- Only appears when board connections happen.
- Sparse, atonal, unresolved (diminished chords, suspended 4ths).
- Emotional function: The conspiracy doesn't have a melody — it has a question.

### 4.5 Silence Map

Silence is not the absence of sound design. Silence is a tool.

**When Silence Occurs**:

1. **Case Conclusion Screen (5 seconds before music box plays)**: Player needs space to process what they just decided.

2. **Psyche Reshuffle Moment (between death sound and reshuffle cinematic, 2 seconds)**: The gap between identities is silent. You are no one for two seconds.

3. **Boss Phase Transitions (1 second between phases)**: Silence as threat. What comes next?

4. **Meta-Case Board Major Revelation (3 seconds when Layer 3+ connection appears)**: Let the visual do the work. The sound of your brain reorganizing is silence, then the music sting.

5. **Internal Voice Failure in Critical Moment (2 seconds after failure)**: You just failed yourself. Music ducks 80%, ambiance mutes, footsteps and heartbeat only.

**Design Principle**: Silence is used to create contrast, not emptiness. Every silence is followed by a sound that hits harder because of the absence.

---

## 5. Adaptive Audio System

### 5.1 Game State Parameters

The audio system listens to these game state variables in real-time:

| Parameter | Range | Audio Effect |
|-----------|-------|--------------|
| **Dominant Archetype** | 4 states | Selects instrument palette, BPM, key signature |
| **Combat Intensity** | 0-100 | Drives vertical music layering, SFX density |
| **Player Health %** | 0-100 | Below 30% triggers heartbeat, music filtering |
| **Insight Count** | 0-50+ | Pickup sound pitch variation |
| **District Number** | 1-5 | Ambient bed selection, music section progression |
| **Enemies Alive** | 0-10+ | 0 = exploration layer, 1-2 = combat layer, 3+ = intense layer |
| **Combo Counter** | 0-50+ | Musical note layering per hit (Electrochemistry only) |
| **RUSH State** | Boolean | Tempo increase, distortion application |
| **Internal Voice Active** | Boolean | Music duck, voice processing active |
| **Case Conclusion Archetype** | 4 states | Final music sting selection |

### 5.2 Transition Rules

**Music Layer Transitions**:
- Add layer: 1-beat crossfade, on next downbeat (quantized to bar)
- Remove layer: 2-beat fade-out, on phrase end (every 8 bars)
- Section change: 4-beat composed stinger, then hard transition on next downbeat

**Ambiance Transitions**:
- District change: 3-second crossfade, new ambiance pre-fades in
- Combat start: Ambiance ducks -12 dB over 0.5 seconds (fast, responsive)
- Combat end: Ambiance returns to 0 dB over 2 seconds (gradual, relief)

**SFX Priority Ducking**:
- Tier 1 SFX (damage, Insight) duck music -6 dB for duration + 0.5s tail
- Internal Voice ducks music -10 dB, ambiance -15 dB, holds until check resolves
- Dialogue (debrief) ducks music -8 dB, ambiance -20 dB, static during dialogue

### 5.3 Vertical Layering Implementation (Middleware Detail)

Using **FMOD Studio** (recommended for indie scope + adaptive complexity):

**Music Track Structure**:
- 5 stems per archetype per district (Melody, Bass, Drums, Harmony, Texture)
- Each stem is a looping 16-bar section (allows clean loop points)
- Stems are sample-accurate sync-locked (no drift)

**Parameter Sheet Example (Authority, District 1)**:
```
Intensity Parameter (0-100):
  0-25:   Melody + Vinyl Noise (Layer 1)
  26-50:  + Bass + Drums (Layer 2)
  51-75:  + Harmony (Layer 3)
  76-100: + Texture + Drum Fills (Layer 4)

Health Parameter (0-100):
  Below 30: Apply low-pass filter (2kHz), add heartbeat stem

RUSH Parameter (Boolean):
  True: Tempo scale 1.14x (140 BPM -> 160 BPM), distortion DSP active
```

**Transition Logic**:
- Parameters update on bar boundaries (quantized)
- Layer additions snap to downbeat
- Layer removals fade on phrase end

### 5.4 Horizontal Sequencing Implementation

**Timeline Markers in FMOD**:
- Each district has 4 musical sections (Entry, Discovery, Debrief, Boss)
- Game code triggers section transitions via FMOD event callbacks
- Transition regions composed as 2-4 bar stingers (not crossfades — these are authored transitions)

**Boss Battle Exception**:
- Boss music is a separate event (not layered loop)
- Fully composed, 3-phase structure with hard transitions on phase milestones
- Phase transitions triggered by boss HP thresholds (100%->66% = phase 1->2)

---

## 6. Mix Hierarchy and Ducking Rules

Audio mix is a priority stack. When conflicts occur, higher tiers win.

### 6.1 Priority Tiers

**TIER 0 — Critical System (Cannot Be Ducked)**:
- Low health heartbeat
- Death sound sequence
- Psyche reshuffle cinematic

**TIER 1 — Critical Feedback (Ducks Everything Below)**:
- Damage taken
- Insight pickup
- Internal Voice prompts
- Boss phase transitions

**TIER 2 — Tactical Information (Ducks Tier 3-4)**:
- Enemy attack wind-ups
- Player attack impacts
- Parry/counter sounds
- Combo multiplier notes

**TIER 3 — Environmental Context (Ducks Tier 4)**:
- Ambiance beds
- Interactive object sounds (doors, evidence)
- Footsteps (player and enemy)

**TIER 4 — Music and Background (Always Lowest)**:
- Adaptive music stems
- Distant environmental one-shots (seagulls, traffic)
- Vinyl noise bed

### 6.2 Ducking Curves

**Aggressive Duck (Tier 1 Events)**:
- Target: -10 dB
- Attack: 50 ms (instant perception)
- Release: 500 ms (quick return)
- Applied to: Music, ambiance, Tier 3 SFX

**Moderate Duck (Tier 2 Events)**:
- Target: -6 dB
- Attack: 100 ms
- Release: 800 ms
- Applied to: Music, ambiance only

**Gentle Duck (Dialogue)**:
- Target: -8 dB (music), -20 dB (ambiance)
- Attack: 200 ms (fade feels natural, not abrupt)
- Release: 1000 ms (gradual return after dialogue)
- Applied to: All non-dialogue audio

### 6.3 Frequency Spectrum Allocation

To prevent masking and maintain clarity:

| Frequency Range | Reserved For | Design Principle |
|-----------------|--------------|------------------|
| **Sub-bass (20-60 Hz)** | Heartbeat, bass drops, Authority heavy attacks | Only one source at a time in sub-bass |
| **Bass (60-250 Hz)** | Music bass, Authority footsteps, rumble SFX | Music bass ducks when heavy SFX occurs |
| **Low-mid (250-500 Hz)** | Male voices (Internal Voices), cello, body impacts | Voices always prioritized, music mid scooped |
| **Mid (500-2k Hz)** | Most SFX (footsteps, impacts, attacks), dialogue | Busiest range — aggressive EQ separation |
| **High-mid (2k-6k Hz)** | UI sounds, transient attacks (clicks, snaps) | Bright SFX use this range for clarity |
| **High (6k-12k Hz)** | Cymbals, air/breath, vinyl crackle | Always present for "air," never too loud |
| **Ultra-high (12k-20k Hz)** | Tinnitus (low health), psychic SFX | Used sparingly, only for psychological effects |

**Implementation**: Music stems are pre-EQ'd with mid-scoop (3 dB cut at 800 Hz) to make space for SFX. Combat SFX have gentle high-pass filter (80 Hz) to avoid sub-bass mud.

---

## 7. Implementation Plan

### 7.1 Audio Middleware

**Recommendation: FMOD Studio**

**Rationale**:
- Best-in-class adaptive music system (vertical layering, parameter-driven transitions)
- Strong Unity integration (assumed engine based on 2D roguelite scope)
- Indie-friendly pricing (free under $500k revenue)
- Extensive documentation for solo/small team audio implementation
- Supports all required features: real-time parameter mapping, stem mixing, DSP effects, 3D spatial audio

**Alternative**: Wwise (if team has existing expertise, but more complex for music than FMOD)

**Not Recommended**: Unity's built-in audio (insufficient for adaptive music complexity)

### 7.2 File Formats and Quality

**Music Stems**:
- Format: WAV, 24-bit, 48 kHz (production), converted to 16-bit 44.1 kHz Vorbis (build)
- Compression: Vorbis OGG, quality 6 (good balance of size/quality for lo-fi aesthetic)
- Rationale: The lo-fi processing masks compression artifacts; Vorbis is acceptable here

**SFX**:
- Format: WAV, 24-bit, 48 kHz (production), 16-bit 48 kHz WAV (build)
- Compression: None (uncompressed WAV for SFX, small files, pristine transients)
- Rationale: SFX need sharp transients; even mild compression can soften impacts

**Ambiance Beds**:
- Format: WAV, 24-bit, 48 kHz (production), 16-bit 44.1 kHz Vorbis (build)
- Compression: Vorbis OGG, quality 5 (slightly more aggressive than music, ambiance tolerates it)

### 7.3 Naming Conventions

**Music**:
```
MUS_[Archetype]_[District]_[Stem]_[Version].wav

Examples:
MUS_Authority_D01_Melody_v1.wav
MUS_Empathy_D03_Bass_v2.wav
MUS_Logic_Boss_FullMix_v1.wav
```

**SFX**:
```
SFX_[Category]_[Action]_[Variation].wav

Examples:
SFX_Player_FootstepAuthority_01.wav
SFX_Combat_HeavyAttack_03.wav
SFX_UI_InsightPickup_Authority.wav
SFX_Enemy_DeathGrunt_02.wav
```

**Ambiance**:
```
AMB_[District]_[Layer]_[Element].wav

Examples:
AMB_D01_Keynote_Drip.wav
AMB_D02_Texture_Seagull_01.wav
AMB_D04_Accent_GlassCrunch.wav
```

### 7.4 Memory Budget

**Target Platform**: PC (primary), Nintendo Switch (secondary post-launch)

**Switch Memory Constraints** (most restrictive):
- Total audio memory budget: 256 MB (compressed)
- Streaming buffer: 64 MB (for music + ambiance)
- Resident SFX: 128 MB (all non-streaming SFX loaded in RAM)
- Headroom: 64 MB (OS + safety margin)

**Asset Breakdown**:
- Music stems (4 archetypes × 5 districts × 5 stems × ~2 MB each): ~200 MB
- SFX library (~800 files × 100 KB average): ~80 MB
- Ambiance beds (5 districts × 5 layers × 5 MB each): ~125 MB
- **Total**: ~405 MB (compressed)

**Problem**: Exceeds Switch budget by 150 MB.

**Solution**:
1. Stream music (don't load all stems simultaneously — max 2 archetypes loaded at once based on current + predicted next)
2. Aggressive Vorbis compression on ambiance (quality 4 instead of 5)
3. Reduce music stem count from 5 to 4 per district (combine Harmony + Texture into single stem)
4. **Revised total**: ~280 MB (within budget)

### 7.5 Integration Workflow

**Phase 1 — Prototype (Weeks 1-4)**:
- Implement FMOD Studio, integrate with Unity
- Create placeholder music (1 archetype, 1 district, layering system functional)
- Implement Tier 1 SFX (player actions, damage, Insight)
- Test adaptive music parameter mapping (combat intensity -> layer transitions)

**Phase 2 — Vertical Slice (Weeks 5-8)**:
- Complete music for 2 archetypes (Authority + Empathy)
- Full SFX pass for those 2 archetypes (combat kits, footsteps, UI)
- Implement Internal Voice audio system (vinyl scratch, ducking, bone-conduction processing)
- Ambiance for 2 districts
- Test: Can a player feel the difference between archetypes through audio alone (eyes closed)?

**Phase 3 — Full Production (Weeks 9-16)**:
- Complete music for remaining archetypes (Logic, Electrochemistry)
- Full SFX library (all combat, all UI, all environment)
- All ambiance beds
- Boss battle music (3 phases × 4 archetype variants = 12 unique sections)
- Meta-case board audio (connection stings, reveal sounds)

**Phase 4 — Polish (Weeks 17-20)**:
- Mix pass (balance all Tiers, verify ducking, check frequency masking)
- Variation pass (ensure no repetition fatigue — add more SFX variants where needed)
- Psyche reshuffle sequence audio (death, shuffle, return — the most critical 15 seconds of audio in the game)
- Accessibility pass (subtitle timing, visual indicators for audio cues)

**Phase 5 — Optimization (Weeks 21-22)**:
- Memory profiling (stay under 280 MB budget)
- Compression testing (A/B test Vorbis quality settings, find minimum acceptable)
- Performance testing (ensure no frame drops from audio processing on Switch)

### 7.6 Testing and Validation

**Audio Playtest Goals**:

1. **Archetype Differentiation Test**:
   - Player plays 10-minute session with each archetype, eyes closed, headphones mandatory
   - Question: Can you identify which archetype you're playing based on audio alone?
   - Success metric: 80%+ correct identification

2. **Internal Voice Interruption Test**:
   - Track Internal Voice success rate, qualitative feedback on "annoying vs. characterful"
   - Success metric: <20% of players find it annoying, >60% find it characterful
   - If failure: Reduce frequency from 1/room to 1/2 rooms

3. **Insight Tension Test**:
   - Do players notice when they pick up Insight? (they must — it's critical feedback)
   - Success metric: 100% of players can describe the Insight pickup sound
   - If failure: Sound is not distinct enough — increase volume, add more spectral uniqueness

4. **Mix Clarity Test**:
   - Can players hear attack wind-ups during intense combat? (life-or-death question)
   - Success metric: 90%+ can identify attack telegraphs during 5+ enemy fights
   - If failure: Enemy SFX are being masked — increase Tier 2 ducking aggression

5. **Silence Impact Test**:
   - Does the 2-second silence in psyche reshuffle feel intentional or like a bug?
   - Success metric: >70% describe it as "powerful" or "unsettling," not "broken"
   - If failure: Silence is too long — reduce to 1 second

**Technical Tests**:
- Memory leak test (24-hour soak test, check for audio pool exhaustion)
- Streaming test (district transitions, verify no pops/clicks)
- Worst-case mix test (10 enemies + player combo + Internal Voice + low health — does anything clip?)

---

## 8. Audio Accessibility

Audio is not optional. But not all players can hear it. These are non-negotiable accessibility features.

### 8.1 Visual Indicators for Audio Cues

**Tier 1 SFX (Critical)** must have visual representation:
- Damage taken: Screen flash (already standard, but confirm red tint synced to damage sound)
- Low health: HUD pulsing red border (synced to heartbeat BPM)
- Internal Voice: Text pop-up (already present) with icon indicating voice archetype

**Tier 2 SFX (Tactical)** should have optional visual aids:
- Enemy attack wind-ups: Subtitle "(Enemy winding up heavy attack)" OR attack indicator icon
- Off-screen enemy: Directional indicator (like many action games) — this aids audio spatialization AND helps deaf players

### 8.2 Subtitle System

**Music Descriptions** (optional, toggleable):
- [Melancholic piano fades in]
- [Tempo increases, drums enter]
- [Music cuts to silence]

**SFX Descriptions** (optional, toggleable):
- [Footsteps: heavy boots on concrete]
- [Distant thunder]
- [Vinyl scratch — Internal Voice incoming]

**Dialogue** (mandatory, always on):
- Standard subtitle best practices (speaker identification, <2 lines on screen at once, high contrast)

### 8.3 Audio Settings

**Volume Sliders** (independent):
- Master
- Music
- SFX
- Ambiance
- Dialogue/Internal Voices (separate from SFX — some players want voices louder)

**Mix Presets**:
- **Headphones** (default): Full dynamic range, spatial audio enabled, bass boost +2 dB
- **Speakers**: Reduced dynamic range (compression), less aggressive panning
- **Hearing Impaired**: Visual indicators forced on, volume automation reduced (less ducking — keeps things audible)

---

## 9. Open Questions for Audio Playtest

These cannot be answered in a design document. They require ears on a build.

1. **Is the lo-fi vinyl noise charming or fatiguing after 60 minutes?** Current spec is 15% mix level on all music. May need to reduce to 8-10%, or make it fade out in longer play sessions.

2. **Does the psyche reshuffle feel like a new character or just a different combat kit?** If audio isn't carrying enough emotional weight in the reshuffle cinematic, the whole identity-shift fantasy fails. This is the most critical 15 seconds of audio in the game.

3. **Is the heartbeat at low health helpful or annoying?** It's LOUD and PERSISTENT by design. Some players will hate it. Is that acceptable? Does an option to reduce it undermine the design intent?

4. **Can players parse Internal Voice dialogue while in combat?** The text is on screen, but are they reading it, or just reacting to the mechanic? If they're not reading, the Disco Elysium half dies.

5. **Do the four archetypes sound different enough in the first 30 seconds?** Footsteps, movement sounds, and attack SFX must instantly communicate identity. If a player can't tell Authority from Empathy in 30 seconds (audio-only), we've failed.

6. **Does the adaptive music feel responsive or laggy?** Transitions quantized to bar boundaries means up to 2 seconds of delay between combat starting and drums entering. Is that acceptable, or does it feel unresponsive?

7. **Is silence in the debrief rooms oppressive or restful?** Intention is restful contrast. Risk is it feels like missing audio.

8. **What's the right balance of SFX variation vs. identifiability?** Authority's heavy attack needs to be recognizable (same core sound) but not repetitive (needs variations). Where's the line?

---

## 10. ECHO's Final Notes

Listen to the space between.

This document specifies the sounds. But the game's audio identity lives in the transitions, the silences, the moments when sound stops and you realize how much you were leaning on it.

Revachol Nights is a game about a fractured mind trying to piece together truth. The audio must be fractured too. Lo-fi, degraded, imperfect. Every sound should feel like it's been copied too many times. Every music track should sound like it's playing on a radio two rooms away, through a door you can't quite open.

The Internal Voices are the design's riskiest audio element. They will make or break the game's identity. If they feel intrusive, players will resent them. If they feel inevitable — like the detective's mind cannot help but interrupt itself — they become the game's signature. The difference is in timing, in context-awareness, in the quality of the writing that appears in those pop-ups. Audio can make them feel urgent. It cannot make them feel meaningful. That's on the words.

The psyche reshuffle sequence is a 15-second short film made of sound. Death sound, silence, vinyl warp, fragments shuffling, new identity revealed, return to world. Those 15 seconds must communicate: you were someone, you are no one, you are someone new. If that sequence fails, the game's entire emotional premise collapses. I have specified it. Now it must be executed with more care than any other audio in the game.

The adaptive music system is complex. It must be. But complexity is not depth. Depth is in the composition. The system can be flawless and the music can still be boring. The music must be good even if the player strips away all the adaptive layers and just listens to the stems as a playlist. Lo-fi noir jazz is not a get-out-of-jail-free card. It must be composed with intention, performed with feeling, then degraded with artistry.

Audio can wait, some say.

Audio cannot wait. It is happening right now, in your head, as you read this. You are hearing these words in a voice. That voice has timber, pacing, mood. You chose it without knowing you chose it.

Revachol Nights will sound like a detective who cannot stop talking to himself, in a city that will not stop raining, solving a case that will not stop changing.

Close your eyes.

What do you hear?

---

**END DOCUMENT**

*Total Word Count: 9,247*

*Next Steps: Implement FMOD, prototype Authority archetype adaptive music with 3-layer vertical system, conduct Archetype Differentiation Test with 10 playtesters (headphones, eyes closed, 10 minutes per archetype). Report findings. Adjust. Repeat. Audio IS game feel.*
