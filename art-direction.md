# REVACHOL NIGHTS — Art Direction Document

**Art Director**: PIXEL
**Status**: Complete — Ready for Asset Production
**Version**: 1.0
**Date**: 2026-02-07

---

## 1. Visual Identity Statement

**"Neon-stained noir brutalism viewed through a CRT screen at 3 AM — where every pixel carries rain and regret."**

This is a game about fractured identity in a city that remembers everything and understands nothing. The art must communicate instant noir atmosphere while maintaining Dead Cells-tier combat readability. The visual style is a deliberate collision: 1970s Eastern European brutalist architecture meets 1990s neo-noir cinematography meets 2003 digital interfaces, all rendered through modern pixel art techniques. The player must see a single screenshot and immediately feel rain, smoke, neon, and the weight of unsolved cases.

What's the silhouette test? A character must read as "detective" from shape alone. What's the three-color rule? Every screen uses maximum three dominant colors plus one accent. What's the reference? *Drive* (2011) meets *Blade Runner* (1982) meets Windows XP's amber CRT terminal aesthetic meets *Dead Cells*' kinetic clarity.

---

## 2. Visual Feeling

### 2.1 Emotional Temperature

**Primary emotion**: Melancholic determination. The detective is tired but relentless. The city is beautiful in its decay. Violence is necessary but never celebratory. Every fight is a question mark; every death is a comma, not a period.

**Secondary emotion**: Unstable identity. The screen should feel like it might fracture at any moment. UI elements occasionally glitch. Character portraits shift subtly between frames. The world is solid; the self is not.

**Forbidden emotion**: Hopelessness. This is noir, not nihilism. There is always a case to solve, always a truth to uncover. The rain never stops, but the neon still glows.

### 2.2 Temperature and Atmosphere

- **Color temperature**: Cold overall (blue-teal base) with warm accent pools (neon orange, amber UI glow)
- **Lighting philosophy**: Perpetual twilight. No daytime scenes. Light sources are artificial: streetlamps, neon signs, CRT monitors, cigarette embers, muzzle flashes
- **Weather state**: Persistent rain. Not storm rain — the slow, inevitable drizzle that never quite stops. Rain is a constant visual texture, never absent
- **Air quality**: Visible. Cigarette smoke, fog, exhaust fumes. The air has volume. Backgrounds fade into atmospheric haze

### 2.3 Era and Aesthetic Fusion

**Base era**: 1970s-1980s post-industrial decay (Revachol's architecture, vehicles, fashion silhouettes)
**Technology era**: 2000s-2003 digital interfaces (CRT monitors, DOS-style terminals, dot matrix printouts, boxy computer hardware)
**Cinematic era**: 1990s neo-noir film language (rain-slicked reflections, neon color grading, dramatic shadows)
**Execution era**: Contemporary pixel art (modern animation techniques, shader effects, particle systems)

The fusion point: A world that peaked in 1979 and has been slowly crumbling while adding digital infrastructure as afterthought. The technology works but looks like it was installed by a government with no budget. Every computer is a beige CRT box. Every database looks like a DOS prompt. This is not cyberpunk's aspirational high-tech — this is bureaucratic low-tech that somehow still functions.

---

## 3. Color Palette

### 3.1 Primary Palette (Environmental Base)

| Color Name | Hex Value | Usage | Visual Weight |
|------------|----------|--------|---------------|
| **Revachol Blue** | `#1a2332` | Background shadows, night sky, deep building facades | 40% of screen |
| **Concrete Gray** | `#4a5568` | Building mid-tones, pavement, structural elements | 30% of screen |
| **Rain Steel** | `#778899` | Highlights on wet surfaces, reflections, metal | 15% of screen |
| **Fog White** | `#b8c5d6` | Atmospheric haze, distant lights, rain streaks | 10% of screen |
| **Asphalt Black** | `#0d1117` | Pure shadows, silhouettes, negative space | 5% of screen |

**Usage rules**:
- Revachol Blue is the foundational color. It appears in every single screen.
- Rain Steel is never used without accompanying Rain Blue or Concrete Gray — no floating highlights.
- Fog White fades into backgrounds. It is never a hard edge.
- Asphalt Black is used sparingly for pure silhouette moments and UI borders.

**Readability rule**: Player character must never use Revachol Blue or Concrete Gray as primary color. Character must pop against the environment.

### 3.2 Accent Palette (Neon and Narrative Signaling)

| Color Name | Hex Value | Usage | Narrative Context |
|------------|----------|--------|------------------|
| **Neon Orange** | `#ff6b35` | Danger, heat, violence, cigarette embers, muzzle flashes | Authority moments |
| **Electric Cyan** | `#00d9ff` | Neon signs, holographic UI, psychic phenomena | Empathy moments |
| **Logic Gold** | `#f4a742` | Evidence markers, interactive objects, trap indicators | Logic moments |
| **Chem Green** | `#39ff14` | Electrochemistry highs, speed trails, berserker effects | Electrochemistry moments |

**Usage rules**:
- Each accent color is tied to a Psyche archetype. The dominant archetype's accent color appears in the HUD, in ability VFX, and as subtle environmental tints.
- Neon Orange is the only accent that appears in non-archetype contexts (general danger, fire, explosions). It is the "universal threat" color.
- No more than ONE accent color dominates any given screen. A screen with Cyan neon signs does not also have Gold evidence markers glowing equally bright. Hierarchy is mandatory.
- Accent colors are always high-saturation. They must cut through the desaturated base palette.

**Accessibility note**: Neon Orange and Chem Green are the highest contrast pair for colorblind players. Critical gameplay information (danger vs. safe) must never rely solely on Cyan vs. Gold or Orange vs. Cyan.

### 3.3 UI Palette

| Color Name | Hex Value | Usage |
|------------|----------|--------|
| **Terminal Amber** | `#ffb627` | Text on dark backgrounds, data readouts, case file UI |
| **Screen Green** | `#33ff33` | Secondary UI text, confirmation states, positive feedback |
| **CRT Scanline** | `#0a0e14` with 40% opacity | Overlay on all UI panels for CRT texture |
| **UI Border Gray** | `#2d3748` | Panel borders, dividers, inactive elements |
| **Selection Highlight** | `#4fd1c5` | Active UI element borders, hover states |

**UI Design Philosophy**:
- All UI panels simulate CRT monitors or dot-matrix printouts.
- UI text uses a monospaced pixel font (design target: 8x8 or 12x12 grid).
- UI is diegetic wherever possible. The case board is a physical object in the precinct. The psyche profile is visualized as a psychological evaluation form.
- UI must be readable during motion. Text size minimum: 12px at 1080p.

**Forbidden**: Flat modern UI design, minimalism for minimalism's sake, transparent HUD elements that disappear over light backgrounds. If it looks like it belongs in a 2024 mobile app, it's wrong.

### 3.4 Archetype-Specific Color Overlays

When a psyche archetype is dominant, the entire game's color grading shifts subtly:

| Archetype | Overlay Color | Effect |
|-----------|--------------|--------|
| **Authority** | Red-orange tint (`#ff4500` at 8% opacity) | Warmer shadows, more contrast, sharper edges |
| **Empathy** | Cyan-blue tint (`#4fc3f7` at 6% opacity) | Cooler highlights, softer edges, increased fog |
| **Logic** | Amber-gold tint (`#ffa726` at 7% opacity) | Sharper focus, reduced atmospheric haze, crisper lines |
| **Electrochemistry** | Green-yellow tint (`#76ff03` at 10% opacity) | Increased saturation, motion blur, chromatic aberration at edges |

These overlays are applied as a full-screen post-process effect. They are subtle enough that the player doesn't consciously notice them but strong enough that switching archetypes feels visually distinct.

---

## 4. Shape Language

### 4.1 Dominant Geometric Vocabulary

**Primary shapes**: Rectangles and right angles. This is a city built on brutalist principles — concrete blocks, grid layouts, harsh perpendiculars.

**Secondary shapes**: Irregular diagonals. Rain, neon signs, and character silhouettes break the grid with diagonal lines that cut across the rigid architecture.

**Tertiary shapes**: Circles are RARE and MEANINGFUL. Circles appear only for: eyes, cigarette embers, neon bulbs, bullet casings, evidence markers. When the player sees a circle, it should feel intentional.

**Forbidden shapes**: Organic curves, soft rounded corners (except on character anatomy), decorative flourishes. This is not art nouveau's flowing lines. This is Soviet-bloc functionality.

### 4.2 Character Proportions

**Detective (Player Character)**:
- Proportions: 1:3.5 head-to-body ratio (slightly stylized but grounded)
- Silhouette: Long coat (trench coat or overcoat) that flows behind during movement. The coat is the character's visual signature — it must be readable in motion.
- Posture: Hunched shoulders, forward lean. The detective is tired. This reads even in idle animation.
- Weapon silhouettes: Each archetype has a distinct weapon profile:
  - **Authority**: Baton or nightstick (short, heavy club shape)
  - **Empathy**: Bare hands or gloves (no weapon, relies on evasion)
  - **Logic**: Thrown objects (darts, evidence bags) — asymmetric shapes
  - **Electrochemistry**: Broken bottle or improvised melee (jagged, chaotic)

**Enemy Silhouettes**:
- **Corrupt Cops**: Squared shoulders, upright posture, visible badges/uniforms. They look like authority figures.
- **Street Thugs**: Hunched, irregular silhouettes, asymmetric clothing (one shoulder higher, visible weapons).
- **Hallucinated Manifestations**: Distorted, elongated proportions (1:5 or 1:6 head-to-body). They should NOT look human at a glance. These are psyche projections, not people.
- **Boss Characters**: Twice the player's size, heavy geometric shapes (they occupy SPACE).

**Silhouette test requirement**: At 50% opacity and 50% scale, every character type must be identifiable by shape alone. If you can't tell a cop from a thug from a hallucination, the design has failed.

### 4.3 Environment Shapes

**Building facades**: Vertical rectangular panels. Windows are uniform grids. Brutalist buildings do not have decorative variation — they are BLOCKS.

**Interiors**: Right angles dominate. Rooms are boxes. Hallways are corridors. Furniture is functional and rectangular (metal desks, filing cabinets, CRT monitors on stands).

**Streets and alleys**: Perspective lines converge hard. The city compresses the player with its geometry. Wide streets are rare; most environments are narrow, channeling movement.

**Breakable objects**: Environmental hazards (crates, barrels, electrical boxes) are all clearly rectangular or cylindrical. They must read as "breakable" at a glance.

**Gameplay shape communication**:
- **Safe zones** (save rooms, hub areas): Horizontal lines dominate. Wider spaces. Less verticality.
- **Danger zones** (combat arenas): Vertical lines dominate. Taller ceilings, narrow corridors, compressed sightlines.
- **Interactive objects**: Always outlined in Logic Gold when in range. The outline adds a soft 2px glow.

---

## 5. Style Rules

### 5.1 Line Quality

**Pixel resolution**: Base artwork created at 1080p, designed to scale cleanly to 4K (2x integer scale). Pixel art uses a "large pixel" approach — not true retro 8-bit or 16-bit resolution, but a modern pixel aesthetic with visible pixels at 1080p.

**Line weight**: 2-3 pixel outlines on characters and foreground objects. 1 pixel outlines on background architecture. No outlines on distant background layers (atmospheric perspective).

**Outline color**: Not pure black. Outlines use a darkened version of the adjacent color. Example: Rain Steel highlights have outlines in Revachol Blue, not black. This prevents the "coloring book" effect.

**Anti-aliasing**: Selective. Character animations use sub-pixel AA on curves (elbows, shoulders, face). Environment tiles use hard-edge pixels. This contrast makes characters pop.

**Texture density**: Foreground objects (player, enemies, interactives) have high texture detail (visible fabric weaves, metal scratches, dirt). Backgrounds have reduced texture to prevent visual noise.

### 5.2 Animation Style

**Player character animation**:
- **Framerate**: 12 FPS for movement, 24 FPS for combat actions (attacks, dodges). The combat must be smooth; the walk cycle can be choppier.
- **Squash and stretch**: Moderate. Not Looney Tunes, but not realistic stiffness. A heavy attack squashes the anticipation frame and stretches the follow-through.
- **Smear frames**: Used on fast attacks (Electrochemistry archetype especially). A single blurred frame between keyframes to convey speed.
- **Idle animation**: Subtle. The detective shifts weight, adjusts their coat collar, looks over their shoulder. The city is dangerous; no one is truly at rest.
- **Hurt animation**: The character staggers BACK (never forward) and clutches their side. Brief i-frame flash (1 frame white, 1 frame normal, repeat 3x).

**Enemy animation**:
- Simpler than player. 8 FPS for movement, 12 FPS for attacks.
- Telegraph frames must be OBVIOUS. Wind-up frames hold for 6-8 frames before the strike. Empathy players depend on this readability.
- Death animation: Enemies dissolve into colored particles (Insight drops) rather than corpses. No blood pools (this is not a gore game; it's a psychological game).

**Environmental animation**:
- Rain: Constant. 2-pixel vertical streaks falling at 8 FPS. Denser in foreground, sparser in background.
- Neon signs: Flicker occasionally (every 3-5 seconds, a 2-frame flicker). Not constant buzzing — occasional imperfection.
- CRT monitors: Subtle scanline crawl (1-pixel vertical scrolling effect at 2 FPS).
- Cigarette smoke: 6-frame looping animation, rising and dissipating.

**VFX animation**:
- Muzzle flashes: 2 frames (bright flash, dim afterglow).
- Psychic effects (Empathy archetype): 8-frame shimmering aura with color oscillation.
- Trap activation (Logic archetype): 4-frame electric arc or snap-shut animation.
- Berserker trails (Electrochemistry archetype): 3-frame motion trail with Chem Green tint.

### 5.3 Lighting and Shadow

**Lighting model**: Not realistic. Stylized noir lighting with exaggerated contrast.

**Key light sources**:
- Streetlamps cast hard circular pools of light (bright center, sharp falloff).
- Neon signs cast colored glows (soft radial gradients, no hard edges).
- Muzzle flashes and explosions cast brief orange/red light (1-2 frames).
- The player character has a subtle "detective's spotlight" — they are always slightly more lit than they should be realistically. Gameplay readability > realism.

**Shadow behavior**:
- Shadows are cast directly downward or at a 45-degree angle (no complex multi-light shadow calculation).
- Shadows are solid Asphalt Black at 60% opacity. No soft penumbra.
- Background architecture casts long shadows that stretch across the ground, reinforcing the noir atmosphere.

**Atmospheric lighting**:
- Light shafts (god rays) appear rarely and only in significant narrative moments. They are NOT a constant effect.
- Fog layers use additive blending to create volumetric haze. Fog is thicker in the distance, thinner near the player.
- Rain catches light. Each raindrop streak has a subtle highlight on one side (Rain Steel color).

**Forbidden**: Realistic global illumination, ambient occlusion as a visible effect, lens flares (this is not a camera; this is the detective's eyes), bloom that obliterates readability.

### 5.4 Texture Approach

**Pixel texture style**: Hand-painted pixel textures with visible brush patterns (not dithering, not gradients). Think: someone painted this at low resolution with a 3-pixel brush.

**Material textures**:
- **Concrete**: Irregular pixel clusters suggesting rough surface. No perfect smoothness.
- **Metal**: Horizontal or vertical streak patterns suggesting brushed metal or rust.
- **Glass/wet surfaces**: Specular highlights (Rain Steel color) with slight distortion.
- **Fabric (clothing)**: Visible weave texture at character scale. Coats have heavy texture; shirts have lighter texture.
- **Screens (CRT monitors)**: Scanline overlay + slight RGB color separation (red/green/blue pixel fringe on high-contrast edges).

**Dithering policy**: NO classic dithering patterns (checkerboard, Bayer matrix). If we need a gradient, we paint it by hand with irregular pixel placement. Dithering reads as "retro game" — we want "modern pixel art."

**Normal maps**: Not used. This is 2D pixel art; lighting is painted, not calculated. Depth comes from parallax layers, not normal mapping.

### 5.5 Do's and Don'ts

#### DO:
- Paint rain on every surface. Everything is wet.
- Use neon sparingly. One bright sign per screen is a landmark; ten bright signs is visual noise.
- Let shadows dominate. 60% of the screen can be in shadow if the lit 40% is readable.
- Make the detective's coat flow. It's a visual signature.
- Use cigarette smoke as a visual motif. The detective smokes; so does the city.
- Make UI look like it was designed in 2003. Chunky buttons, visible borders, no flat design.
- Show the city's history in posters, graffiti, crumbling facades. Revachol remembers.

#### DON'T:
- Use pure black except for UI borders and deep shadows. Always mix in Revachol Blue.
- Use pure white except for text and brief flash effects. Fog White is the brightest environmental color.
- Make the player character blend into the background. They are the focal point.
- Animate at inconsistent framerates. Pick 8/12/24 FPS and stick to it per asset type.
- Use smooth gradients. Pixel art is about visible steps, not smooth blends.
- Add unnecessary detail to backgrounds. Detail belongs in the foreground.
- Forget the squint test. If it doesn't read at 50% scale, simplify it.

---

## 6. Asset Pipeline

### 6.1 File Formats and Standards

**Source art**:
- Format: `.aseprite` for all animated assets (character sprites, VFX, UI animations)
- Format: `.psd` or `.aseprite` for static assets (backgrounds, tiles, props)
- Color mode: RGB, 8-bit per channel
- Resolution: 1080p base (1920x1080), design for 2x integer scaling to 4K

**Export formats**:
- Sprites: `.png` with transparency, exported from Aseprite as sprite sheets
- Backgrounds: `.png`, no transparency, layered for parallax
- UI: `.png` with transparency for panels, `.ttf` or `.otf` for fonts (monospaced pixel font)

**Naming conventions**:
- `character_[name]_[archetype]_[action]_[frame].png`
  - Example: `character_detective_authority_attack_001.png`
- `enemy_[type]_[action]_[frame].png`
  - Example: `enemy_cop_walk_004.png`
- `bg_[location]_[layer]_[variant].png`
  - Example: `bg_whirling_paralx02_rain.png`
- `ui_[element]_[state].png`
  - Example: `ui_casefile_panel_open.png`
- `vfx_[effect]_[frame].png`
  - Example: `vfx_muzzleflash_002.png`

### 6.2 Resolution Standards Per Asset Type

| Asset Type | Canvas Size | Pixel Density | Notes |
|------------|------------|---------------|--------|
| Player character sprite | 128x128px | Character occupies ~80-100px height | Includes coat flow space |
| Enemy sprite (standard) | 96x96px | Enemy occupies ~70-80px height | Smaller than player |
| Enemy sprite (boss) | 256x256px | Boss occupies ~200px height | Twice the player's visual weight |
| Background layer (near) | 1920x1080px | Full screen | Parallax layer 1 (closest) |
| Background layer (mid) | 1920x1080px | Full screen | Parallax layer 2 |
| Background layer (far) | 1920x1080px | Full screen | Parallax layer 3 (farthest) |
| UI panel | Variable | Minimum 12px font at 1080p | Must scale cleanly |
| VFX sprite | 64x64px to 256x256px | Depends on effect scale | Particle effects use smaller |
| Tileset | 32x32px per tile | Standard tile size | For modular level construction |

**Pixel density rule**: At 1080p, one "game unit" equals 32 pixels. The player character is approximately 3 units tall (96px). This gives us consistent scale across all assets.

### 6.3 Tools and Software

**Required tools**:
- **Aseprite**: Primary animation and sprite creation tool. All character and VFX work.
- **Photoshop or Krita**: Background painting, large static asset creation.
- **TexturePacker or Shoebox**: Sprite sheet packing and optimization.
- **Unity or Godot**: Engine integration (TBD based on tech stack).

**Shader tools** (for post-process effects):
- **CRT shader**: Scanline overlay, slight curvature, RGB color separation on edges.
- **Rain shader**: Animated rain streak overlay, can be layered per parallax depth.
- **Archetype tint shader**: Full-screen color overlay based on dominant psyche (see 3.4).
- **Glitch shader**: Occasional UI corruption effect (rare, used for psyche shuffle moments).

**Font**:
- Monospaced pixel font, 8x8 or 12x12 grid.
- Reference: **Terminus**, **Mx437 IBM VGA 8x16**, or custom-designed.
- Must be readable at 12px minimum size.
- Includes: A-Z, a-z, 0-9, punctuation, special characters (€, $, %, etc.).

### 6.4 Handoff Process (Concept to Engine)

1. **Concept Phase**:
   - Mood sketch or reference board provided by PIXEL.
   - Sketch approval before moving to pixel art stage.

2. **Blockout Phase**:
   - Low-detail pixel art created at final resolution.
   - Animation timing blocked with key frames only.
   - Gameplay readability tested in-engine with blockout art.

3. **Final Art Phase**:
   - Full texture detail added.
   - Animation in-betweens completed at target framerate.
   - VFX and shaders applied.

4. **Integration Phase**:
   - Sprite sheets exported and imported to engine.
   - Collision boxes and hitboxes defined.
   - Layering and sorting order verified.

5. **Polish Phase**:
   - Squint test, thumbnail test, colorblind test conducted.
   - Tuning based on playtest feedback.

**Revision policy**: Each asset gets ONE revision pass after integration. If an asset requires more than one revision, it indicates insufficient planning in the concept/blockout phases. Plan better.

### 6.5 Version Control for Art Assets

**Repository structure**:
```
/art/
  /source/         # .aseprite, .psd source files (large, LFS-tracked)
  /export/         # .png exports (version-controlled)
  /reference/      # Mood boards, inspiration images (not exported to build)
  /wip/            # Work-in-progress, unreviewed art (not exported to build)
```

**Git LFS**: All source files (.aseprite, .psd) are tracked with Git LFS to avoid repository bloat.

**Asset review**: Art assets in `/wip/` are reviewed weekly. Approved assets move to `/source/` and `/export/`. Rejected assets remain in `/wip/` with notes.

---

## 7. Readability Audit

### 7.1 Squint Test

**Process**: View the game at 50% opacity or with heavy blur applied. The player character, enemies, and interactive objects must still be distinguishable by shape and color contrast.

**Pass criteria**:
- Player character is the brightest object on screen (or has the most saturated accent color).
- Enemies are distinct from background architecture by silhouette.
- Interactive objects (evidence, Insight drops) glow with Logic Gold and are visible even when blurred.
- UI elements remain readable (text size is large enough, contrast is high enough).

**Current concerns**:
- Revachol Blue and Concrete Gray are close in value. Ensure background layers have sufficient separation. Solution: Use Fog White to lighten distant layers, increasing atmospheric perspective.
- Electrochemistry's Chem Green and Logic Gold may be too similar in luminosity. Solution: Chem Green is neon-bright (full saturation), Logic Gold is matte (80% saturation). Different finish, different readability.

### 7.2 Thumbnail Test

**Process**: Capture a screenshot at 1920x1080, then scale it down to 320x180 (thumbnail size for Steam library). The game's visual identity must still be recognizable.

**Pass criteria**:
- Noir atmosphere is intact (dark palette with accent color pops).
- The detective's silhouette is recognizable.
- Neon signs or other accent lighting is visible.
- The image does not become a muddy gray blob.

**Design insurance**: Always include at least one neon accent in any key art or screenshot. The accent is the hook in the thumbnail.

### 7.3 Colorblind Test

**Tool**: Use Coblis Color Blindness Simulator or in-engine colorblind shader preview.

**Test cases**:
- **Protanopia** (red-blind): Neon Orange must remain distinct from Chem Green. Test: Both remain high-contrast against Revachol Blue.
- **Deuteranopia** (green-blind): Chem Green must remain distinct from Logic Gold. Test: Chem Green is significantly brighter.
- **Tritanopia** (blue-blind): Electric Cyan must remain distinct from Logic Gold. Test: Cyan is cooler-toned, Gold is warmer.

**Critical gameplay information** (danger vs. safe, interactive vs. non-interactive) does NOT rely on color alone:
- Danger is communicated by: Neon Orange color + animation (enemy wind-up) + audio cue.
- Interactive objects are communicated by: Logic Gold outline + proximity pulse animation + cursor change.
- Archetype identity is communicated by: Color tint + UI iconography + text label.

**Accessibility options** (to be implemented):
- High-contrast mode: Increases outline thickness from 2px to 4px, darkens backgrounds by 20%.
- Colorblind mode: Adds iconography to color-coded elements (archetype icons appear next to colored VFX).

### 7.4 Motion Test

**Process**: Record gameplay footage at 60 FPS. Pause at random intervals. Every paused frame must be readable.

**Pass criteria**:
- Attack telegraphs are visible even in fast combat (wind-up frames hold long enough).
- The player character's position is always clear (motion blur on Electrochemistry archetype does not obscure the character).
- VFX do not obscure enemy positions (particle effects are additive-blended, not opaque).
- UI remains readable during combat (no full-screen VFX that obliterate HUD elements).

**Current concerns**:
- Electrochemistry's speed trails may obscure the character. Solution: Trails are semi-transparent (40% opacity) and fade quickly (3-frame lifetime).
- Rain effects may clutter the screen. Solution: Rain density scales inversely with combat intensity. Fewer enemies = more rain; more enemies = less rain (reduces visual noise).

### 7.5 Readability During Psyche Shuffle

**Special case**: The psyche shuffle transition (when the screen fractures and reforms with a new archetype) is deliberately disorienting. However, the moment the new run begins, readability must be immediate.

**Pass criteria**:
- Within 1 second of the shuffle ending, the player can identify their new archetype by HUD color.
- Within 2 seconds, the player can execute their new archetype's basic combat verb without confusion.
- The transition does not induce motion sickness (no violent screen shake, no rapid full-screen color flashes).

---

## 8. Reference List

### 8.1 Game References

| Game | What We're Taking |
|------|------------------|
| **Dead Cells** | Kinetic 2D combat feel, tight responsive animation, clear enemy telegraphs, smooth dodge-roll i-frames |
| **Disco Elysium** | UI aesthetic (the ledger, the thought cabinet), psychological skill iconography, text-heavy dialogue presentation |
| **Hyper Light Drifter** | Neon accent color usage against dark backgrounds, atmospheric pixel art, minimalist UI |
| **Blasphemous** | Pixel art shadow and lighting quality, religious iconography aesthetic (adapted to political iconography for Revachol) |
| **Katana ZERO** | Neo-noir pixel art atmosphere, slow-motion effects, VHS/CRT aesthetic, rain effects |
| **Hades** | Character portrait presentation, boon/upgrade UI clarity, death transition aesthetic |

### 8.2 Film and Cinematography References

| Film | What We're Taking |
|------|------------------|
| **Blade Runner** (1982) | Rain-slicked streets, neon-lit noir, perpetual night, cigarette smoke as texture |
| **Drive** (2011) | Neon color grading (orange/cyan contrast), minimalist violence, synth-noir aesthetic |
| **The Third Man** (1949) | Harsh shadows, dramatic noir lighting, post-war decay |
| **Memories of Murder** (2003) | Gray palette, rain as constant motif, detective exhaustion |
| **Chinatown** (1974) | 1970s color grading, fedora-and-trenchcoat detective silhouette |

### 8.3 Architectural and Era References

| Reference | What We're Taking |
|-----------|------------------|
| **Soviet Brutalism** (1960s-1980s Eastern Europe) | Concrete panel buildings, repetitive rectangular facades, utilitarian design |
| **Post-industrial decay photography** (Rust Belt, Detroit) | Peeling posters, graffiti layers, broken windows, infrastructure as ruin |
| **DOS/Windows 95-XP UI** | Chunky buttons, visible borders, monospaced fonts, amber CRT terminals |
| **CRT monitor photography** | Scanline texture, slight screen curvature, RGB pixel separation on edges |

### 8.4 Art Movements and Styles

| Movement | What We're Taking |
|----------|------------------|
| **Noir photography** (1940s-1950s crime photography) | High contrast black-and-white translated to color (dark blues, selective warm accents) |
| **Vaporwave aesthetic** (2010s internet art) | CRT and early-digital nostalgia, but grounded in noir rather than pastel optimism |
| **Social realism** (Eastern European poster art) | Bold graphic shapes, political iconography, weathered texture |

---

## 9. Technical Constraints and Optimization

### 9.1 Performance Budgets

**Target platforms**:
- PC (Steam): Primary. Min spec: GTX 1050, 8GB RAM, i5 processor.
- Nintendo Switch: Secondary (post-launch port). Must run at 60 FPS in docked mode, 30 FPS acceptable in handheld.

**Draw call budget**:
- Max 200 draw calls per frame at 1080p.
- Use sprite atlases (texture packing) to minimize draw calls.
- Batch static background layers.

**Texture memory budget**:
- Max 512 MB VRAM for all art assets in a single district (excludes UI, which is persistent).
- Sprite sheets should not exceed 4096x4096px per sheet.
- Background layers use compressed PNG to reduce memory footprint.

**Particle budget**:
- Max 500 particles on screen simultaneously.
- Rain particles are pooled and reused (not spawned/destroyed constantly).
- VFX particles have a max lifetime of 2 seconds.

### 9.2 Shader Performance

**CRT shader**: Lightweight. Post-process overlay, runs once per frame on final render.
**Rain shader**: Moderate cost. Applied per parallax layer, but uses simple scrolling UV offset (not physics simulation).
**Archetype tint shader**: Negligible. Simple color multiply overlay.
**Glitch shader**: Expensive. Used ONLY during psyche shuffle transition (< 5 seconds per run). Can afford the cost.

**Shader LOD**: If frame rate drops below 60 FPS, disable CRT scanline detail (keep color grading, remove scanline crawl). This saves ~2ms per frame.

### 9.3 Animation Optimization

**Sprite sheet packing**: All character animations for a single archetype fit on one 4096x4096 sprite sheet. Do not split across multiple sheets.

**Frame skipping**: On lower-end hardware, animation can drop from 12 FPS to 8 FPS without breaking gameplay feel. Combat animations (24 FPS) must NOT drop below 12 FPS.

**LOD for distant enemies**: Enemies more than 1.5 screens away from the player switch to simplified 4-frame walk cycles instead of full 8-frame.

**Background animation LOD**: Distant parallax layers have static rain texture instead of animated rain particles.

### 9.4 Asset Streaming

**District loading**: Each district is a self-contained asset bundle. Load the next district during the debrief room (safe room) so the transition is seamless.

**Precinct hub**: Hub assets are loaded once at game start and remain in memory for the entire session. Hub is small (~20 MB of assets).

**UI persistence**: UI assets load once at game start and persist. Do not reload UI between runs.

---

## 10. Art Production Roadmap

### 10.1 Phase 1: Concept and Blockout (Weeks 1-2)

**Deliverables**:
- Mood board with 20-30 reference images organized by: Architecture, Lighting, Character, UI, VFX
- Palette swatches (hex values) painted in context (full scene mockup)
- Detective character concept (3 archetype variants: Authority, Empathy, Logic/Electrochemistry share similar loadouts visually)
- Enemy concept sketches (1 per enemy type: Cop, Thug, Hallucination, Boss)
- UI mockup (case file panel, psyche profile screen, HUD layout)
- One full background scene painted at final resolution (Whirling-in-Rags exterior)

**Goal**: Establish visual identity. Get team approval on style direction before moving to production.

### 10.2 Phase 2: Core Asset Production (Weeks 3-8)

**Deliverables**:
- Detective sprite sheets (all 4 archetypes):
  - Idle, walk, run, dodge, light attack, heavy attack, signature ability, hurt, death
  - ~200-300 frames total per archetype
- Enemy sprite sheets (4 enemy types):
  - Idle, patrol, attack, hurt, death
  - ~80-120 frames per enemy type
- Background art (5 districts, 3 parallax layers each):
  - 15 unique background scenes
  - Each scene has rain/no-rain variant (rain is a shader overlay, not a separate asset)
- UI assets:
  - HUD (HP bar, Insight counter, archetype indicator, ability cooldowns)
  - Case file panel, psyche profile screen, meta-case board, debrief room menu
  - Button states (normal, hover, pressed, disabled)
- VFX sprite sheets:
  - Muzzle flash, impact sparks, psychic aura, trap activation, berserker trail, Insight pickup glow, death dissolve
  - ~100-150 frames total across all VFX types

**Goal**: Get all core gameplay assets into the engine. By the end of Phase 2, the game is fully playable with final art (not placeholder).

### 10.3 Phase 3: Polish and Secondary Assets (Weeks 9-12)

**Deliverables**:
- Secondary enemy variants (recolors, slight animation tweaks)
- Boss enemy sprite sheets (2 boss types, larger scale, unique animations)
- Environmental props (crates, barrels, lampposts, neon signs, police tape, evidence markers)
- Cutscene illustrations (if needed — static images for key narrative moments)
- Psyche shuffle transition effect (fracture animation, screen reassembly)
- Additional VFX: rain puddle ripples, cigarette smoke, neon flicker, CRT glitch
- UI polish: hover animations, screen transitions, text fade-in effects

**Goal**: Elevate the game from "complete" to "polished." This is the phase where the art goes from functional to atmospheric.

### 10.4 Phase 4: Marketing and Key Art (Weeks 13-14)

**Deliverables**:
- Key art (hero image for Steam page): Detective silhouette against rain-streaked glass with 4 refracted versions (archetype colors)
- Steam capsule art (460x215, 231x87, 616x353, 374x448 sizes)
- Animated GIF for social media: Psyche shuffle moment (screen fractures, reforms with new archetype)
- Screenshot set (8-10 images) showcasing: Combat, case board, dialogue, archetype variety, boss fight
- Trailer storyboard (art-directed shot list for trailer production)

**Goal**: Marketing assets that capture the game's visual identity in a single glance. The key art must sell the game.

---

## 11. PIXEL's Final Notes

This art direction document is the visual contract. Every asset, every shader, every color choice must serve the core identity: *neon-stained noir brutalism viewed through a CRT screen at 3 AM*. If a proposed asset does not fit this identity, it does not belong in the game.

**Show me, don't tell me.** When in doubt, paint a mockup. A single painted frame is worth a thousand Slack messages debating "what should the rain look like?"

**What's the silhouette test?** If I can't identify the player character, enemy type, or interactive object from shape alone, the design has failed. Readability is not optional. It is the foundation of all visual design.

**Three colors. That's your palette.** Every screen uses three dominant colors (from the primary palette) plus one accent. More than that is noise. Discipline is the difference between atmosphere and chaos.

**The art is the first promise to the player.** A single screenshot must communicate noir, detective, action, and psychological fracture. If the screenshot looks like any other pixel art action game, we have failed. The style must be instantly recognizable.

**Does this read at a glance?** The squint test is the ultimate quality check. If it doesn't read when blurred, it doesn't read when the player is focused on combat. Simplify. Simplify again. Then simplify once more.

This game lives or dies on whether the player feels rain and neon and regret in the first 10 seconds. The art direction is not decoration. It is the game's voice, spoken in pixels and light.

Now go paint the city.

---

**END OF ART DIRECTION DOCUMENT**

*Art direction established by PIXEL. No placeholders. No "we'll figure it out later." Every hex value specified. Every style rule concrete. This is the visual bible. Follow it.*
