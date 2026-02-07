# REVACHOL NIGHTS -- Technical Architecture Document

**Author**: BYTE, Lead Programmer
**Status**: Architecture Complete -- Ready for Prototyping
**Version**: 1.0
**Date**: 2026-02-07

---

## 0. Executive Summary

Ship it. Then improve it.

This is the technical architecture for REVACHOL NIGHTS -- a 2D noir detective roguelite where personality is your build. The game demands:
- Frame-perfect combat (Dead Cells responsiveness)
- Complex narrative branching (Disco Elysium-style psyche system)
- Procedural case assembly with authored content
- Cross-run persistence with a meta-case board
- 4 distinct combat archetypes with 24 sub-skills
- 20-40 minute run loops with tight performance

Target: 60 FPS on PC (Steam), 30 FPS minimum on Nintendo Switch. Memory budget: 2GB runtime, 1.5GB on Switch. Development timeline: 18-24 months with a 4-person core team.

This document specifies concrete technologies, data structures, and system architectures. No hand-waving. No "we'll figure it out later." If something could go wrong technically, it's documented with mitigation strategies.

What's the simplest version? That's what this architecture builds.

---

## 1. Engine & Framework Selection

### 1.1 Engine Recommendation: Godot 4.3

**Decision: Use Godot 4.3 as the primary engine.**

**Rationale:**

**Why Godot over Unity/Unreal:**
- **2D-first architecture**: Godot's 2D renderer is purpose-built, not a bolt-on to a 3D engine. Dead Cells-tier responsiveness requires tight control over sprite batching, animation systems, and physics determinism. Godot's `CanvasItem` and `Node2D` systems are clean, predictable, and fast.
- **Open source + export flexibility**: No runtime fees, no license surprises, no Unity-2023-style rug pulls. Critical for an indie roguelite that may sell 10k copies or 500k copies -- we can't predict revenue, so we can't afford revenue-dependent costs.
- **GDScript + C#**: Prototype in GDScript (fast iteration), optimize hot paths in C# or C++ via GDExtension. The psyche system's skill check logic will be GDScript. The combat loop will be C#/GDExtension.
- **Lightweight runtime**: Godot's runtime overhead is minimal. PC export is ~50MB, Switch export is ~30MB. No bloat.
- **Animation system**: `AnimationPlayer` + `AnimationTree` for archetype-specific combat animations. Built-in state machine support for combat state management (idle/attack/dodge/hit/dead).
- **Scene system as prefabs**: `.tscn` files are human-readable, git-friendly, and composable. Each district room is a scene. Each enemy type is a scene. The case board is a scene. Composition over inheritance everywhere.

**Why NOT Unreal**: Unreal's 2D tools are third-class citizens. Blueprints are great for prototyping but become spaghetti at scale. The runtime size for 2D is absurd (200MB+ base). We don't need nanite.

**Why NOT Unity**: Post-2023 trust issues aside, Unity's 2D pipeline is good but not great. The Input System is overcomplicated. The runtime fees model is unstable. Godot's simplicity wins.

**Why NOT custom engine**: I spent 18 months writing an engine that never shipped. Never again. Godot gives us 90% of what we need out of the box. The 10% we write ourselves (case refraction system, psyche build generator) are game-specific, not engine-level.

### 1.2 Language Choice

**Primary: GDScript** (Godot's built-in scripting language)
- Gameplay logic, UI systems, case assembly, narrative trees
- Fast iteration, hot reload, integrated with editor
- Python-like syntax, easy to onboard writers for dialogue scripting

**Secondary: C# via GDExtension** (for performance-critical paths)
- Combat loop (enemy AI, player state machine, hitbox calculations)
- Pathfinding and spatial queries
- Insight economy calculations
- Procedural district generation

**Tertiary: C++ via GDExtension** (if profiling shows bottlenecks)
- Custom tilemap renderer if we need visual effects that Godot's CanvasItem doesn't optimize
- Not expected to be necessary unless we add post-processing shaders per-archetype

**Rationale**: GDScript is fast enough for 95% of the game. The 5% that runs every frame (combat update loop, animation blending, physics queries) will be C#. Profile before optimizing. We start 100% GDScript and rewrite hot paths in C# only after profiling shows the need.

### 1.3 Target Platforms

**Primary: PC (Steam)**
- Windows 10/11, x64
- Linux (Proton-compatible, native export as stretch)
- macOS (Metal renderer, arm64 + x64 universal binary)
- Target specs: GTX 1050 / RX 560 or integrated equivalent, 8GB RAM

**Secondary: Nintendo Switch**
- 30 FPS minimum, 60 FPS target in docked mode
- 720p handheld, 1080p docked
- Memory budget: 1.5GB runtime (Switch OS reserves ~1GB)
- Export via Godot's official Switch SDK (requires Nintendo developer license)

**Tertiary: PlayStation 5 / Xbox Series (post-launch ports)**
- 60 FPS locked, 4K upscale from 1080p native
- DualSense feature support (haptics for Internal Voice triggers)
- Not scoped for v1.0 -- post-launch if PC sales justify it

**Mobile: No.**
- The combat system requires precise input. Touch controls would compromise core feel. Not worth the design dilution.

### 1.4 Build and Export Configuration

**PC Steam**: Godot export template with embedded PCK, x64 binary
**Switch**: Separate dev and release builds, release with NX-specific optimizations
**All platforms**: Mono/.NET runtime bundled for C# scripts

---

## 2. Architecture Overview

### 2.1 High-Level System Diagram (Text)

```
┌────────────────────────────────────────────────────────┐
│                    GAME DIRECTOR                       │
│  (Singleton, manages run lifecycle, scene transitions) │
└──────────────┬─────────────────────────────────────────┘
               │
    ┌──────────┴─────────────┐
    │                        │
┌───▼────────────┐   ┌───────▼───────────┐
│  RUN MANAGER   │   │  PRECINCT HUB     │
│  - Psyche gen  │   │  - Meta-case      │
│  - District    │   │  - Persistence    │
│    sequencing  │   │  - Psyche Echo    │
│  - Death/win   │   │    shop           │
└───┬────────────┘   └───────────────────┘
    │
    ├─────────────────┬──────────────────┬────────────────┐
    │                 │                  │                │
┌───▼──────────┐ ┌───▼─────────┐ ┌─────▼────────┐ ┌─────▼─────────┐
│   PSYCHE     │ │  COMBAT     │ │  CASE        │ │  DIALOGUE     │
│   SYSTEM     │ │  SYSTEM     │ │  REFRACTION  │ │  SYSTEM       │
│              │ │             │ │  ENGINE      │ │               │
│ - Build gen  │ │ - Player    │ │ - Evidence   │ │ - Branching   │
│ - Skill      │ │   state     │ │   nodes      │ │   trees       │
│   checks     │ │ - Enemy AI  │ │ - Archetype  │ │ - Psyche      │
│ - Sub-skill  │ │ - Hitboxes  │ │   filtering  │ │   gating      │
│   activation │ │ - Combat    │ │ - Meta tags  │ │ - Internal    │
│ - Internal   │ │   verbs     │ │              │ │   Voice       │
│   Voices     │ └─────────────┘ └──────────────┘ │   injection   │
└──────────────┘                                   └───────────────┘
    │
    ├──────────────────┬──────────────────┐
    │                  │                  │
┌───▼──────────┐  ┌───▼─────────┐  ┌─────▼────────┐
│  INSIGHT     │  │  DISTRICT   │  │  SAVE        │
│  ECONOMY     │  │  GENERATION │  │  SYSTEM      │
│              │  │             │  │              │
│ - Drop calc  │  │ - Room      │  │ - Run state  │
│ - Spend      │  │   assembly  │  │ - Meta-case  │
│   channels   │  │ - Enemy     │  │   persistence│
│ - Shop UI    │  │   placement │  │ - Archetype  │
└──────────────┘  └─────────────┘  │   history    │
                                    └──────────────┘
```

### 2.2 Component Architecture: Composition Over Inheritance

**Pattern: Entity-Component System (not a full ECS like Bevy, but component-based design in Godot's scene tree)**

Every game object is a `Node2D` scene with attached components. No deep inheritance hierarchies.

**Example: Player Entity**
```
Player (Node2D)
├─ Sprite2D (visual)
├─ AnimationPlayer (animations)
├─ CollisionShape2D (physics body)
├─ PlayerController (script: input handling)
├─ CombatController (script: archetype-specific verbs)
├─ PsycheProfile (script: current build data)
├─ HealthComponent (script: HP, damage, death)
├─ InsightComponent (script: Insight counter, pickup)
├─ InternalVoiceEmitter (script: triggers skill checks)
└─ AudioStreamPlayer2D (sfx)
```

**Example: Enemy Entity**
```
Enemy (Node2D)
├─ Sprite2D
├─ AnimationPlayer
├─ CollisionShape2D
├─ EnemyAI (script: behavior tree)
├─ HealthComponent (reused from player)
├─ LootDropper (script: Insight + Evidence fragments)
└─ AudioStreamPlayer2D
```

**Why this pattern:**
- **Reusability**: `HealthComponent` is the same script for player, enemies, destructible objects. No copy-paste.
- **Testability**: Each component can be unit-tested in isolation. `InsightComponent` doesn't care what node it's attached to.
- **Designer-friendly**: Designers can compose new enemy types by mixing components in the Godot editor without writing code.
- **Debuggability**: Each component has a single responsibility. When combat feels wrong, you look at `CombatController`. When Insight is broken, you look at `InsightComponent`.

### 2.3 Data Flow

```
RUN START
    ↓
[PsycheSystem] generates build → stores in PsycheProfile
    ↓
[DistrictGeneration] queries PsycheProfile → assembles case-relevant rooms
    ↓
[Player] enters room
    ↓
[CombatSystem] updates (enemy AI, player input, hitboxes)
    ↓
[InternalVoiceEmitter] triggers check → [PsycheSystem] validates
    ↓
[Enemy] dies → [LootDropper] spawns Insight + Evidence
    ↓
[Player] collects → [InsightComponent] increments counter
    ↓
[District] cleared → [Debrief UI] presents spend choices
    ↓
[Player] spends Insight → [CombatController] upgrades OR [CaseRefraction] unlocks
    ↓
[Next District] or [Death] or [Case Close]
    ↓
[RunManager] logs results → [SaveSystem] persists to meta-case board
    ↓
[PsycheSystem] reshuffles → RUN START
```

**Key insight**: The PsycheProfile data structure is read by EVERY major system. It is the "source of truth" for a run. If PsycheProfile is corrupted, the entire run is invalid. Therefore: PsycheProfile is immutable after generation. No mid-run edits except through explicit Insight upgrades (which create a new profile version, not mutate the old one).

### 2.4 Core Systems List

1. **Psyche System** — build generation, skill checks, sub-skill activation
2. **Combat System** — player state machine, enemy AI, hitbox/hurtbox, archetype verbs
3. **Case Refraction Engine** — evidence node filtering, case conclusion assembly
4. **Dialogue System** — branching trees, psyche-gated options, Internal Voices
5. **Insight Economy** — drop calculation, spend channels, UI
6. **District Generation** — procedural room assembly (with authored content)
7. **Meta-Case Board** — cross-run persistence, evidence threads, conspiracy layer unlocks
8. **Save System** — run state serialization, meta-case persistence
9. **Animation System** — archetype-specific combat animations, state blending
10. **Audio System** — archetype-reactive music, sfx, Internal Voice audio stings

Each system gets a full specification below.

---

## 3. Core Systems Design

### 3.1 Psyche System

**Responsibilities:**
- Generate psyche builds at run start (4 archetypes, 24 sub-skills)
- Store build data in a runtime-accessible structure
- Validate Internal Voice skill checks
- Provide archetype query API for other systems ("is Authority Tier 2+?")

**Data Structure: PsycheProfile**

```gdscript
class_name PsycheProfile
extends Resource

# Archetype point distribution (sums to 24)
var authority: int = 0
var empathy: int = 0
var logic: int = 0
var electrochemistry: int = 0

# Sub-skill activation flags (6 per archetype, 24 total)
var active_subskills: Dictionary = {
    "intimidation": false,
    "endurance": false,
    "composure": false,
    "volition": false,
    "esprit_de_corps": false,
    "rhetoric": false,
    # ... (18 more, one per sub-skill)
}

# Computed at generation
var dominant_archetype: String = ""  # "authority", "empathy", "logic", "electrochemistry"
var dump_stat: String = ""
var tier_map: Dictionary = {}  # { "authority": 2, "empathy": 1, ... }

# Combat verb unlocks (derived from archetype tiers)
var unlocked_verbs: Array[String] = []
var signature_ability: String = ""

func _init():
    pass

func get_archetype_tier(archetype: String) -> int:
    return tier_map.get(archetype, 0)

func is_subskill_active(subskill_name: String) -> bool:
    return active_subskills.get(subskill_name, false)

func to_dict() -> Dictionary:
    # Serialization for save system
    return {
        "authority": authority,
        "empathy": empathy,
        "logic": logic,
        "electrochemistry": electrochemistry,
        "active_subskills": active_subskills,
        "dominant_archetype": dominant_archetype
    }

static func from_dict(data: Dictionary) -> PsycheProfile:
    var profile = PsycheProfile.new()
    profile.authority = data.authority
    profile.empathy = data.empathy
    profile.logic = data.logic
    profile.electrochemistry = data.electrochemistry
    profile.active_subskills = data.active_subskills
    profile.dominant_archetype = data.dominant_archetype
    profile._compute_derived_stats()
    return profile

func _compute_derived_stats():
    # Tier calculation
    tier_map["authority"] = _points_to_tier(authority)
    tier_map["empathy"] = _points_to_tier(empathy)
    tier_map["logic"] = _points_to_tier(logic)
    tier_map["electrochemistry"] = _points_to_tier(electrochemistry)

    # Unlock verbs based on tiers
    if get_archetype_tier("authority") >= 1:
        unlocked_verbs.append("heavy_strike")
    if get_archetype_tier("authority") >= 2:
        unlocked_verbs.append("crowd_slam")
    if get_archetype_tier("authority") >= 3:
        signature_ability = "commanding_presence"
    # ... repeat for other archetypes

func _points_to_tier(points: int) -> int:
    if points <= 2: return 0
    if points <= 5: return 1
    if points <= 8: return 2
    return 3
```

**Generation Algorithm**

```gdscript
class_name PsycheGenerator
extends Node

const TOTAL_POINTS = 24
const MIN_DOMINANT = 8
const MAX_DOMINANT = 12
const MIN_DUMP = 1
const MAX_DUMP = 3

func generate_build() -> PsycheProfile:
    var profile = PsycheProfile.new()
    var archetypes = ["authority", "empathy", "logic", "electrochemistry"]

    # Shuffle to randomize which archetype is dominant
    archetypes.shuffle()

    var dominant = archetypes[0]
    var dump = archetypes[3]

    # Assign points
    var dominant_points = randi_range(MIN_DOMINANT, MAX_DOMINANT)
    var dump_points = randi_range(MIN_DUMP, MAX_DUMP)
    var remaining = TOTAL_POINTS - dominant_points - dump_points

    # Split remaining between the two middle archetypes
    var mid1_points = randi_range(remaining / 3, remaining * 2 / 3)
    var mid2_points = remaining - mid1_points

    # Assign to profile
    profile.set(dominant, dominant_points)
    profile.set(dump, dump_points)
    profile.set(archetypes[1], mid1_points)
    profile.set(archetypes[2], mid2_points)

    profile.dominant_archetype = dominant
    profile.dump_stat = dump

    # Activate sub-skills based on thresholds
    _activate_subskills(profile)

    profile._compute_derived_stats()

    return profile

func _activate_subskills(profile: PsycheProfile):
    # Sub-skill activation logic (maps archetype points to sub-skill unlocks)
    # Authority sub-skills
    if profile.authority >= 3:
        profile.active_subskills["intimidation"] = true
        profile.active_subskills["endurance"] = true
    if profile.authority >= 6:
        profile.active_subskills["composure"] = true
        profile.active_subskills["volition"] = true
    if profile.authority >= 9:
        profile.active_subskills["esprit_de_corps"] = true
        profile.active_subskills["rhetoric"] = true

    # ... repeat for empathy, logic, electrochemistry
```

**Internal Voice Skill Checks**

```gdscript
class_name InternalVoiceCheck
extends Node

var psyche_profile: PsycheProfile
var check_result: bool = false

func trigger_check(subskill_name: String, difficulty: int) -> bool:
    # Difficulty: 0 = easy, 1 = medium, 2 = hard
    var is_active = psyche_profile.is_subskill_active(subskill_name)

    if not is_active:
        # Auto-fail if sub-skill not active
        check_result = false
        return false

    # Roll a check (for now, simple random with archetype bonus)
    var roll = randi_range(1, 20)
    var archetype_bonus = _get_archetype_bonus_for_subskill(subskill_name)
    var threshold = 10 + (difficulty * 3) - archetype_bonus

    check_result = roll >= threshold
    return check_result

func _get_archetype_bonus_for_subskill(subskill_name: String) -> int:
    # Map sub-skills to their parent archetype and return tier bonus
    if subskill_name in ["intimidation", "endurance", "composure", "volition", "esprit_de_corps", "rhetoric"]:
        return psyche_profile.get_archetype_tier("authority") * 2
    # ... repeat for other sub-skills
    return 0
```

**Integration Points:**
- `CombatController` queries `PsycheProfile.unlocked_verbs` to enable attacks
- `CaseRefractionEngine` queries `PsycheProfile.get_archetype_tier()` to filter evidence
- `DialogueSystem` queries `PsycheProfile.is_subskill_active()` to gate dialogue options
- `InternalVoiceEmitter` calls `InternalVoiceCheck.trigger_check()` during combat

**Performance Considerations:**
- `PsycheProfile` is a single resource loaded once per run. All queries are O(1) dictionary lookups.
- Generation happens at run start only (not every frame). No runtime cost.
- Internal Voice checks are rare (1 per room), so even inefficient implementations won't bottleneck.

### 3.2 Combat System

**Responsibilities:**
- Player input handling (movement, attack, dodge, signature ability)
- Archetype-specific combat verbs
- Enemy AI behavior trees
- Hitbox/hurtbox collision detection
- Damage calculation and Health management
- Animation state machine integration

**Player State Machine**

```gdscript
class_name PlayerController
extends Node2D

enum State { IDLE, MOVE, ATTACK, DODGE, HIT, DEAD }

var current_state: State = State.IDLE
var psyche_profile: PsycheProfile
var combat_stats: Dictionary = {
    "move_speed": 200.0,
    "dodge_speed": 400.0,
    "dodge_duration": 0.3,
    "attack_damage": 10,
    "attack_speed": 1.0
}

var velocity: Vector2 = Vector2.ZERO
var is_invulnerable: bool = false

@onready var animation_player: AnimationPlayer = $AnimationPlayer
@onready var health_component: HealthComponent = $HealthComponent
@onready var combat_controller: CombatController = $CombatController

func _ready():
    psyche_profile = RunManager.current_psyche_profile
    combat_controller.initialize(psyche_profile)
    _apply_archetype_modifiers()

func _apply_archetype_modifiers():
    # Modify combat stats based on dominant archetype
    match psyche_profile.dominant_archetype:
        "authority":
            combat_stats.move_speed = 150.0
            combat_stats.dodge_duration = 0.2
            combat_stats.attack_damage = 15
        "empathy":
            combat_stats.move_speed = 250.0
            combat_stats.dodge_duration = 0.5
            combat_stats.attack_damage = 7
        "logic":
            combat_stats.move_speed = 200.0
            combat_stats.attack_damage = 10
        "electrochemistry":
            combat_stats.move_speed = 300.0
            combat_stats.attack_damage = 12
            combat_stats.attack_speed = 1.5

func _physics_process(delta):
    match current_state:
        State.IDLE:
            _handle_idle()
        State.MOVE:
            _handle_movement(delta)
        State.ATTACK:
            _handle_attack()
        State.DODGE:
            _handle_dodge(delta)
        State.HIT:
            _handle_hit()
        State.DEAD:
            pass

func _handle_idle():
    velocity = Vector2.ZERO
    if Input.is_action_pressed("move"):
        current_state = State.MOVE
    if Input.is_action_just_pressed("attack"):
        current_state = State.ATTACK
        combat_controller.execute_attack()
    if Input.is_action_just_pressed("dodge"):
        current_state = State.DODGE
        _start_dodge()

func _handle_movement(delta):
    var input_dir = Input.get_vector("left", "right", "up", "down")
    velocity = input_dir * combat_stats.move_speed
    position += velocity * delta

    if input_dir == Vector2.ZERO:
        current_state = State.IDLE
    if Input.is_action_just_pressed("attack"):
        current_state = State.ATTACK
        combat_controller.execute_attack()
    if Input.is_action_just_pressed("dodge"):
        current_state = State.DODGE
        _start_dodge()

func _start_dodge():
    is_invulnerable = true
    var dodge_dir = velocity.normalized()
    if dodge_dir == Vector2.ZERO:
        dodge_dir = Vector2(1, 0)  # Default dodge forward
    velocity = dodge_dir * combat_stats.dodge_speed
    get_tree().create_timer(combat_stats.dodge_duration).timeout.connect(_end_dodge)
    animation_player.play("dodge")

func _end_dodge():
    is_invulnerable = false
    current_state = State.IDLE

func _handle_attack():
    velocity = Vector2.ZERO
    # Wait for animation to finish (handled by animation signal)
    pass

func take_damage(amount: int):
    if is_invulnerable:
        return
    health_component.take_damage(amount)
    if health_component.is_alive():
        current_state = State.HIT
        animation_player.play("hit")
        get_tree().create_timer(0.3).timeout.connect(func(): current_state = State.IDLE)
    else:
        current_state = State.DEAD
        _on_death()

func _on_death():
    RunManager.on_player_death()
```

**Combat Verbs (Archetype-Specific)**

```gdscript
class_name CombatController
extends Node

var psyche_profile: PsycheProfile
var unlocked_verbs: Array[String] = []
var current_combo: int = 0

@onready var hitbox: Area2D = $Hitbox

func initialize(profile: PsycheProfile):
    psyche_profile = profile
    unlocked_verbs = profile.unlocked_verbs

func execute_attack():
    if "heavy_strike" in unlocked_verbs:
        _heavy_strike()
    elif "light_strike" in unlocked_verbs:
        _light_strike()
    elif "logic_dart" in unlocked_verbs:
        _logic_dart()
    elif "electro_rush" in unlocked_verbs:
        _electro_rush()

func _heavy_strike():
    # Authority verb: slow, heavy, wide arc
    hitbox.monitoring = true
    hitbox.scale = Vector2(2.0, 2.0)  # Wide arc
    await get_tree().create_timer(0.5).timeout  # Slow attack
    hitbox.monitoring = false
    _check_hitbox_damage(15, "authority")

func _light_strike():
    # Empathy verb: fast, low damage, combo-friendly
    hitbox.monitoring = true
    hitbox.scale = Vector2(1.0, 1.0)
    await get_tree().create_timer(0.2).timeout
    hitbox.monitoring = false
    _check_hitbox_damage(7, "empathy")
    current_combo += 1

func _logic_dart():
    # Logic verb: ranged attack
    var projectile = preload("res://combat/projectiles/logic_dart.tscn").instantiate()
    get_tree().root.add_child(projectile)
    projectile.global_position = global_position
    projectile.direction = get_global_mouse_position() - global_position

func _electro_rush():
    # Electrochemistry verb: rapid melee, combo-scaling
    hitbox.monitoring = true
    await get_tree().create_timer(0.15).timeout
    hitbox.monitoring = false
    var damage = 12 + (current_combo * 2)  # Scales with combo
    _check_hitbox_damage(damage, "electrochemistry")
    current_combo += 1

func _check_hitbox_damage(base_damage: int, archetype: String):
    var bodies = hitbox.get_overlapping_bodies()
    for body in bodies:
        if body.has_node("HealthComponent"):
            var health = body.get_node("HealthComponent")
            health.take_damage(base_damage)
```

**Enemy AI (Behavior Tree Pattern)**

```gdscript
class_name EnemyAI
extends Node

enum Behavior { IDLE, PATROL, CHASE, ATTACK, RETREAT }

var current_behavior: Behavior = Behavior.PATROL
var player: Node2D = null
var patrol_points: Array[Vector2] = []
var current_patrol_index: int = 0
var attack_range: float = 50.0
var chase_range: float = 300.0

@onready var nav_agent: NavigationAgent2D = $NavigationAgent2D
@onready var health_component: HealthComponent = $HealthComponent

func _ready():
    player = get_tree().get_first_node_in_group("player")
    _generate_patrol_points()

func _physics_process(delta):
    match current_behavior:
        Behavior.PATROL:
            _behavior_patrol(delta)
        Behavior.CHASE:
            _behavior_chase(delta)
        Behavior.ATTACK:
            _behavior_attack()
        Behavior.RETREAT:
            _behavior_retreat(delta)

func _behavior_patrol(delta):
    var distance_to_player = global_position.distance_to(player.global_position)
    if distance_to_player < chase_range:
        current_behavior = Behavior.CHASE
        return

    nav_agent.target_position = patrol_points[current_patrol_index]
    if nav_agent.is_navigation_finished():
        current_patrol_index = (current_patrol_index + 1) % patrol_points.size()

func _behavior_chase(delta):
    var distance_to_player = global_position.distance_to(player.global_position)
    if distance_to_player < attack_range:
        current_behavior = Behavior.ATTACK
        return
    if distance_to_player > chase_range * 1.5:
        current_behavior = Behavior.PATROL
        return

    nav_agent.target_position = player.global_position

func _behavior_attack():
    # Execute attack animation and damage
    var damage = 10
    if global_position.distance_to(player.global_position) < attack_range:
        player.take_damage(damage)

    await get_tree().create_timer(1.0).timeout  # Attack cooldown
    current_behavior = Behavior.CHASE

func _behavior_retreat(delta):
    # Low HP behavior
    var retreat_dir = (global_position - player.global_position).normalized()
    position += retreat_dir * 100 * delta

    if health_component.health > health_component.max_health * 0.3:
        current_behavior = Behavior.PATROL
```

**Hitbox/Hurtbox System**

Using Godot's `Area2D` nodes with collision layers:
- **Layer 1**: Player hitboxes (attacks)
- **Layer 2**: Enemy hitboxes (attacks)
- **Layer 3**: Player hurtbox (body)
- **Layer 4**: Enemy hurtboxes (bodies)

```gdscript
# Player hitbox monitors Layer 4 (enemy hurtboxes)
# Enemy hitbox monitors Layer 3 (player hurtbox)
```

**Performance Considerations:**
- Combat update loop runs every physics frame (60 FPS target). Keep per-frame operations minimal.
- Hitbox checks use Godot's built-in spatial hash. No custom collision detection.
- Animation state machine is hardware-accelerated via `AnimationTree`.
- Enemy AI behavior trees are throttled to 10 FPS evaluation (check behavior every 6th frame) for non-aggressive enemies.

**Optimization Strategy:**
- Profile with Godot's built-in profiler. If combat loop exceeds 12ms per frame on target hardware, move enemy AI to C#.
- Spatial hash queries for nearby enemies (only update AI for enemies within camera bounds + margin).

### 3.3 Case Refraction Engine

**Responsibilities:**
- Store authored case content (evidence nodes, case conclusions)
- Filter evidence nodes based on PsycheProfile
- Assemble case conclusions based on accumulated evidence
- Provide evidence visibility API for world/dialogue systems

**Data Structure: Evidence Node**

```gdscript
class_name EvidenceNode
extends Resource

@export var id: String  # "bruises_on_arms"
@export var display_name: String  # "Bruises on Victim's Arms"
@export var description: String  # "Signs of a struggle..."
@export var evidence_type: String  # "physical", "testimonial", "circumstantial", "psychological"

# Psyche requirements (archetype + tier)
@export var required_archetype: String  # "authority", "empathy", "logic", "electrochemistry", or ""
@export var required_tier: int  # 0 = no requirement, 1-3 = tier threshold

# Meta-case tags (for cross-run connections)
@export var meta_tags: Array[String] = []  # ["conspiracy_layer_2", "lena_hargate"]

# Case conclusion links
@export var points_to_conclusion: String  # "conclusion_authority_1"

func is_visible_to_profile(profile: PsycheProfile) -> bool:
    if required_archetype == "":
        return true  # Always visible
    return profile.get_archetype_tier(required_archetype) >= required_tier
```

**Evidence Database**

```gdscript
# res://data/evidence_database.gd
class_name EvidenceDatabase
extends Resource

var evidence_nodes: Dictionary = {}  # { "id": EvidenceNode }

func _init():
    _load_evidence_from_json()

func _load_evidence_from_json():
    var file = FileAccess.open("res://data/evidence_nodes.json", FileAccess.READ)
    var json_data = JSON.parse_string(file.get_as_text())

    for evidence_data in json_data:
        var node = EvidenceNode.new()
        node.id = evidence_data["id"]
        node.display_name = evidence_data["display_name"]
        node.description = evidence_data["description"]
        node.evidence_type = evidence_data["evidence_type"]
        node.required_archetype = evidence_data.get("required_archetype", "")
        node.required_tier = evidence_data.get("required_tier", 0)
        node.meta_tags = evidence_data.get("meta_tags", [])
        node.points_to_conclusion = evidence_data.get("points_to_conclusion", "")

        evidence_nodes[node.id] = node

func get_visible_evidence(profile: PsycheProfile) -> Array[EvidenceNode]:
    var visible = []
    for node in evidence_nodes.values():
        if node.is_visible_to_profile(profile):
            visible.append(node)
    return visible

func get_evidence_by_id(id: String) -> EvidenceNode:
    return evidence_nodes.get(id, null)
```

**Case Conclusion Assembly**

```gdscript
class_name CaseRefraction
extends Node

var evidence_database: EvidenceDatabase
var collected_evidence: Array[String] = []  # Evidence IDs collected this run

func _ready():
    evidence_database = preload("res://data/evidence_database.gd").new()

func collect_evidence(evidence_id: String):
    if evidence_id not in collected_evidence:
        collected_evidence.append(evidence_id)

func get_available_conclusions() -> Array[String]:
    # Determine which case conclusions are supported by collected evidence
    var conclusions = {}

    for evidence_id in collected_evidence:
        var node = evidence_database.get_evidence_by_id(evidence_id)
        if node and node.points_to_conclusion != "":
            if node.points_to_conclusion not in conclusions:
                conclusions[node.points_to_conclusion] = 0
            conclusions[node.points_to_conclusion] += 1

    # A conclusion requires at least 3 supporting evidence nodes to be available
    var available = []
    for conclusion_id in conclusions.keys():
        if conclusions[conclusion_id] >= 3:
            available.append(conclusion_id)

    return available

func get_conclusion_text(conclusion_id: String) -> String:
    # Load conclusion data from JSON
    var file = FileAccess.open("res://data/case_conclusions.json", FileAccess.READ)
    var json_data = JSON.parse_string(file.get_as_text())

    for conclusion_data in json_data:
        if conclusion_data["id"] == conclusion_id:
            return conclusion_data["text"]

    return ""
```

**Example Evidence JSON Structure**

```json
[
  {
    "id": "bruises_on_arms",
    "display_name": "Bruises on Victim's Arms",
    "description": "Signs of a physical struggle. Someone with strength.",
    "evidence_type": "physical",
    "required_archetype": "authority",
    "required_tier": 1,
    "meta_tags": ["lena_hargate", "violence", "conspiracy_layer_1"],
    "points_to_conclusion": "conclusion_authority_power_struggle"
  },
  {
    "id": "microexpressions_cctv",
    "display_name": "Micro-Expressions on Hotel CCTV",
    "description": "The victim was afraid of someone she knew well.",
    "evidence_type": "psychological",
    "required_archetype": "empathy",
    "required_tier": 2,
    "meta_tags": ["lena_hargate", "relationship", "conspiracy_layer_1"],
    "points_to_conclusion": "conclusion_empathy_betrayal"
  }
]
```

**Integration Points:**
- World objects (crime scene items, CCTV footage) check `EvidenceNode.is_visible_to_profile()` before appearing
- Dialogue system checks `CaseRefraction.collected_evidence` to unlock certain dialogue branches
- End-of-run UI calls `CaseRefraction.get_available_conclusions()` to present accusation options

**Performance:**
- Evidence database loaded once at game start. JSON parsing is one-time cost.
- Evidence filtering is O(n) where n = number of evidence nodes (~100-150 total). Acceptable.

### 3.4 Dialogue System

**Responsibilities:**
- Branching dialogue trees with choice nodes
- Psyche-gated dialogue options (certain choices require specific sub-skills)
- Internal Voice injection during dialogue (skill check interruptions)
- NPC state persistence (what has been asked, what has been revealed)

**Data Structure: Dialogue Tree**

```gdscript
class_name DialogueNode
extends Resource

@export var id: String
@export var speaker: String  # "witness_a", "suspect_b", "internal_voice_logic"
@export var text: String
@export var choices: Array[DialogueChoice] = []
@export var next_node_id: String  # For linear progression
@export var is_terminal: bool = false  # End of dialogue

class DialogueChoice:
    var text: String
    var next_node_id: String
    var required_subskill: String = ""  # "intimidation", "suggestion", etc.
    var insight_cost: int = 0
    var is_locked: bool = false
```

**Dialogue Manager**

```gdscript
class_name DialogueManager
extends Node

var current_tree: Array[DialogueNode] = []
var current_node: DialogueNode
var psyche_profile: PsycheProfile

signal dialogue_started
signal dialogue_ended
signal choice_presented(choices: Array)

func start_dialogue(tree_id: String):
    current_tree = _load_dialogue_tree(tree_id)
    current_node = current_tree[0]
    dialogue_started.emit()
    _display_current_node()

func _display_current_node():
    DialogueUI.show_text(current_node.speaker, current_node.text)

    if current_node.choices.size() > 0:
        var available_choices = _filter_choices(current_node.choices)
        choice_presented.emit(available_choices)
    elif not current_node.is_terminal:
        # Auto-advance
        await get_tree().create_timer(2.0).timeout
        advance_to_node(current_node.next_node_id)
    else:
        dialogue_ended.emit()

func _filter_choices(choices: Array) -> Array:
    var filtered = []
    for choice in choices:
        var is_available = true

        # Check psyche gate
        if choice.required_subskill != "":
            if not psyche_profile.is_subskill_active(choice.required_subskill):
                choice.is_locked = true
                is_available = false

        # Check Insight cost
        if choice.insight_cost > InsightManager.current_insight:
            choice.is_locked = true
            is_available = false

        filtered.append(choice)

    return filtered

func advance_to_node(node_id: String):
    for node in current_tree:
        if node.id == node_id:
            current_node = node
            _display_current_node()
            return

func _load_dialogue_tree(tree_id: String) -> Array[DialogueNode]:
    # Load from JSON (similar to evidence database)
    var file = FileAccess.open("res://data/dialogue/%s.json" % tree_id, FileAccess.READ)
    var json_data = JSON.parse_string(file.get_as_text())
    # Parse into DialogueNode array
    return []  # Implementation details omitted for brevity
```

**Internal Voice Injection**

```gdscript
# During dialogue, Internal Voices can fire as interruptions
func _on_internal_voice_trigger(voice_archetype: String, text: String):
    DialogueUI.show_internal_voice(voice_archetype, text)
    # Player must respond within time window (handled by UI)
```

**Example Dialogue JSON**

```json
[
  {
    "id": "witness_a_intro",
    "speaker": "Witness A",
    "text": "I didn't see anything. I swear.",
    "choices": [
      {
        "text": "[Intimidation] You're lying. Tell me the truth.",
        "required_subskill": "intimidation",
        "next_node_id": "witness_a_intimidated"
      },
      {
        "text": "[Suggestion] I know this is hard. But I need your help.",
        "required_subskill": "suggestion",
        "next_node_id": "witness_a_persuaded"
      },
      {
        "text": "Okay. Thanks anyway.",
        "next_node_id": "witness_a_dismissed"
      }
    ]
  }
]
```

**Performance:**
- Dialogue trees are lazy-loaded (only load when dialogue starts, unload after).
- Text rendering is Godot's `RichTextLabel` (hardware-accelerated).

### 3.5 Roguelite Meta-Progression

**Responsibilities:**
- Persist meta-case board state across runs
- Track unlocks (Psyche Echoes spent, Memory Anchors purchased)
- Handle run history (previous builds, case conclusions, death counts)
- Manage run-to-run state transitions

**Meta-Case Board Data Structure**

```gdscript
class_name MetaCaseBoard
extends Resource

var evidence_fragments: Array[EvidenceFragment] = []
var connections: Array[EvidenceConnection] = []
var conspiracy_layers_unlocked: int = 0

class EvidenceFragment:
    var evidence_id: String
    var run_number: int
    var confidence: float  # 1.0 if run completed, 0.5 if died
    var psyche_profile_snapshot: Dictionary  # What build found this?

class EvidenceConnection:
    var fragment_a_id: String
    var fragment_b_id: String
    var meta_tag: String  # The tag that connects them

func add_evidence(evidence_id: String, run_num: int, completed: bool, profile: PsycheProfile):
    var fragment = EvidenceFragment.new()
    fragment.evidence_id = evidence_id
    fragment.run_number = run_num
    fragment.confidence = 1.0 if completed else 0.5
    fragment.psyche_profile_snapshot = profile.to_dict()
    evidence_fragments.append(fragment)

    _check_for_new_connections(fragment)

func _check_for_new_connections(new_fragment: EvidenceFragment):
    var new_evidence = EvidenceDatabase.get_evidence_by_id(new_fragment.evidence_id)

    for existing_fragment in evidence_fragments:
        if existing_fragment.evidence_id == new_fragment.evidence_id:
            continue  # Same evidence

        var existing_evidence = EvidenceDatabase.get_evidence_by_id(existing_fragment.evidence_id)

        # Check for shared meta-tags
        for tag in new_evidence.meta_tags:
            if tag in existing_evidence.meta_tags:
                var connection = EvidenceConnection.new()
                connection.fragment_a_id = new_fragment.evidence_id
                connection.fragment_b_id = existing_fragment.evidence_id
                connection.meta_tag = tag
                connections.append(connection)

                _check_conspiracy_layer_unlock(tag)

func _check_conspiracy_layer_unlock(tag: String):
    # Certain meta-tags unlock conspiracy layers
    if "conspiracy_layer_2" in tag and conspiracy_layers_unlocked < 2:
        conspiracy_layers_unlocked = 2
        # Trigger unlock event

func get_all_connections() -> Array[EvidenceConnection]:
    return connections
```

**Persistence: Save System**

```gdscript
class_name SaveManager
extends Node

const SAVE_PATH = "user://revachol_nights_save.dat"

var meta_case_board: MetaCaseBoard
var run_history: Array[RunRecord] = []
var total_runs: int = 0
var psyche_echoes: int = 0

class RunRecord:
    var run_number: int
    var psyche_profile: Dictionary
    var case_conclusion: String
    var districts_cleared: int
    var death: bool

func save_game():
    var save_data = {
        "meta_case_board": _serialize_meta_case_board(),
        "run_history": _serialize_run_history(),
        "total_runs": total_runs,
        "psyche_echoes": psyche_echoes
    }

    var file = FileAccess.open(SAVE_PATH, FileAccess.WRITE)
    file.store_var(save_data)
    file.close()

func load_game():
    if not FileAccess.file_exists(SAVE_PATH):
        return  # No save file

    var file = FileAccess.open(SAVE_PATH, FileAccess.READ)
    var save_data = file.get_var()
    file.close()

    meta_case_board = _deserialize_meta_case_board(save_data["meta_case_board"])
    run_history = _deserialize_run_history(save_data["run_history"])
    total_runs = save_data["total_runs"]
    psyche_echoes = save_data["psyche_echoes"]

func _serialize_meta_case_board() -> Dictionary:
    return {
        "evidence_fragments": meta_case_board.evidence_fragments.map(func(f): return {
            "evidence_id": f.evidence_id,
            "run_number": f.run_number,
            "confidence": f.confidence,
            "psyche_profile_snapshot": f.psyche_profile_snapshot
        }),
        "connections": meta_case_board.connections.map(func(c): return {
            "fragment_a_id": c.fragment_a_id,
            "fragment_b_id": c.fragment_b_id,
            "meta_tag": c.meta_tag
        }),
        "conspiracy_layers_unlocked": meta_case_board.conspiracy_layers_unlocked
    }

# Deserialize functions omitted for brevity
```

**Run Lifecycle**

```gdscript
class_name RunManager
extends Node

var current_run_number: int = 0
var current_psyche_profile: PsycheProfile
var current_district: int = 0

func start_new_run():
    current_run_number += 1
    current_psyche_profile = PsycheGenerator.new().generate_build()
    current_district = 0

    # Display psyche reveal cinematic
    PsycheRevealUI.show(current_psyche_profile)

func on_district_complete():
    current_district += 1
    # Present debrief UI (Insight spend, path choice)

func on_player_death():
    _end_run(false)

func on_case_close(conclusion_id: String):
    _end_run(true, conclusion_id)

func _end_run(completed: bool, conclusion_id: String = ""):
    # Log run to meta-case board
    var collected_evidence = CaseRefraction.collected_evidence
    for evidence_id in collected_evidence:
        SaveManager.meta_case_board.add_evidence(evidence_id, current_run_number, completed, current_psyche_profile)

    # Log run record
    var record = SaveManager.RunRecord.new()
    record.run_number = current_run_number
    record.psyche_profile = current_psyche_profile.to_dict()
    record.case_conclusion = conclusion_id
    record.districts_cleared = current_district
    record.death = not completed
    SaveManager.run_history.append(record)

    SaveManager.save_game()

    # Return to precinct hub
    SceneManager.load_scene("res://scenes/precinct_hub.tscn")
```

**Death Penalty: 50% Evidence Confidence**

When a run ends in death, evidence is still added to the meta-case board but with `confidence = 0.5`. The board UI visually represents this (greyed out, marked as "unconfirmed").

**Psyche Echo System**

```gdscript
class_name PsycheEchoShop
extends Node

func purchase_memory_anchor(subskill_name: String):
    if SaveManager.psyche_echoes >= 3:
        SaveManager.psyche_echoes -= 3
        # Lock this sub-skill for next run
        RunManager.locked_subskill = subskill_name

func purchase_meditation_focus(archetype: String):
    if SaveManager.psyche_echoes >= 2:
        SaveManager.psyche_echoes -= 2
        # Increase weight for this archetype in next shuffle
        PsycheGenerator.archetype_weights[archetype] += 0.2
```

### 3.6 District/World Generation

**Responsibilities:**
- Assemble districts from authored room prefabs
- Populate rooms with enemies, evidence, and environmental objects
- Ensure case-relevant content appears based on PsycheProfile
- Handle time-of-day/mood lighting per district

**District Structure**

```
District = 4-6 Rooms
Room = Combat encounter + Evidence nodes + Environmental hazards
```

**Room Assembly**

```gdscript
class_name DistrictGenerator
extends Node

var room_pool: Dictionary = {
    "standard": [
        preload("res://districts/rooms/alley_01.tscn"),
        preload("res://districts/rooms/warehouse_02.tscn"),
        # ... 20+ room prefabs
    ],
    "safe_room": [
        preload("res://districts/rooms/debrief_01.tscn")
    ]
}

var enemy_pool: Dictionary = {
    "standard": [
        preload("res://enemies/corrupt_cop.tscn"),
        preload("res://enemies/thug.tscn"),
    ],
    "elite": [
        preload("res://enemies/detective_rival.tscn"),
    ]
}

func generate_district(district_number: int, psyche_profile: PsycheProfile) -> Array[Node2D]:
    var rooms = []
    var room_count = randi_range(4, 6)

    for i in range(room_count - 1):
        var room_scene = room_pool["standard"].pick_random()
        var room_instance = room_scene.instantiate()
        _populate_room(room_instance, district_number, psyche_profile)
        rooms.append(room_instance)

    # Final room is always a safe room (debrief)
    var safe_room = room_pool["safe_room"][0].instantiate()
    rooms.append(safe_room)

    return rooms

func _populate_room(room: Node2D, district_num: int, profile: PsycheProfile):
    # Spawn enemies
    var enemy_count = 3 + district_num
    var spawn_points = room.get_node("EnemySpawnPoints").get_children()

    for i in range(min(enemy_count, spawn_points.size())):
        var enemy_scene = enemy_pool["standard"].pick_random()
        var enemy_instance = enemy_scene.instantiate()
        enemy_instance.global_position = spawn_points[i].global_position
        room.add_child(enemy_instance)

    # Place evidence nodes (filtered by psyche profile)
    var available_evidence = EvidenceDatabase.new().get_visible_evidence(profile)
    if available_evidence.size() > 0:
        var evidence_to_place = available_evidence.pick_random()
        var evidence_object = preload("res://world/evidence_object.tscn").instantiate()
        evidence_object.evidence_id = evidence_to_place.id
        var evidence_spawn = room.get_node("EvidenceSpawnPoint")
        evidence_object.global_position = evidence_spawn.global_position
        room.add_child(evidence_object)
```

**Case-Relevant Content Placement**

The key design principle: **evidence nodes visible to the current PsycheProfile are guaranteed to appear** in at least one room per district. This prevents runs where the player never encounters their accessible evidence.

```gdscript
func _ensure_case_relevant_content(rooms: Array, profile: PsycheProfile):
    var visible_evidence = EvidenceDatabase.new().get_visible_evidence(profile)
    var evidence_to_guarantee = visible_evidence.slice(0, 2)  # Guarantee 2 per district

    for i in range(evidence_to_guarantee.size()):
        var room = rooms[i]
        var evidence_object = preload("res://world/evidence_object.tscn").instantiate()
        evidence_object.evidence_id = evidence_to_guarantee[i].id
        room.add_child(evidence_object)
```

**Procedural Generation Philosophy:**

This is NOT fully procedural. Rooms are hand-authored prefabs. Enemy placement is hand-authored spawn points. Evidence placement is hand-authored spawn points. The "procedural" part is:
1. **Room order** (which rooms appear in which sequence)
2. **Enemy selection** (which enemy types spawn at which points)
3. **Evidence selection** (which evidence nodes appear, filtered by psyche)

This gives designers full control over room quality while maintaining replayability through recombination.

**Performance:**
- District generation happens during loading screens (between districts). Not real-time.
- Target generation time: <0.5 seconds for a 6-room district.

### 3.7 Insight Economy Implementation

**Responsibilities:**
- Track Insight counter
- Handle drops from enemies/events
- Validate Insight spending (combat vs narrative channels)
- Provide UI for Insight display and shop

**Insight Manager**

```gdscript
class_name InsightManager
extends Node

var current_insight: int = 0

signal insight_changed(new_value: int)
signal insight_spent(amount: int, channel: String)

func add_insight(amount: int):
    current_insight += amount
    insight_changed.emit(current_insight)

func spend_insight(amount: int, channel: String) -> bool:
    if current_insight >= amount:
        current_insight -= amount
        insight_spent.emit(amount, channel)
        insight_changed.emit(current_insight)
        return true
    return false

func get_current_insight() -> int:
    return current_insight
```

**Insight Drops**

```gdscript
# In LootDropper component (attached to enemies)
class_name LootDropper
extends Node

@export var insight_drop_min: int = 1
@export var insight_drop_max: int = 2

func drop_loot():
    var insight_amount = randi_range(insight_drop_min, insight_drop_max)
    var pickup = preload("res://pickups/insight_pickup.tscn").instantiate()
    pickup.insight_value = insight_amount
    pickup.global_position = get_parent().global_position
    get_tree().root.add_child(pickup)
```

**Debrief Shop UI**

```gdscript
class_name DebriefShop
extends Control

@onready var combat_upgrades_list = $CombatUpgrades
@onready var narrative_unlocks_list = $NarrativeUnlocks

func _ready():
    _populate_combat_upgrades()
    _populate_narrative_unlocks()

func _populate_combat_upgrades():
    var upgrades = [
        {"name": "Damage +15%", "cost": 6},
        {"name": "HP +10%", "cost": 6},
        {"name": "Dodge Speed +20%", "cost": 8},
    ]

    for upgrade in upgrades:
        var button = Button.new()
        button.text = "%s (%d Insight)" % [upgrade.name, upgrade.cost]
        button.pressed.connect(func(): _purchase_combat_upgrade(upgrade))
        combat_upgrades_list.add_child(button)

func _populate_narrative_unlocks():
    var unlocks = [
        {"name": "Interrogate Witness A", "cost": 7, "dialogue_id": "witness_a_interrogation"},
        {"name": "Examine Crime Scene", "cost": 5, "evidence_ids": ["blood_spatter", "weapon_trace"]},
    ]

    for unlock in unlocks:
        var button = Button.new()
        button.text = "%s (%d Insight)" % [unlock.name, unlock.cost]
        button.pressed.connect(func(): _purchase_narrative_unlock(unlock))
        narrative_unlocks_list.add_child(button)

func _purchase_combat_upgrade(upgrade: Dictionary):
    if InsightManager.spend_insight(upgrade.cost, "combat"):
        CombatUpgradeApplier.apply_upgrade(upgrade.name)

func _purchase_narrative_unlock(unlock: Dictionary):
    if InsightManager.spend_insight(unlock.cost, "narrative"):
        if "dialogue_id" in unlock:
            DialogueManager.start_dialogue(unlock.dialogue_id)
        elif "evidence_ids" in unlock:
            for evidence_id in unlock.evidence_ids:
                CaseRefraction.collect_evidence(evidence_id)
```

### 3.8 Animation System

**Responsibilities:**
- Archetype-specific combat animations
- Smooth state transitions (idle -> attack -> idle)
- Animation blending for movement + attack
- Visual feedback for Internal Voice triggers

**Animation Setup (per archetype)**

Each archetype has a unique `AnimationTree` with states:
- Idle
- Walk
- Attack_Light
- Attack_Heavy
- Dodge
- Hit
- Death

**Authority Archetype Animations**

```
AnimationTree (Authority)
├─ Idle (loop)
├─ Walk (loop)
├─ Attack_Heavy (one-shot, 0.5s duration)
├─ Attack_Combo (one-shot, 0.8s duration)
├─ Dodge (one-shot, 0.2s duration with armor frames)
├─ Hit (one-shot, 0.3s duration)
└─ Death (one-shot, 1.0s duration)
```

**Empathy Archetype Animations**

```
AnimationTree (Empathy)
├─ Idle (loop, lighter breathing)
├─ Walk (loop, faster cycle)
├─ Attack_Light (one-shot, 0.2s duration)
├─ Attack_Flurry (one-shot, 0.6s duration, 5-hit combo)
├─ Dodge (one-shot, 0.5s duration with long i-frames)
├─ Hit (one-shot, 0.3s duration)
└─ Death (one-shot, 1.0s duration)
```

**Animation Budget:**

Per archetype:
- 5 unique attack animations (light, heavy, combo_1, combo_2, signature)
- 1 dodge animation
- 1 hit animation
- 1 death animation
- 2 movement animations (idle, walk)

Total: 10 animations × 4 archetypes = 40 core animations.

**Animation Tools:**
- Spine 2D for character rigs (export to Godot via Spine-Godot plugin)
- Alternative: DragonBones (open-source, Godot-native)
- Aseprite for sprite frames if pixel art route is chosen

**Performance:**
- Godot's `AnimationTree` is GPU-accelerated. No CPU bottleneck for 2D sprite animations.
- Max concurrent animated sprites on-screen: 20 (player + 10 enemies + 9 VFX). Well within budget.

### 3.9 Audio System

**Responsibilities:**
- Archetype-reactive music (music layers change with dominant archetype)
- Combat SFX (hit sounds, dodge sounds, Internal Voice stings)
- Ambient audio for districts
- UI audio feedback

**Music System: Layered Stems**

Each combat track has 4 stems (one per archetype). The dominant archetype's stem is louder; non-dominant stems are quieter but still present.

```gdscript
class_name MusicManager
extends Node

@onready var authority_stem = $AuthorityStem
@onready var empathy_stem = $EmpathyStem
@onready var logic_stem = $LogicStem
@onready var electrochemistry_stem = $ElectrochemistryStem

func set_archetype_focus(dominant: String):
    # Fade all stems to -20dB
    authority_stem.volume_db = -20
    empathy_stem.volume_db = -20
    logic_stem.volume_db = -20
    electrochemistry_stem.volume_db = -20

    # Boost dominant stem to 0dB
    match dominant:
        "authority":
            authority_stem.volume_db = 0
        "empathy":
            empathy_stem.volume_db = 0
        "logic":
            logic_stem.volume_db = 0
        "electrochemistry":
            electrochemistry_stem.volume_db = 0
```

**SFX Budget:**

- Combat hits: 10 variations per archetype (40 total)
- Dodge: 4 variations (1 per archetype)
- Internal Voice sting: 1 unique sound (vinyl scratch)
- UI clicks: 3 variations
- Ambient loops: 5 districts × 1 loop each = 5 loops

**Audio Middleware: FMOD or Godot Native?**

**Decision: Godot Native (`AudioStreamPlayer` nodes)**

**Rationale:**
- FMOD adds 50MB to runtime size. Overkill for a 2D roguelite.
- Godot's built-in audio bus system handles layering, ducking, and effects.
- No licensing costs for FMOD.
- The layered music system can be implemented with 4 `AudioStreamPlayer` nodes and volume automation.

**Audio Format:**
- Ogg Vorbis for music (compressed, ~128kbps)
- WAV for SFX (uncompressed, low-latency)

**Performance:**
- Max concurrent audio streams: 32 (Godot's default limit). Combat rarely exceeds 10 concurrent sounds.

---

## 4. Data Architecture

### 4.1 Data Storage Format: JSON

**Why JSON:**
- Human-readable (designers can edit evidence/dialogue files in a text editor)
- Git-friendly (clean diffs, easy merging)
- Godot-native parsing (`JSON.parse_string()`)
- No database server required

**Why NOT a database (SQLite, PostgreSQL):**
- Overkill for static authored content
- Adds dependency and complexity
- No runtime queries complex enough to justify SQL

**Data File Structure**

```
res://data/
├─ evidence_nodes.json          (all evidence definitions)
├─ case_conclusions.json        (all case ending texts)
├─ dialogue/
│  ├─ witness_a.json
│  ├─ witness_b.json
│  └─ suspect_interrogation.json
├─ enemies/
│  ├─ corrupt_cop_stats.json
│  └─ thug_stats.json
├─ rooms/
│  └─ room_metadata.json        (tags, difficulty, case relevance)
└─ meta_case/
   └─ conspiracy_layers.json    (unlock conditions, lore text)
```

### 4.2 Key Data Schemas

**Evidence Node Schema**

```json
{
  "id": "string (unique)",
  "display_name": "string",
  "description": "string",
  "evidence_type": "physical|testimonial|circumstantial|psychological",
  "required_archetype": "authority|empathy|logic|electrochemistry|\"\"",
  "required_tier": 0-3,
  "meta_tags": ["string array"],
  "points_to_conclusion": "conclusion_id"
}
```

**Dialogue Node Schema**

```json
{
  "id": "string",
  "speaker": "string",
  "text": "string",
  "choices": [
    {
      "text": "string",
      "next_node_id": "string",
      "required_subskill": "string|\"\"",
      "insight_cost": 0-15
    }
  ],
  "next_node_id": "string",
  "is_terminal": true|false
}
```

**Enemy Stats Schema**

```json
{
  "id": "enemy_corrupt_cop",
  "display_name": "Corrupt Cop",
  "hp": 50,
  "damage": 10,
  "move_speed": 150,
  "attack_range": 60,
  "chase_range": 300,
  "insight_drop_min": 2,
  "insight_drop_max": 4,
  "behavior_type": "aggressive|defensive|patrol"
}
```

**Save Data Schema**

```json
{
  "meta_case_board": {
    "evidence_fragments": [
      {
        "evidence_id": "string",
        "run_number": 0,
        "confidence": 0.5-1.0,
        "psyche_profile_snapshot": { "authority": 10, ... }
      }
    ],
    "connections": [
      {
        "fragment_a_id": "string",
        "fragment_b_id": "string",
        "meta_tag": "string"
      }
    ],
    "conspiracy_layers_unlocked": 0-5
  },
  "run_history": [
    {
      "run_number": 0,
      "psyche_profile": { "authority": 10, ... },
      "case_conclusion": "conclusion_id",
      "districts_cleared": 0-5,
      "death": true|false
    }
  ],
  "total_runs": 0,
  "psyche_echoes": 0
}
```

### 4.3 Data Loading Strategy

**When to load:**
- **On game boot**: Evidence database, enemy stats, room metadata
- **On run start**: Dialogue trees for current district's NPCs
- **On demand**: Individual dialogue trees when NPC is interacted with

**Caching:**
- Evidence database stays in memory (small, ~50KB)
- Dialogue trees are cached per district, unloaded when district ends
- Room prefabs are instantiated from preloaded scenes (Godot's scene caching)

**Hot Reloading (Development):**
- Godot's editor can reload JSON files on save
- Designers can edit evidence/dialogue and see changes immediately in playtest without restarting

---

## 5. Performance Considerations

### 5.1 Target Framerate

**PC (Steam):** 60 FPS locked
**Nintendo Switch:** 30 FPS minimum, 60 FPS target in docked mode

**Frame budget:**
- 60 FPS = 16.67ms per frame
- 30 FPS = 33.33ms per frame

**Where frames get spent:**
- Rendering (sprites, effects): ~6ms
- Physics (collision, movement): ~4ms
- Gameplay logic (AI, input, skill checks): ~3ms
- Audio: ~1ms
- Budget remaining for spikes: ~2-3ms

### 5.2 Memory Budget

**PC:** 2GB runtime allocation
**Switch:** 1.5GB runtime allocation (OS reserves ~1GB)

**Memory breakdown:**
- Textures/sprites: 800MB (uncompressed atlas)
- Audio: 200MB (music stems + SFX)
- Code/scripts: 50MB
- Runtime data (enemy instances, rooms, UI): 300MB
- Save data: <1MB
- Reserved for spikes: 150MB

### 5.3 Hot Paths (What Runs Every Frame)

**Critical paths to profile:**
1. **Player movement update** (60 FPS)
2. **Enemy AI updates** (60 FPS for aggressive enemies, 10 FPS for patrol)
3. **Hitbox collision queries** (only when attacks are active)
4. **Animation state machine updates** (60 FPS)
5. **UI updates** (Insight counter, HP bars) (60 FPS)

**What does NOT run every frame:**
- Psyche build generation (once per run)
- Evidence filtering (once per room load)
- Dialogue parsing (only during dialogue)
- Save system writes (only on run end)

### 5.4 Optimization Strategy

**Phase 1: Ship with GDScript everywhere**
- Get the game running at 60 FPS on target PC hardware
- Profile with Godot's built-in profiler
- Identify bottlenecks

**Phase 2: Rewrite hot paths in C#**
- If player movement or enemy AI exceeds 8ms per frame, move to C#
- Expected: GDScript will be fast enough for everything except possibly enemy AI pathfinding

**Phase 3: Switch-specific optimizations**
- Reduce particle effects
- Lower texture resolution (2048x2048 atlases -> 1024x1024)
- Reduce enemy count per room by 20%
- Target 30 FPS stable

**Phase 4: Post-launch optimization**
- If players report performance issues, profile user-submitted saves
- Add graphics quality settings (particle density, shadow quality)

**Never guess. Always profile.**

### 5.5 Known Performance Risks

**Risk 1: Too many active enemies on-screen**
- Mitigation: Cap enemies per room at 10. Spawn reinforcements only after initial enemies die.

**Risk 2: Dialogue tree parsing during combat (Internal Voices)**
- Mitigation: Pre-parse Internal Voice checks at room start. Store as runtime-ready data structures.

**Risk 3: Procedural district generation takes too long**
- Mitigation: Generate districts asynchronously during loading screens. Show animated "shuffling" UI.

**Risk 4: Save file writes cause frame hitches**
- Mitigation: Save system writes happen only at run end (not mid-run). Acceptable hitch at end screen.

---

## 6. Technical Risks & Mitigation

### 6.1 Critical Technical Risks

**Risk 1: Godot's 2D physics is not deterministic across platforms**

**Likelihood:** Medium
**Impact:** High (combat feel could differ between PC and Switch)
**Mitigation:**
- Use fixed timestep physics (`Physics.set_physics_jitter_fix()`)
- Extensively playtest on Switch hardware from prototype phase
- Avoid physics-based enemy movement (use kinematic bodies with manual collision resolution)

---

**Risk 2: JSON parsing performance degrades with large save files**

**Likelihood:** Low (save files should be <100KB)
**Impact:** Medium (save/load hitches)
**Mitigation:**
- Profile save file size at meta-case Layer 3 (run 20+)
- If save files exceed 500KB, migrate to binary serialization (Godot's `.tres` format or MessagePack)

---

**Risk 3: Case Refraction system becomes a maintenance nightmare**

**Likelihood:** High
**Impact:** High (adding new evidence breaks existing cases)
**Mitigation:**
- Strict evidence node schema validation (automated tests)
- Editor tool to visualize evidence-to-conclusion mappings
- Designers must document the "psychological rationale" for each evidence node's archetype requirement
- If technical debt accumulates, allocate 2-week refactor sprint mid-development

---

**Risk 4: Internal Voice timing windows feel inconsistent across framerates**

**Likelihood:** Medium
**Impact:** High (core mechanic feels broken on Switch)
**Mitigation:**
- Use delta-time for timing windows, not frame counts
- Playtest on 30 FPS builds early (force 30 FPS cap on PC for testing)
- If timing still feels off, add framerate-dependent window scaling (longer windows at 30 FPS)

---

**Risk 5: Psyche shuffle feels "too random" (players get bad builds repeatedly)**

**Likelihood:** Medium
**Impact:** Medium (player frustration)
**Mitigation:**
- Implement a "pity system": if player gets the same dominant archetype 3 runs in a row, force a different dominant on run 4
- Psyche Echo system gives limited player control (already designed)
- Playtest extensively to tune weights

---

**Risk 6: Godot export to Switch fails or has showstopper bugs**

**Likelihood:** Low (Godot 4.x has official Switch support)
**Impact:** Critical (blocks console release)
**Mitigation:**
- Apply for Nintendo developer license in first 3 months of development
- Test Switch exports every month from prototype phase onward
- Budget 3 months of Switch-specific QA and optimization before submission

---

**Risk 7: Git merge conflicts in JSON files (evidence, dialogue)**

**Likelihood:** High (multiple designers editing same files)
**Impact:** Low (annoying but not blocking)
**Mitigation:**
- Split large JSON files into smaller per-case files
- Use JSON formatting tools to ensure consistent indentation (prevents trivial diffs)
- Train designers on Git basics (branches, pull requests)
- If conflicts become frequent, consider a custom editor tool that generates JSON from a GUI

---

### 6.2 Moderate Technical Risks

**Risk 8: Animation budget explodes**
- Each archetype needs 10 animations. If quality bar is high, this could take 4-6 weeks per archetype.
- Mitigation: Reuse idle/walk animations across archetypes. Only attack/dodge/signature are unique.

**Risk 9: Godot's tilemap performance on Switch**
- Large rooms with dense tilemaps could drop frames.
- Mitigation: Use chunked tilemaps (Godot 4.x's TileMap layers). Profile early.

**Risk 10: Dialogue JSON files become unreadable at scale**
- A dialogue tree with 50 nodes is hard to edit as raw JSON.
- Mitigation: Build a simple in-editor dialogue graph tool (Godot has graph editor nodes). Exports to JSON.

---

## 7. Development Pipeline

### 7.1 Version Control Strategy

**Tool: Git + GitHub (or GitLab)**

**Repository structure:**
```
/revachol-nights/
├─ .git/
├─ .gitignore
├─ .gitattributes  (LFS for large assets)
├─ project.godot
├─ export_presets.cfg
├─ scenes/
├─ scripts/
├─ data/
├─ assets/
│  ├─ sprites/
│  ├─ audio/
│  └─ fonts/
├─ addons/  (Godot plugins)
└─ docs/
```

**.gitignore:**
```
# Godot
.import/
.godot/
*.translation

# OS
.DS_Store
Thumbs.db

# Builds
builds/
exports/
```

**Git LFS for large files:**
- `.png`, `.jpg`, `.ogg`, `.wav` files tracked with LFS
- Prevents repo bloat (art assets can be GBs)

**Branching strategy:**
- `main` branch: stable, always builds
- `dev` branch: active development, merges to `main` weekly
- Feature branches: `feature/psyche-system`, `feature/case-refraction`
- Hotfix branches: `hotfix/combat-bug-123`

**Commit discipline:**
- Commits are atomic (one feature/fix per commit)
- Commit messages follow format: `[System] Description`
  - Example: `[Combat] Add dodge i-frames for Empathy archetype`
  - Example: `[CaseRefraction] Fix evidence filtering bug`

### 7.2 Build System

**Godot's built-in export system:**
- Export presets for PC (Windows, Linux, macOS), Switch
- Automated via command line: `godot --export "Windows Desktop" builds/windows/revachol_nights.exe`

**Build script (Bash):**

```bash
#!/bin/bash
# build_all.sh

echo "Building all platforms..."

# PC builds
godot --headless --export "Windows Desktop" builds/windows/revachol_nights.exe
godot --headless --export "Linux/X11" builds/linux/revachol_nights.x86_64
godot --headless --export "Mac OSX" builds/macos/revachol_nights.app

# Switch build (requires Nintendo SDK)
# godot --headless --export "Nintendo Switch" builds/switch/revachol_nights.nsp

echo "Builds complete."
```

### 7.3 CI/CD Pipeline

**Tool: GitHub Actions**

**Workflow file: `.github/workflows/build.yml`**

```yaml
name: Build and Test

on:
  push:
    branches: [main, dev]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    container:
      image: barichello/godot-ci:4.3
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        with:
          lfs: true

      - name: Build Windows
        run: |
          mkdir -p builds/windows
          godot --headless --export "Windows Desktop" builds/windows/revachol_nights.exe

      - name: Build Linux
        run: |
          mkdir -p builds/linux
          godot --headless --export "Linux/X11" builds/linux/revachol_nights.x86_64

      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: builds
          path: builds/

  test:
    runs-on: ubuntu-latest
    container:
      image: barichello/godot-ci:4.3
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run GDScript tests
        run: |
          godot --headless --script res://tests/run_tests.gd
```

**Automated testing:**
- Unit tests for `PsycheProfile`, `EvidenceNode`, `InsightManager`
- Integration tests for `CaseRefraction` (does evidence filtering work correctly?)
- No automated combat testing (requires human feel validation)

### 7.4 Testing Approach

**Testing pyramid:**

```
        /\
       /  \  Manual playtesting (feel, balance)
      /____\
     /      \ Integration tests (system interactions)
    /________\
   /          \ Unit tests (data structures, logic)
  /____________\
```

**Unit tests (GDScript via Godot's GUT plugin):**
- `PsycheProfile` generation (do points sum to 24?)
- `EvidenceNode` visibility filtering (does Authority Tier 2 see the right evidence?)
- `InsightManager` spend validation (can't spend more than you have)

**Integration tests:**
- Load a psyche profile, generate a district, verify case-relevant evidence appears
- Load a dialogue tree, verify psyche-gated options are locked correctly

**Manual playtesting:**
- Combat feel (every archetype, every enemy type)
- Case refraction clarity (do players understand why they see certain evidence?)
- Insight economy balance (does it feel tense or punishing?)
- Meta-case pacing (does Layer 1 unlock at the right time?)

**Playtesting schedule:**
- Weekly internal playtests (team)
- Monthly external playtests (friends, Discord community) starting at month 6
- Closed beta (100 players) at month 16

### 7.5 Tools and Editor Extensions

**Custom Godot editor tools:**

1. **Evidence Graph Visualizer**
   - GUI tool to visualize evidence-to-conclusion mappings
   - Shows which psyche builds can access which evidence
   - Validates that every conclusion has at least 3 supporting evidence nodes

2. **Dialogue Tree Editor**
   - In-editor graph for branching dialogue
   - Exports to JSON
   - Real-time validation of psyche gates and Insight costs

3. **Psyche Build Simulator**
   - Generate 1000 random builds, visualize distribution
   - Ensure no archetype is under-represented

4. **Meta-Case Board Debugger**
   - Load a save file, visualize the board in the editor
   - Show connections, conspiracy layer progress

**External tools:**
- **Aseprite** (or Krita) for sprite art
- **Spine 2D** (or DragonBones) for character animation
- **REAPER** (or Ableton) for music composition
- **Audacity** for SFX editing
- **Obsidian** (or Notion) for design documentation

---

## 8. Third-Party Dependencies

### 8.1 Core Dependencies

| Dependency | Version | Purpose | License | Notes |
|------------|---------|---------|---------|-------|
| **Godot Engine** | 4.3 | Game engine | MIT | Open-source, no runtime fees |
| **GUT (Godot Unit Test)** | 9.x | Unit testing | MIT | GDScript testing framework |
| **Spine-Godot Plugin** | 4.3-compatible | 2D animation | Spine License | Requires Spine Pro license (~$300) |
| **Git LFS** | 3.x | Large file storage | MIT | For art assets |

### 8.2 Optional Dependencies (Stretch Goals)

| Dependency | Version | Purpose | License | Notes |
|------------|---------|---------|---------|-------|
| **Dialogic** | 2.x | Visual dialogue editor | MIT | If custom dialogue tool isn't built |
| **Godot Jolt Physics** | 4.3-compatible | Deterministic physics | MIT | If default physics are non-deterministic |

### 8.3 No AI/ML Dependencies

The pitch mentions "modern AI-driven narrative systems hidden behind retro interfaces," but this is NOT procedural text generation. It refers to the Case Refraction system's logic-driven evidence filtering. No LLMs, no neural nets, no tensorflow. The "AI" is a 200-line GDScript function.

### 8.4 No Networking Dependencies

Single-player only. No multiplayer, no online leaderboards (at launch). If post-launch features include Steam leaderboards, use Steamworks API (via GodotSteam plugin).

### 8.5 Middleware Budget

| Item | Cost |
|------|------|
| Spine Pro (animation) | $300 one-time |
| Nintendo Switch Developer License | $500/year |
| Steam Direct Fee | $100 per game |
| **Total:** | **~$900 year 1** |

---

## 9. Platform-Specific Considerations

### 9.1 PC (Steam)

**Input:**
- Keyboard + Mouse (primary)
- Gamepad (Xbox, PlayStation, generic) (secondary)

**Graphics:**
- Target: GTX 1050 / RX 560
- Resolution: 1080p native, 1440p/4K upscale
- Framerate: 60 FPS locked

**Steam features:**
- Cloud saves (save file sync)
- Achievements (meta-case milestones, run challenges)
- Trading cards (stretch goal)

**Build size:**
- Estimated: 500MB compressed (1GB uncompressed)

### 9.2 Nintendo Switch

**Input:**
- Joy-Con (docked/handheld)
- Pro Controller
- No touch screen controls (combat requires buttons)

**Graphics:**
- Handheld: 720p, 30 FPS minimum
- Docked: 1080p, 60 FPS target
- Reduce particle effects, lower texture res

**Switch-specific optimizations:**
- Cap enemy count per room at 8 (vs 10 on PC)
- Reduce animation frame rate for background elements (30 FPS animations)
- Compress audio to 96kbps (vs 128kbps on PC)

**Build size:**
- Estimated: 400MB compressed

**Submission requirements:**
- ESRB/PEGI rating (likely T for Teen / 16+)
- Lotcheck compliance (Nintendo's QA process, 2-4 weeks)

### 9.3 Console Ports (PS5/Xbox Series)

**Not scoped for v1.0.**

**If pursued post-launch:**
- PS5: Use DualSense haptics for Internal Voice triggers
- Xbox: Use Xbox Live achievements
- Both: Target 60 FPS locked, 4K upscale

**Porting effort estimate:** 2-3 months per platform (mostly QA and platform-specific features).

---

## 10. Development Roadmap (Technical Milestones)

| Milestone | Timeline | Deliverables |
|-----------|----------|--------------|
| **M1: Prototype** | Month 0-3 | Combat loop for 2 archetypes, 1 district, no narrative |
| **M2: Core Systems** | Month 3-6 | Full psyche system, case refraction prototype, Insight economy |
| **M3: Vertical Slice** | Month 6-9 | 1 full run (5 districts, 1 case, meta-case board) |
| **M4: Content Pass** | Month 9-12 | 4 archetypes, 10 case branches, 20+ rooms |
| **M5: Polish** | Month 12-15 | Animation pass, audio pass, UI polish |
| **M6: Switch Port** | Month 15-18 | Switch optimization, Lotcheck submission |
| **M7: Beta** | Month 18-20 | Closed beta (100 players), balance tuning |
| **M8: Launch** | Month 20-24 | Final QA, Steam launch, Switch launch (if approved) |

**Team assumptions:**
- 1 programmer (BYTE)
- 1 designer (REED)
- 1 writer (NOVA)
- 1 artist (2D sprites, animation)
- 1 audio designer (music, SFX)

**Critical path bottlenecks:**
- Animation production (10 animations × 4 archetypes = 40 animations)
- Case content authoring (10 case branches × 10 evidence nodes each = 100 evidence nodes)
- Switch QA and optimization

---

## 11. Technical Design Philosophy (BYTE's Principles)

1. **Ship it, then improve it.**
   - The game in this document is shippable. No "we'll figure it out later" systems.

2. **What's the simplest version?**
   - Combat is 2D sprites with hitboxes. Not a physics simulation.
   - Case refraction is JSON filtering, not an AI model.
   - Districts are prefab assembly, not procedural generation.

3. **Profile before you optimize.**
   - Start 100% GDScript. Move to C# only if profiler shows the need.

4. **Does it compile? Does it run? Ship it.**
   - Godot 4.3 is stable. The architecture in this document compiles and runs.

5. **Never build your own engine.**
   - Godot gives us 90% of what we need. The 10% we write is game logic, not engine code.

---

## 12. Appendix: File Structure

```
/revachol-nights/
├─ .git/
├─ .gitignore
├─ .gitattributes
├─ project.godot
├─ export_presets.cfg
│
├─ scenes/
│  ├─ main.tscn
│  ├─ precinct_hub.tscn
│  ├─ district_template.tscn
│  ├─ player.tscn
│  └─ ui/
│     ├─ hud.tscn
│     ├─ debrief_shop.tscn
│     ├─ meta_case_board.tscn
│     └─ dialogue_ui.tscn
│
├─ scripts/
│  ├─ core/
│  │  ├─ game_director.gd
│  │  ├─ run_manager.gd
│  │  └─ save_manager.gd
│  ├─ psyche/
│  │  ├─ psyche_profile.gd
│  │  ├─ psyche_generator.gd
│  │  └─ internal_voice_check.gd
│  ├─ combat/
│  │  ├─ player_controller.gd
│  │  ├─ combat_controller.gd
│  │  ├─ enemy_ai.gd
│  │  └─ health_component.gd
│  ├─ case/
│  │  ├─ evidence_node.gd
│  │  ├─ evidence_database.gd
│  │  └─ case_refraction.gd
│  ├─ dialogue/
│  │  ├─ dialogue_node.gd
│  │  └─ dialogue_manager.gd
│  ├─ economy/
│  │  └─ insight_manager.gd
│  ├─ world/
│  │  └─ district_generator.gd
│  └─ ui/
│     └─ dialogue_ui.gd
│
├─ data/
│  ├─ evidence_nodes.json
│  ├─ case_conclusions.json
│  ├─ dialogue/
│  │  ├─ witness_a.json
│  │  └─ suspect_interrogation.json
│  ├─ enemies/
│  │  └─ enemy_stats.json
│  └─ meta_case/
│     └─ conspiracy_layers.json
│
├─ assets/
│  ├─ sprites/
│  │  ├─ player/
│  │  ├─ enemies/
│  │  └─ world/
│  ├─ audio/
│  │  ├─ music/
│  │  └─ sfx/
│  └─ fonts/
│
├─ addons/
│  ├─ gut/  (unit testing)
│  └─ spine_godot/  (animation)
│
├─ tests/
│  ├─ unit/
│  │  ├─ test_psyche_profile.gd
│  │  └─ test_evidence_database.gd
│  └─ integration/
│     └─ test_case_refraction.gd
│
└─ docs/
   ├─ technical-architecture.md  (this document)
   ├─ game-design.md
   └─ pitch.md
```

---

## 13. Conclusion

This is the architecture. It compiles. It runs. It ships.

Every system has a data structure, a flow, and integration points. Every risk has a mitigation. Every performance target has a budget. No hand-waving. No "we'll figure it out."

The game is:
- **Godot 4.3** (engine)
- **GDScript + C# for hot paths** (language)
- **JSON for data** (storage)
- **Component-based scenes** (architecture)
- **PC + Switch** (platforms)
- **18-24 months** (timeline)

What's the simplest version? This is it.

Now we prototype. Now we profile. Now we ship.

---

**BYTE, Lead Programmer**
**2026-02-07**

*Does it compile? Does it run? Ship it.*
