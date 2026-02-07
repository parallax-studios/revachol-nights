# REVACHOL NIGHTS — Production Plan

**Producer**: CLOCK
**Status**: Ready for Team Review and Scheduling
**Version**: 1.0
**Date**: 2026-02-07

---

## 0. Executive Summary

When is this actually shipping? 24 months from greenlight. Not 18. Not "when it's done." 24 months.

This is the production plan for REVACHOL NIGHTS — a 2D noir detective roguelite that is Dead Cells combat with Disco Elysium's psyche system. The design is ambitious. The art is specific. The audio is complex. The tech is solid. My job is to turn six excellent design documents into a game that exists.

**Core tension:** This game has AAA design depth with an indie team budget. Four archetypes with unique combat kits. Ten authored case branches. Procedural assembly of hand-crafted content. Adaptive music. Platform-reactive pixel art. This is not a small game disguised as one.

**What's the MVP?** Two archetypes, one case with four branches, five districts, meta-case board functional. Everything else is a v1.1 feature or a cut.

**What's the critical path?** Animation production. BYTE can build systems faster than PIXEL can animate them. The bottleneck is 40 unique animations across four archetypes. This drives the entire schedule.

**What could kill this project?** Scope creep on case content. NOVA's narrative bible defines 10 case conclusions. Each requires 8-10 unique evidence nodes and 3-4 witness dialogues. If we let this expand to 15 conclusions or 12 witnesses, we miss the ship date by six months. Cut scope, not corners.

**Team structure:** 5 people (1 programmer, 1 game designer, 1 writer, 1 artist, 1 audio designer). Part-time contractor for QA in months 18-24. No one crunches. If we can't ship without crunch, we cut scope.

**Budget assumption:** Indie scale ($200k-300k total, self-funded or small publisher advance). No investor pressure. Realistic timeline over aggressive promises.

This document contains:
- Project overview (scope, team, timeline)
- Milestone definitions with entry/exit criteria
- Sprint plan (24 months, broken into 2-week sprints)
- Task breakdown with owners, estimates, dependencies
- Risk register (likelihood, impact, mitigation)
- Critical path visualization
- Scope management (what's in, what's cut, what's at risk)

What's the plan? Build horizontally first (all systems shallow), then vertically (one archetype deep), then breadth (all four archetypes). Prototype fast, cut early, ship clean.

---

## 1. Project Overview

### 1.1 Scope Statement

**What we're building:**

A 2D action-roguelite detective game where:
- The player's personality (psyche build) determines their combat abilities, the evidence they can perceive, and the case conclusions they can reach
- Four distinct archetypes (Authority, Empathy, Logic, Electrochemistry) with unique combat kits and narrative access
- A murder case with 10 possible conclusions, filtered by psyche perspective
- 20-40 minute run loops with cross-run meta-case progression
- 5 districts with procedurally assembled hand-authored rooms
- PC (Steam) primary, Nintendo Switch secondary
- 60 FPS on PC, 30+ FPS on Switch

**What we're NOT building (v1.0):**
- Multiplayer or co-op
- More than one core case (Lena Hargate murder)
- Procedurally generated narrative content (all case branches are authored)
- Mobile ports
- Open-world exploration
- Voice acting for protagonist
- PlayStation/Xbox ports (post-launch only)

**Feature pillars (non-negotiable):**
1. Psyche build system (4 archetypes, 24 sub-skills)
2. Tight 2D combat (Dead Cells responsiveness standard)
3. Case Refraction narrative engine (evidence filtering by psyche)
4. Meta-case board (cross-run persistence)
5. Internal Voices system (mid-combat psychological interruptions)
6. Insight economy (single resource, dual spend channels)

**Stretch goals (v1.1 or cut if schedule slips):**
1. Psyche Blending (lock sub-skills between runs)
2. Partner NPC system
3. Rival Detective encounters
4. Dream Sequences hub
5. Revachol Radio adaptive audio

### 1.2 Team Structure

| Role | Name | Responsibilities | Availability |
|------|------|-----------------|--------------|
| **Producer** | CLOCK | Schedule, scope, dependencies, risk management, milestone validation | Full-time |
| **Lead Programmer** | BYTE | Combat system, psyche system, case refraction engine, Godot integration | Full-time |
| **Game Designer** | REED | Core loop tuning, Insight economy, progression curves, systems balance | Full-time |
| **Narrative Designer** | NOVA | Case content authoring, dialogue trees, evidence nodes, character writing | Full-time |
| **Art Director** | PIXEL | Sprite art, animations, visual effects, UI art, style enforcement | Full-time |
| **Sound Designer** | ECHO | Music composition, SFX recording, FMOD implementation, audio mixing | Full-time |
| **QA Lead** | CRASH | Bug tracking, test case design, platform validation, balance testing | Part-time (months 18-24) |

**External contractors (as needed):**
- Additional pixel artist (months 9-15, for secondary animations and environment art)
- Marketing consultant (month 18-20, for Steam page and trailer)

**Decision authority:**
- CLOCK has final call on scope cuts and schedule changes
- REED has final call on systems design and balance
- NOVA has final call on narrative content and tone
- PIXEL has final call on visual style and readability
- BYTE has final call on technical architecture and platform feasibility

### 1.3 Timeline Overview

**Total duration:** 24 months from greenlight to Steam launch

**Phase breakdown:**
- **Months 1-3:** Prototype (combat loop, psyche generation, basic Insight economy)
- **Months 4-6:** Core Systems (case refraction, dialogue, meta-case board)
- **Months 7-9:** Vertical Slice (1 full run, 2 archetypes, 1 case)
- **Months 10-15:** Content Production (4 archetypes, 10 case branches, 20+ rooms)
- **Months 16-18:** Polish (animation, audio, UI, balance)
- **Months 19-21:** Switch Port and QA
- **Months 22-24:** Beta, final QA, launch prep

**Key dates:**
- **Month 0:** Project kickoff, team onboarding
- **Month 3:** Prototype playable (internal only)
- **Month 9:** Vertical slice complete (first external playtests)
- **Month 16:** Content complete (feature lock)
- **Month 18:** Polish complete (alpha build)
- **Month 21:** Beta launch (100 external testers)
- **Month 24:** Steam launch

**Switch launch:** Month 25-26 (1-2 months after PC, pending Lotcheck approval)

### 1.4 Budget Constraints

**Assumed total budget:** $250,000 USD

**Budget allocation:**
- Salaries/contractor fees: $180,000 (72%)
- Software licenses: $5,000 (Spine, Nintendo dev kit)
- Platform fees: $1,000 (Steam Direct, Lotcheck)
- Marketing: $20,000 (trailer, Steam page art, influencer keys)
- Contingency: $44,000 (18% reserve for overruns and cuts)

**Cost-saving measures:**
- Godot engine (free, open-source)
- Self-publishing on Steam (no publisher revenue split)
- No outsourcing of core systems (all built in-house)
- Minimal external playtesting until month 16 (use Discord community)

**Budget risks:**
- Animation overrun (if external contractor needed for full 6 months: +$30k)
- Switch port complexity (if optimization requires external help: +$15k)
- Marketing underestimation (trailer production alone can hit $10k-15k)

**If budget is exceeded:** Cut Switch port to post-launch. Cut stretch goals. Reduce case branch count from 10 to 6.

---

## 2. Milestone Definitions

Each milestone has:
- **Entry criteria** (what must be true before this milestone starts)
- **Exit criteria** (what must be true to consider this milestone complete)
- **Deliverables** (specific artifacts or builds)
- **Owner** (who is accountable for completion)
- **Duration** (estimated calendar time)

### Milestone 1: Prototype (Months 1-3)

**Goal:** Prove the core combat feel and psyche system work together.

**Entry criteria:**
- Team onboarded
- Development environment set up (Godot 4.3, Git, FMOD)
- Design documents reviewed and approved by all leads

**Exit criteria:**
- Player can control a character with two archetype builds (Authority and Empathy)
- Combat feels responsive at 60 FPS on target PC hardware
- Psyche build generation algorithm produces valid builds
- Insight drops from enemies and can be spent on one upgrade type
- One room with 3 enemy types is playable
- Internal playtest confirms "Dead Cells-tier responsiveness"

**Deliverables:**
- Playable Windows build
- Prototype combat video (30 seconds, both archetypes)
- Psyche build generation test suite (100 builds, all valid)

**Owner:** BYTE (tech) + REED (design validation)

**Duration:** 12 weeks

**Key dependencies:**
- PIXEL delivers placeholder animations (idle, walk, attack, dodge) for both archetypes
- ECHO delivers placeholder combat SFX (hit, dodge, death)
- BYTE delivers player controller, enemy AI, psyche generation system

**Risks:**
- Combat doesn't feel tight (requires animation rework, could slip by 2 weeks)
- Godot 4.3 has undiscovered bugs (mitigation: BYTE prototypes in week 1 to validate engine)

---

### Milestone 2: Core Systems (Months 4-6)

**Goal:** All major systems exist in skeletal form. The game is playable but not fun yet.

**Entry criteria:**
- Milestone 1 complete
- Design specs for Case Refraction and Dialogue systems approved
- Evidence node schema defined (NOVA)

**Exit criteria:**
- Case Refraction engine filters evidence by psyche build
- Dialogue system supports branching trees with psyche-gated options
- Meta-case board displays evidence fragments and connects them
- Insight economy has both combat and narrative spend channels
- Two districts are playable (10 total rooms)
- One authored case branch (3 evidence nodes, 1 witness, 1 conclusion) is completable

**Deliverables:**
- Playable Windows build with 2 archetypes, 2 districts, 1 case branch
- Evidence database JSON with 20 evidence nodes
- Meta-case board UI mockup (functional, not polished)

**Owner:** BYTE (systems) + NOVA (case content) + REED (economy tuning)

**Duration:** 12 weeks

**Key dependencies:**
- NOVA delivers 20 evidence nodes with psyche tags
- NOVA delivers 3 dialogue trees (witness interrogations)
- PIXEL delivers UI mockups for case board and debrief shop
- BYTE delivers evidence filtering, dialogue manager, meta-case persistence

**Risks:**
- Case Refraction feels random instead of psychological (requires NOVA + REED collaboration to tune)
- Insight economy collapses (too easy or too hard) — requires 2 weeks of balance iteration
- Meta-case board is confusing (UI rework could add 1-2 weeks)

---

### Milestone 3: Vertical Slice (Months 7-9)

**Goal:** One full run is completable, demonstrating the entire core loop from run start to case conclusion.

**Entry criteria:**
- Milestone 2 complete
- All 5 districts have room layouts designed (REED)
- Music stems for 2 archetypes are composed (ECHO)

**Exit criteria:**
- Player can complete a full run (5 districts, case conclusion) with 2 archetypes
- Death triggers psyche reshuffle and returns to precinct hub
- Meta-case board accumulates evidence across 3+ runs
- Internal Voice system fires during combat and provides buffs/narrative
- Adaptive music layers change with combat intensity
- Vertical slice playable by external testers (first feedback loop)

**Deliverables:**
- Vertical slice build (Windows, 60 FPS, ~30 minutes per run)
- First external playtest with 10-15 participants
- Playtest report with prioritized feedback

**Owner:** CLOCK (milestone coordination) + full team

**Duration:** 12 weeks

**Key dependencies:**
- PIXEL delivers final animations for 2 archetypes (20 animations total)
- ECHO delivers music stems and combat SFX
- NOVA delivers 4 case branches (one per dominant archetype, simplified)
- BYTE integrates all systems into cohesive run loop

**Risks:**
- Vertical slice doesn't "feel like a game" (common at this stage — requires REED to tune pacing)
- External playtesters find Internal Voices annoying (high-priority fix, could require design rework)
- Run length exceeds 40 minutes (need to cut 1 district or reduce room count)

**Playtest goals:**
- Does combat feel good? (must be 8/10 or higher)
- Do players understand the psyche system? (60%+ comprehension rate)
- Is the Insight economy engaging? (qualitative: "agonizing in a good way")

---

### Milestone 4: Content Production (Months 10-15)

**Goal:** Expand from 2 archetypes to 4, from 4 case branches to 10, from 10 rooms to 25+. This is the breadth phase.

**Entry criteria:**
- Milestone 3 complete and playtest feedback incorporated
- All archetype designs finalized (REED)
- All case branch outlines written (NOVA)
- Animation pipeline proven (PIXEL can deliver 10 animations in 4 weeks)

**Exit criteria:**
- All 4 archetypes are playable with unique combat kits
- 10 case branches are authored (4 dominant archetype conclusions + 6 hybrid)
- 25+ unique room layouts across 5 districts
- 50+ enemy variants (standard, elite, boss)
- All evidence nodes authored (estimated 100 total)
- All witness/suspect dialogues written (estimated 15 NPCs)

**Deliverables:**
- Feature-complete build (all archetypes, all case branches)
- Full evidence database JSON
- Full dialogue tree library
- Content complete milestone build (Windows)

**Owner:** Full team (heavy load on PIXEL and NOVA)

**Duration:** 24 weeks (6 months)

**Key dependencies:**
- **Critical path: PIXEL animation production**
  - Logic archetype animations: 10 animations, 4 weeks
  - Electrochemistry archetype animations: 10 animations, 4 weeks
  - Boss enemy animations: 6 animations, 3 weeks
  - Environmental animations: 4 weeks
  - Total: 15 weeks of animation work over 24-week period
  - **If PIXEL falls behind, hire external contractor (budgeted)**

- NOVA case content authoring:
  - 6 additional case branches: 12 weeks (2 weeks per branch)
  - 10 additional witness dialogues: 6 weeks
  - 80 additional evidence nodes: 4 weeks
  - Total: 22 weeks of writing over 24-week period (feasible with parallel work)

- BYTE content integration:
  - New archetypes: 2 weeks each (8 weeks total)
  - Boss enemy AI: 4 weeks
  - District generation polish: 2 weeks
  - Performance optimization pass: 2 weeks
  - Total: 16 weeks over 24-week period (feasible)

**Risks (HIGH ALERT):**
- **Animation budget explodes** (likelihood: HIGH)
  - Each archetype needs 10 animations. If quality bar is raised mid-production, this becomes 12-15 per archetype.
  - Mitigation: Lock animation list at month 9. No additions after Milestone 3.
  - Contingency: Hire external animator for 3 months (cost: $15k-20k)

- **Case content becomes a maintenance nightmare** (likelihood: MEDIUM)
  - 10 case branches with 100 evidence nodes = 1000 possible interactions. Easy to create contradictions.
  - Mitigation: NOVA uses Evidence Graph Visualizer tool (BYTE builds this in month 7-8)
  - Contingency: Cut 2 case branches (reduce to 8 total)

- **Performance degrades with full content** (likelihood: MEDIUM)
  - Combat at 60 FPS with 2 archetypes doesn't guarantee 60 FPS with 4 archetypes + full VFX.
  - Mitigation: BYTE runs performance profiling every sprint starting month 10
  - Contingency: Reduce enemy count per room, simplify VFX

**Monthly check-ins during this phase:**
- Month 10: Logic archetype playable
- Month 11: Electrochemistry archetype playable
- Month 12: All 10 case branches authored (draft)
- Month 13: All animations complete (final)
- Month 14: All dialogue and evidence integrated
- Month 15: Content complete build, internal playtest, bug triage

---

### Milestone 5: Polish (Months 16-18)

**Goal:** The game is feature-complete. Now make it feel good.

**Entry criteria:**
- Milestone 4 complete (all content in)
- Feature lock (no new systems, no new case branches)
- Bug database established (using GitHub Issues or similar)

**Exit criteria:**
- All animations have final polish (timing, VFX, camera shake)
- All audio implemented (music, SFX, adaptive layers)
- All UI has final art (no placeholder buttons or panels)
- Balance pass complete (Insight drop rates, enemy HP, damage values)
- 50+ critical bugs fixed
- Game runs at 60 FPS on minimum spec PC (GTX 1050)

**Deliverables:**
- Alpha build (Windows, feature-complete and polished)
- Balance tuning document (Insight economy, archetype power levels)
- Art and audio asset finalization

**Owner:** REED (balance) + PIXEL (art polish) + ECHO (audio integration)

**Duration:** 12 weeks

**Key dependencies:**
- PIXEL: UI art pass (4 weeks), animation polish pass (4 weeks), VFX pass (2 weeks)
- ECHO: Final music stems (4 weeks), SFX recording (2 weeks), FMOD integration (3 weeks), mix pass (3 weeks)
- REED: Balance tuning (ongoing, 8 weeks), progression curve validation (2 weeks)
- BYTE: Bug fixes (ongoing), performance optimization (4 weeks)

**Risks:**
- Balance tuning takes longer than expected (common — roguelites need iteration)
  - Mitigation: REED starts balance passes in month 14 (during content production)
  - Contingency: Accept "good enough" balance, tune post-launch

- Audio integration reveals performance issues (music layering + SFX = frame drops)
  - Mitigation: ECHO tests FMOD integration in month 10 with placeholder content
  - Contingency: Simplify music layering (3 stems instead of 5)

**Playtest goals (month 16-17):**
- Run 2-3 external playtests with 20-30 participants each
- Focus areas: balance, clarity, pacing, fun
- Success metrics:
  - 70%+ players complete at least one full run
  - 50%+ players start a second run voluntarily
  - 80%+ players rate combat as "fun" or "very fun"
  - <20% players find Internal Voices annoying

---

### Milestone 6: Switch Port and Platform QA (Months 19-21)

**Goal:** The game runs at 30+ FPS on Nintendo Switch in handheld mode, 60 FPS in docked.

**Entry criteria:**
- Milestone 5 complete (alpha build stable)
- Nintendo developer license approved
- Switch dev kit hardware received

**Exit criteria:**
- Game builds and runs on Switch hardware
- Performance targets met (30 FPS handheld, 60 FPS docked)
- Switch-specific optimizations complete (reduced particles, texture compression)
- Lotcheck submission ready (ESRB rating obtained, compliance checklist complete)
- 100+ platform-specific bugs fixed

**Deliverables:**
- Switch build (NSP file)
- Lotcheck submission package
- Performance profiling report (frame time breakdown)

**Owner:** BYTE (porting) + CRASH (QA)

**Duration:** 12 weeks

**Key dependencies:**
- BYTE: Switch export setup (2 weeks), optimization pass (6 weeks), bug fixing (4 weeks)
- CRASH: Switch QA testing (8 weeks, part-time contractor)
- PIXEL: Low-res texture variants if needed (2 weeks)

**Risks:**
- Switch performance is worse than expected (likelihood: MEDIUM)
  - Mitigation: BYTE tests early Switch export in month 15 (before Polish phase)
  - Contingency: Cut particles, reduce enemy count, accept 30 FPS as standard (not just handheld)

- Lotcheck rejection (likelihood: LOW but high impact)
  - Mitigation: Follow Nintendo guidelines exactly, hire consultant if needed
  - Contingency: Push Switch launch to post-PC (month 25-26)

**Switch-specific concerns:**
- Memory budget (1.5GB vs 2GB on PC) — may require asset streaming or reduced texture quality
- Input (Joy-Con vs gamepad) — combat must feel good on small analog sticks
- Screen size (handheld) — UI must be readable at 720p, text size minimum 12px

---

### Milestone 7: Closed Beta (Months 22-23)

**Goal:** 100 external testers play the full game, find bugs, provide balance feedback.

**Entry criteria:**
- Milestone 6 complete (Switch port functional, though may launch later)
- Beta build stable (no critical bugs)
- Steam page live (with Coming Soon date)
- Press/influencer outreach started

**Exit criteria:**
- 100 beta testers recruited (Discord, mailing list, press)
- 50+ bugs reported and triaged
- Balance feedback collected and prioritized
- Press embargo lifted (first previews published)
- Launch trailer scripted and in production

**Deliverables:**
- Beta build (Windows, Steam keys distributed)
- Beta feedback report
- Launch trailer (first draft)
- Marketing assets (key art, screenshots, GIFs)

**Owner:** CLOCK (coordination) + CRASH (bug triage) + HYPE (marketing, external role or team effort)

**Duration:** 8 weeks

**Key dependencies:**
- CRASH: Bug tracking, triage, priority assignment (ongoing)
- BYTE: Critical bug fixes (ongoing)
- REED: Balance tuning based on beta feedback (2 weeks)
- Marketing contractor: Launch trailer production (4-6 weeks, external)
- PIXEL: Key art and Steam capsule art (2 weeks)

**Risks:**
- Beta uncovers game-breaking bug (likelihood: MEDIUM)
  - Mitigation: Internal QA pass before beta launch (CRASH tests for 2 weeks prior)
  - Contingency: Delay launch by 2-4 weeks if critical bugs found

- Beta feedback reveals fundamental balance issue (likelihood: LOW but painful)
  - Example: "Insight economy feels punishing, not tense"
  - Mitigation: This should have been caught in earlier playtests (months 16-18)
  - Contingency: Accept feedback, plan for Day 1 patch rather than delay launch

**Beta success metrics:**
- 70%+ completion rate (players finish at least one run)
- 50%+ return rate (players start 3+ runs)
- <100 bugs reported (manageable)
- Positive sentiment from press (no "fundamentally broken" previews)

---

### Milestone 8: Launch (Month 24)

**Goal:** The game is available on Steam. Players can buy it. It works.

**Entry criteria:**
- Milestone 7 complete
- All critical bugs fixed (P0, P1)
- Steam store page finalized (description, screenshots, trailer, pricing)
- Launch day announcement scheduled (social media, Discord, press)

**Exit criteria:**
- Game launches on Steam
- Launch day patch deployed (if needed)
- Monitoring and hotfix plan in place
- Post-launch roadmap communicated to players

**Deliverables:**
- Steam launch (Windows, Mac, Linux builds)
- Launch trailer published
- Day 1 patch (if critical bugs found in week prior)
- Post-launch support plan

**Owner:** CLOCK (launch coordination) + full team

**Duration:** 4 weeks (final prep and launch week)

**Key dependencies:**
- BYTE: Final bug fixes, launch build, Steam integration testing
- CLOCK: Launch day coordination, press outreach, community management
- Marketing: Launch announcements, influencer keys, Reddit/Discord promotion

**Risks:**
- Launch day server issues (N/A — single-player game, no servers)
- Critical bug discovered on launch day (likelihood: LOW)
  - Mitigation: Pre-launch QA sweep, beta testing catches most issues
  - Contingency: Hotfix within 24 hours, transparent communication with players

- Negative reviews due to performance issues on low-spec PCs (likelihood: MEDIUM)
  - Mitigation: Minimum spec clearly stated on Steam page, tested in beta
  - Contingency: Post-launch optimization patch within 2 weeks

**Launch day checklist:**
- [ ] Steam build uploaded and tested
- [ ] Launch trailer published on YouTube
- [ ] Press embargo lifted
- [ ] Social media announcements posted
- [ ] Discord announcement pinned
- [ ] Key art updated on all platforms
- [ ] Pricing finalized ($19.99 USD recommended)
- [ ] Launch discount considered (10% off first week to drive sales)
- [ ] Review keys sent to press/influencers (2 weeks prior)
- [ ] Monitoring dashboard active (Steam reviews, bug reports, social sentiment)

**Switch launch:** Month 25-26, pending Lotcheck approval (allow 2-4 weeks after submission).

---

## 3. Sprint Plan and Task Breakdown

**Sprint structure:** 2-week sprints, 52 sprints total over 24 months

**Sprint cadence:**
- **Sprint Planning:** Monday morning, week 1 (define tasks, assign owners, estimate effort)
- **Daily Standups:** 15 minutes, async via Slack (what did you do, what are you doing, blockers)
- **Sprint Review:** Friday afternoon, week 2 (demo completed work, gather feedback)
- **Sprint Retro:** Friday afternoon, week 2 (what went well, what didn't, process improvements)

**Task estimation:**
- Tasks are estimated in days (not story points)
- No task larger than 5 days (if larger, break it down)
- Each sprint has 8 working days per person (not 10 — account for meetings, interruptions)
- Buffer 20% for unknowns (e.g., 8 days of capacity = plan for 6.5 days of committed work)

**Priority levels:**
- **P0 (Critical):** Blocks milestone completion, must be done this sprint
- **P1 (High):** Important for milestone, should be done this sprint
- **P2 (Medium):** Nice to have, can slip to next sprint
- **P3 (Low):** Stretch goals, cut if needed

### Sample Sprint Breakdown: Months 1-3 (Prototype Phase)

**Sprint 1-2 (Weeks 1-4): Foundation**

| Task | Owner | Estimate | Dependency | Priority |
|------|-------|----------|------------|----------|
| Set up Godot 4.3 project | BYTE | 1 day | None | P0 |
| Set up Git repo + LFS | BYTE | 0.5 day | None | P0 |
| Create player scene (basic) | BYTE | 2 days | Godot setup | P0 |
| Implement player movement | BYTE | 2 days | Player scene | P0 |
| Create enemy scene (basic) | BYTE | 2 days | Godot setup | P0 |
| Implement enemy AI (patrol) | BYTE | 3 days | Enemy scene | P0 |
| Design psyche build schema | REED | 2 days | None | P0 |
| Write psyche generation algorithm | BYTE | 3 days | Schema design | P0 |
| Create test room scene | BYTE | 1 day | None | P0 |
| Placeholder animations (player idle/walk) | PIXEL | 3 days | Player scene | P0 |
| Placeholder animations (enemy idle/walk) | PIXEL | 2 days | Enemy scene | P0 |
| Placeholder SFX (footsteps, hits) | ECHO | 2 days | None | P1 |

**Total committed: 25.5 days across 5 people over 4 weeks = avg 1.3 days/person/week (safe)**

**Sprint 3-4 (Weeks 5-8): Combat Loop**

| Task | Owner | Estimate | Dependency | Priority |
|------|-------|----------|------------|----------|
| Implement hitbox/hurtbox system | BYTE | 3 days | Player movement | P0 |
| Authority attack animations | PIXEL | 4 days | Hitbox system | P0 |
| Empathy attack animations | PIXEL | 4 days | Hitbox system | P0 |
| Combat controller (Authority) | BYTE | 3 days | Attack anims | P0 |
| Combat controller (Empathy) | BYTE | 3 days | Attack anims | P0 |
| Dodge implementation | BYTE | 2 days | Combat controller | P0 |
| Damage calculation system | BYTE | 2 days | Hitbox system | P0 |
| Health component | BYTE | 1 day | Damage calc | P0 |
| Enemy attack AI | BYTE | 3 days | Combat controller | P0 |
| Combat SFX (hits, dodges) | ECHO | 3 days | Combat controller | P1 |
| Combat feel tuning | REED | 5 days | All combat tasks | P0 |

**Total committed: 33 days over 4 weeks = avg 1.65 days/person/week (acceptable)**

**Sprint 5-6 (Weeks 9-12): Insight Economy and Polish**

| Task | Owner | Estimate | Dependency | Priority |
|------|-------|----------|------------|----------|
| Insight drop system | BYTE | 2 days | Enemy death | P0 |
| Insight pickup implementation | BYTE | 1 day | Drop system | P0 |
| Insight UI (counter) | PIXEL | 2 days | Pickup | P0 |
| Insight spend (combat upgrades) | BYTE | 3 days | Insight UI | P0 |
| Internal playtest (combat feel) | REED | 2 days | All above | P0 |
| Bug fixes from playtest | BYTE | 5 days | Playtest | P0 |
| Polish pass (animations) | PIXEL | 4 days | Playtest | P1 |
| Polish pass (SFX) | ECHO | 2 days | Playtest | P1 |
| Prototype video recording | PIXEL | 1 day | Polish | P1 |
| Milestone 1 review meeting | CLOCK | 0.5 day | All above | P0 |

**Total committed: 22.5 days over 4 weeks (light sprint to allow buffer for playtest feedback)**

**Note:** This is a sample breakdown. Full sprint plan with all 52 sprints is tracked in a separate project management tool (Notion, Jira, or GitHub Projects).

---

## 4. Critical Path Visualization

The critical path is the sequence of tasks that, if delayed, will delay the entire project. In this project, the critical path runs through **animation production** in months 10-15.

```
PROJECT START (Month 0)
    ↓
[PROTOTYPE: Combat Loop] (Months 1-3)
    ↓ Depends on: BYTE (systems), PIXEL (placeholder animations)
[CORE SYSTEMS: Case Refraction] (Months 4-6)
    ↓ Depends on: BYTE (systems), NOVA (evidence content)
[VERTICAL SLICE: 2 Archetypes] (Months 7-9)
    ↓ Depends on: PIXEL (final animations for 2 archetypes) ← CRITICAL PATH STARTS
[CONTENT: Logic Archetype] (Months 10-12)
    ↓ Depends on: PIXEL (10 animations) ← ON CRITICAL PATH
[CONTENT: Electrochemistry Archetype] (Months 13-15)
    ↓ Depends on: PIXEL (10 animations) ← ON CRITICAL PATH
[POLISH: Animation Polish] (Months 16-18)
    ↓ Depends on: PIXEL (polish pass for all 40 animations) ← ON CRITICAL PATH
[SWITCH PORT: Optimization] (Months 19-21)
    ↓ Depends on: BYTE (porting), CRASH (QA)
[BETA: Testing] (Months 22-23)
    ↓ Depends on: CRASH (triage), BYTE (fixes)
[LAUNCH: Steam Release] (Month 24)
    ↓
PROJECT COMPLETE
```

**Why animation is the critical path:**
- PIXEL must deliver 40 unique animations (10 per archetype × 4 archetypes)
- Each animation requires: concept, sprite frames, rigging (if using Spine), export, integration, tuning
- Estimated 3-4 days per animation = 120-160 days of work
- PIXEL has ~480 working days across 24 months (20 days/month average)
- Animation consumes 25-33% of PIXEL's time (acceptable)
- But: If quality bar increases mid-project, or if animations require rework, this path extends
- No one else can unblock this — BYTE can't animate, NOVA can't animate

**Other potential critical paths (watch carefully):**
- **Case content authoring** (NOVA): 10 case branches, 100 evidence nodes, 15 dialogue trees
  - Estimated 22 weeks of work over 24 weeks (months 10-15)
  - Parallel with animation, so not strictly blocking, but high risk of overrun
- **Balance tuning** (REED): Ongoing in months 16-18
  - Can extend if Insight economy or combat balance is fundamentally broken
  - Mitigation: Early playtests (month 9 onward) catch issues before Polish phase

**Critical path mitigation strategies:**
1. **Parallelize non-dependent work** (BYTE builds systems while PIXEL animates)
2. **Front-load risky work** (animation quality validated in Milestone 3)
3. **External contractor budget** (if PIXEL falls behind, hire help)
4. **Cut scope early** (reduce from 4 archetypes to 3 if needed — do this in month 9, not month 18)

---

## 5. Risk Register

Risks are organized by likelihood and impact. Each risk has a mitigation strategy and a contingency plan.

**Risk scoring:**
- **Likelihood:** Low (10%), Medium (30-50%), High (70%+)
- **Impact:** Low (1 week delay), Medium (1 month delay), High (3+ months delay or budget overrun)

### Critical Risks (High Likelihood OR High Impact)

**Risk 1: Animation production overruns**
- **Likelihood:** High (70%)
- **Impact:** High (3+ month delay)
- **Why this is likely:** 40 animations across 4 archetypes. If each takes 5 days instead of 3, that's +80 days of work.
- **Mitigation:**
  - Lock animation list at Milestone 3 (no scope creep on animation count)
  - PIXEL validates animation pipeline in month 3-6 (prove 3-day turnaround is achievable)
  - Budget for external contractor (3 months, $15k-20k) starting month 12 if PIXEL is behind
- **Contingency:**
  - Cut Electrochemistry archetype (reduce to 3 archetypes, save 10 animations)
  - Reuse animations across archetypes where possible (idle/walk can be shared with recoloring)
  - Delay Switch port to post-launch, reallocate that time to animation
- **Owner:** CLOCK monitors weekly, PIXEL reports progress in sprint reviews

---

**Risk 2: Case Refraction feels random instead of meaningful**
- **Likelihood:** Medium (50%)
- **Impact:** High (core feature failure, requires redesign)
- **Why this is likely:** This is the game's USP. If psyche-based evidence filtering feels arbitrary, the entire premise collapses.
- **Mitigation:**
  - NOVA writes a one-sentence psychological rationale for every evidence node (e.g., "Authority sees bruises because Authority understands violence")
  - REED validates evidence-to-archetype mappings in design reviews
  - Playtest early (Milestone 3) and ask: "Why did you see this evidence and not that evidence?"
  - If 60%+ of playtesters can't articulate the psyche-evidence connection, redesign immediately
- **Contingency:**
  - Make evidence visibility more explicit (add UI tooltip: "Your AUTHORITY allows you to see this")
  - Reduce evidence variety (fewer nodes, but each one is more obviously psyche-linked)
  - In worst case: Make all evidence visible to all archetypes, but interpretation (case conclusion) still varies
- **Owner:** NOVA (content clarity) + REED (system design) + CLOCK (playtest coordination)

---

**Risk 3: Insight economy collapses (too generous or too punishing)**
- **Likelihood:** Medium (50%)
- **Impact:** Medium (1-2 months of balance iteration)
- **Why this is likely:** Balancing a dual-spend economy is hard. If players can afford both combat and narrative, tension is lost. If they can afford neither, frustration sets in.
- **Mitigation:**
  - REED starts tuning Insight drop rates and costs in Prototype phase (month 1-3)
  - Target feel: "I can afford 70% of what I want per run, must choose the other 30%"
  - Playtest metric: Ask "Did you feel the Insight choice was tense?" (target: 60%+ yes)
  - If economy is broken, 2-week balance sprint in month 10-11
- **Contingency:**
  - Increase Insight drops by 25% if too punishing
  - Increase costs by 25% if too generous
  - Add third spend channel (Psyche Echoes, already designed) to create more tension
- **Owner:** REED (balance lead) + BYTE (implements changes)

---

**Risk 4: Internal Voices feel annoying instead of characterful**
- **Likelihood:** High (60%)
- **Impact:** Medium (core mechanic may need redesign, 1-2 months)
- **Why this is likely:** Interrupting the player mid-combat is risky. If timing or frequency is off, players will resent it.
- **Mitigation:**
  - Playtest Internal Voice frequency in Milestone 3 (current design: 1 per room)
  - Metric: "Did Internal Voices feel annoying or interesting?" Target: <20% annoying
  - If >30% say annoying, reduce frequency to 1 per 2 rooms
  - Tune timing: Voices fire at moments of narrative relevance (near evidence, after elite kill) not on flat timers
- **Contingency:**
  - Reduce frequency to boss fights only (cut from regular combat)
  - Make Internal Voices optional (toggle in settings, but warn that this reduces narrative access)
  - In worst case: Cut Internal Voices entirely, move skill checks to debrief rooms only
- **Owner:** REED (design) + ECHO (audio stings) + NOVA (voice writing)

---

**Risk 5: Team burnout (crunch pressure leads to attrition)**
- **Likelihood:** Medium (40%)
- **Impact:** High (losing a team member mid-project = 3+ month delay)
- **Why this is likely:** 24-month timeline is aggressive for a 5-person team. If milestones slip, pressure to crunch builds.
- **Mitigation:**
  - No crunch policy enforced by CLOCK
  - If a milestone slips by 2+ weeks, cut scope immediately (don't extend hours)
  - Monthly check-ins with each team member (how are you feeling? what's blocking you?)
  - Build 20% slack into every sprint (don't over-commit)
- **Contingency:**
  - If someone needs time off (burnout, life event), delay milestone by 2-4 weeks rather than redistribute work
  - Cut scope before cutting people (e.g., reduce case branches from 10 to 8)
  - If someone leaves: Pause production for 2 weeks, reassess scope, potentially cut entire features
- **Owner:** CLOCK (team health monitoring)

---

**Risk 6: Godot Switch export has critical bugs**
- **Likelihood:** Low (20%)
- **Impact:** High (blocks Switch launch, lose platform revenue)
- **Why this could happen:** Godot 4.3's Switch export is official but relatively new. Edge cases or performance issues may not surface until late in development.
- **Mitigation:**
  - BYTE tests Switch export in month 15 (before Switch Port milestone starts)
  - Join Godot Discord/forums, monitor known Switch issues
  - Budget 3 months for Switch porting (months 19-21) specifically for unknowns
- **Contingency:**
  - If showstopper bugs found: Delay Switch launch to post-PC (month 25-26)
  - If bugs are unfixable: Cut Switch port entirely (PC-only launch)
  - Godot has strong community — if bugs found, report upstream and wait for patches
- **Owner:** BYTE (technical lead)

---

### Moderate Risks (Medium Likelihood AND Medium Impact)

**Risk 7: Performance degrades on Switch**
- **Likelihood:** Medium (50%)
- **Impact:** Medium (2-4 weeks of optimization)
- **Mitigation:** Profile early (month 15), reduce particles/textures proactively
- **Contingency:** Accept 30 FPS as standard (not just handheld), reduce enemy count by 20%

**Risk 8: Beta uncovers game-breaking bug**
- **Likelihood:** Medium (40%)
- **Impact:** Medium (2-4 week launch delay)
- **Mitigation:** Internal QA pass before beta (CRASH tests for 2 weeks)
- **Contingency:** Delay launch, communicate transparently with players

**Risk 9: Case content becomes contradictory/confusing**
- **Likelihood:** Medium (50%)
- **Impact:** Medium (2-4 weeks to rewrite/clarify)
- **Mitigation:** NOVA uses Evidence Graph Visualizer tool (built by BYTE in month 7-8)
- **Contingency:** Cut 2 case branches to reduce complexity

**Risk 10: Marketing underperforms (low wishlists, poor launch sales)**
- **Likelihood:** Medium (40%)
- **Impact:** Medium (doesn't delay launch, but affects revenue/sustainability)
- **Mitigation:** Steam page live by month 18, build wishlist base early, leverage Discord community
- **Contingency:** Post-launch marketing push, discounts, influencer outreach

---

### Low Risks (Noted for Completeness)

**Risk 11: Git merge conflicts in JSON files**
- **Likelihood:** High (70%)
- **Impact:** Low (annoying but not blocking)
- **Mitigation:** Split large JSON files, train team on Git basics

**Risk 12: Audio FMOD integration causes performance issues**
- **Likelihood:** Low (20%)
- **Impact:** Low (1 week to simplify)
- **Mitigation:** ECHO tests FMOD in month 10 with placeholder content

**Risk 13: Spine animation tool has learning curve**
- **Likelihood:** Medium (50%)
- **Impact:** Low (1-2 weeks for PIXEL to onboard)
- **Mitigation:** PIXEL trains on Spine in month 1-2 (during Prototype phase)

---

## 6. Scope Management

What's in v1.0, what's cut, and what's at risk of being cut if we fall behind.

### Locked In (Non-Negotiable)

These features define the game. If we cut these, we're not shipping REVACHOL NIGHTS.

1. **Four archetypes** (Authority, Empathy, Logic, Electrochemistry)
   - Each with unique combat kits
   - Each with unique evidence access
   - Each with unique Internal Voice signatures

2. **Case Refraction system** (psyche-based evidence filtering)
   - 6-10 case branches (see "at risk" below)
   - Evidence nodes tagged by archetype requirements
   - Case conclusions feel psychologically coherent

3. **Meta-case board** (cross-run persistence)
   - Evidence fragments persist
   - Connections auto-generate
   - Conspiracy layers unlock

4. **Insight economy** (single resource, dual spend)
   - Combat upgrades
   - Narrative unlocks
   - Tension between survival and understanding

5. **60 FPS combat on PC** (Dead Cells responsiveness standard)
   - Dodge i-frames
   - Attack animations feel weighty
   - Enemy telegraphs are readable

6. **PC (Steam) launch** (primary platform)

### Committed But At Risk

These features are in the plan, but if schedule slips or budget overruns, they're first on the chopping block.

1. **10 case branches** → Can cut to 6-8 if NOVA overruns
   - Each cut case branch saves 2 weeks of authoring + 1 week of integration
   - Minimum viable: 1 per dominant archetype (4 branches) + 2 hybrids (6 total)

2. **Nintendo Switch launch** → Can delay to post-PC if porting issues arise
   - If Switch port blocks PC launch, PC launches first
   - Switch follows in month 25-26 (after PC is stable)

3. **Electrochemistry archetype** → Can cut to 3 archetypes if animation overruns
   - Saves 10 animations + 2 weeks of integration
   - Weakens the "4 archetypes = 4 perspectives" design, but game is still coherent with 3

4. **Internal Voices mid-combat** → Can move to debrief-only if playtest feedback is negative
   - Reduces complexity, but loses the "fractured mind intruding on action" feel
   - Last resort cut

### Stretch Goals (v1.1 or Cut)

These are nice-to-haves. If we finish early (we won't), we add them. Otherwise, post-launch DLC or free updates.

1. **Psyche Blending** (lock sub-skills between runs)
   - Interesting mechanic, but adds complexity to psyche generation
   - Post-launch

2. **Partner NPC system** (rotating NPCs with their own psyche profiles)
   - Doubles narrative complexity (partner dialogue, combat AI, bond system)
   - Post-launch DLC candidate

3. **Revachol Radio** (adaptive in-game radio reacting to case progress)
   - Cool flavor, but non-essential
   - Post-launch

4. **Dream Sequences** (between-run hub in detective's subconscious)
   - Requires new environments, new art, new writing
   - Post-launch

5. **Rival Detective** (procedurally generated rival solving the same case)
   - Interesting but high-complexity AI
   - Post-launch

### Already Cut (Not in Scope)

These were considered during design but are definitively out for v1.0.

1. **Multiplayer/co-op** (the psyche system is single-player by design)
2. **More than one core case** (Lena Hargate only)
3. **Procedurally generated narrative** (all case branches are hand-authored)
4. **Voice acting for protagonist** (would triple budget and reduce narrative branching)
5. **Mobile ports** (combat requires precise input)
6. **Console ports other than Switch at launch** (PS5/Xbox post-launch only)

### Scope Change Authority

**Who can cut scope:**
- CLOCK can cut scope if schedule slips by 2+ weeks on critical path
- REED can propose cuts if playtesting reveals a feature is not fun
- NOVA can propose cuts if case complexity becomes unmanageable
- Team consensus required for cuts to "Locked In" features

**Who CANNOT unilaterally add scope:**
- No one. All new features require team vote + schedule impact analysis.
- "Wouldn't it be cool if..." is the enemy. The answer is always "yes, but not in v1.0."

**Scope freeze date:** End of Milestone 4 (month 15)
- After content production, no new features
- Only bug fixes, polish, and optimization

---

## 7. Communication and Reporting

### Weekly Sprint Rhythm

**Monday (Sprint Start):**
- Sprint planning meeting (1 hour)
- Each person commits to tasks for the next 2 weeks
- CLOCK updates project tracker (Notion/Jira/GitHub Projects)

**Tuesday-Thursday:**
- Async daily standups via Slack (15 min, written)
  - What did you do yesterday?
  - What are you doing today?
  - Any blockers?
- CLOCK monitors for blockers, escalates if needed

**Friday (Sprint End):**
- Sprint review (1 hour)
  - Each person demos completed work
  - Team provides feedback
  - Incomplete work moves to next sprint
- Sprint retro (30 min)
  - What went well?
  - What didn't?
  - Process improvements?
- CLOCK updates milestone tracker

### Monthly Milestones

**End of each month:**
- CLOCK sends milestone report to team (and stakeholders if applicable)
- Report includes:
  - Milestone progress (% complete)
  - Tasks completed this month
  - Tasks slipped or blocked
  - Risk updates (new risks, resolved risks)
  - Schedule forecast (are we on track for next milestone?)
  - Budget burn (how much spent vs. planned)

**Example format:**
```
MILESTONE REPORT: Month 10 (Content Production - Logic Archetype)

Progress: 75% complete (on track)

Completed:
- Logic archetype combat animations (10/10)
- Logic combat controller implementation
- 3 case branches authored

Slipped:
- Logic archetype signature ability VFX (moved to month 11)

Blockers:
- None

Risks:
- Animation quality bar increased mid-sprint (added 1 week to schedule)
- Mitigation: External contractor hired for Electrochemistry archetype

Schedule forecast: On track for Milestone 4 completion by end of month 15

Budget: $120k spent / $180k total salary budget (67% through project, 48% spent — healthy)
```

### Milestone Gates

**At the end of each milestone, CLOCK holds a milestone gate review:**
- Did we meet exit criteria? (yes/no, with evidence)
- Are there blockers to starting the next milestone?
- Do we need to cut scope before proceeding?
- Is the team healthy? (burnout check)

**If exit criteria NOT met:**
- Option 1: Extend milestone by 1-2 weeks (only if blockers are clear and fixable)
- Option 2: Cut scope and proceed to next milestone (preferred)
- Option 3: Pause and re-plan (only if fundamental issue found)

**Decision is made by CLOCK in consultation with team leads (REED, BYTE, NOVA, PIXEL).**

### External Communication

**To stakeholders/investors (if applicable):**
- Monthly milestone reports (high-level summary)
- Quarterly deep-dive meetings (progress, budget, risks)
- Immediate escalation if critical risk materializes

**To community/players:**
- Monthly devlog (starting month 9, after Vertical Slice)
- Announced via Discord, Twitter, Steam page updates
- Includes: GIFs, screenshots, feature highlights, no promises about ship dates

**To press:**
- First outreach at month 16 (when game is polished enough to show)
- Preview builds sent to select press at month 20 (4 months before launch)
- Review keys sent 2 weeks before launch

---

## 8. Success Metrics

How do we know if this production plan is working?

### Milestone Completion Rate

**Target:** 100% of milestones completed on time (within 1 week variance)

**Tracking:** CLOCK monitors at end of each milestone
- If milestone slips by 2+ weeks: Red flag, cut scope or reallocate resources
- If milestone is 1 week early: Rare but good, bank the time for later milestones

**Current forecast:** Based on industry averages for indie teams, expect 1-2 milestones to slip by 1-2 weeks. This is normal. The 24-month timeline includes buffer for this.

### Sprint Velocity

**Target:** 80% of committed tasks completed per sprint

**Tracking:** CLOCK measures at end of each sprint
- If velocity drops below 60% for 2 consecutive sprints: Team is overcommitted or blocked
- Action: Reduce commitments by 20% in next sprint, investigate blockers

**Velocity trends:**
- Expect lower velocity in months 1-3 (onboarding, learning Godot)
- Expect higher velocity in months 10-15 (team is experienced, systems are built)
- Expect lower velocity in months 22-24 (bug fixing, polish, launch prep is unpredictable)

### Playtest Satisfaction

**Target:** 70%+ positive sentiment from playtests

**Tracking:** Playtest surveys at Milestones 3, 5, 7
- Questions:
  - How fun is the combat? (1-10 scale)
  - Do you understand the psyche system? (yes/no)
  - Did the Insight choice feel meaningful? (yes/no)
  - Would you play this game again? (yes/no)

**Thresholds:**
- Combat fun <7/10 → Combat needs rework (delay if needed)
- Psyche understanding <50% → Add UI clarity, tutorial, or tooltips
- Insight choice not meaningful <40% → Economy rebalance required
- Would play again <60% → Core loop is broken, fundamental issue

### Budget Burn Rate

**Target:** Spend 50% of budget by month 12 (halfway point)

**Tracking:** CLOCK reviews monthly
- If spending ahead (60% by month 12): Risk of overrun, tighten spending
- If spending behind (40% by month 12): Team may be understaffed or inefficient

**Budget overrun triggers:**
- If forecasted to exceed $250k by 10% ($275k): Cut scope immediately
- If forecasted to exceed by 25% ($312k): Delay launch, seek additional funding, or cut entire features

### Team Health

**Target:** No voluntary attrition, no crunch

**Tracking:** CLOCK monthly check-ins
- Questions:
  - Are you working more than 40 hours/week? (red flag if yes)
  - How do you feel about the project? (1-10 scale)
  - What's your biggest frustration right now?

**Intervention triggers:**
- Anyone consistently over 45 hours/week → Immediate scope cut
- Team morale <6/10 for 2+ months → Process improvements or scope reduction
- Anyone expresses desire to leave → Pause, reassess, redistribute work

---

## 9. Tools and Infrastructure

**Project management:** Notion (or Jira, GitHub Projects)
- Milestone tracker
- Sprint boards
- Task assignments
- Risk register

**Version control:** Git + GitHub
- Code, art assets (via LFS), data (JSON)
- Branching strategy: `main` (stable), `dev` (active), feature branches

**Communication:**
- Slack (daily standups, quick questions)
- Discord (community management, external playtest coordination)
- Zoom (sprint planning, reviews, retros)

**Bug tracking:** GitHub Issues (or Jira)
- Priority levels: P0 (critical), P1 (high), P2 (medium), P3 (low)
- Tags: bug, feature request, polish, platform-specific

**Documentation:**
- Design docs: Markdown files in repo (`/docs/`)
- Meeting notes: Notion
- Playtest reports: Notion

**Build distribution:**
- Internal builds: Dropbox or Google Drive
- External playtest builds: Steam keys (unlisted branch)
- Beta builds: Steam keys (public beta branch)

---

## 10. CLOCK's Final Notes

This is the plan. It's not perfect. No plan survives contact with reality. But it's real. It's built on actual task estimates, actual team capacity, actual risk assessment.

**What's the MVP?** Two archetypes, one case, five districts, meta-case board. If we ship that in 18 months, we have a game. The other two archetypes and four case branches are v1.0 ambition. The Switch port is v1.1 fallback.

**When is this actually shipping?** 24 months. Not 18, not "when it's done." 24 months. If we're not feature-complete by month 15, we cut scope. If we're not in beta by month 22, we delay launch by 1-2 months maximum. After that, we ship what we have.

**What's the critical path?** Animation production. PIXEL is the bottleneck. If PIXEL falls behind by 4+ weeks, we hire external help or cut an archetype. We know this in month 12, not month 18.

**What could kill this project?** Scope creep. If NOVA writes 12 case branches instead of 10, we slip. If REED adds a fifth archetype "because it would be cool," we slip. If PIXEL raises the animation quality bar mid-production without cutting count, we slip. The answer to scope creep is always: cut scope, not corners.

**Cut scope, not corners.** We do not ship a game with 30 FPS combat because we ran out of time to optimize. We do not ship a game with broken case logic because we didn't test it. We do not ship a game where the psyche system feels random. If any of these are true at month 22, we delay launch or cut features. A delayed game is eventually good. A rushed game is forever mediocre.

**No one crunches.** If we cannot ship in 24 months at 40 hours/week per person, we cut scope. Crunch is a producer failure, not a badge of honor. I have managed crunch. People quit. The game was mediocre. We will not repeat that here.

**What happens if someone leaves?** We pause for 2 weeks, reassess scope, cut features. A 5-person team losing 1 person is a 20% capacity loss. We do not distribute that person's work to the other four. We cut 20% of scope.

**What happens if a milestone slips by 2+ weeks?** We cut scope immediately. We do not extend the timeline. We do not hope it gets better. We cut. The list of "at risk" features is pre-identified for this reason. We know what to cut and when.

**What happens if we finish early?** We bank the time for polish and QA. We do not add new features. We do not expand scope. We make what we have better.

**This plan is a contract.** The team commits to delivering what's "Locked In." CLOCK commits to protecting the team from scope creep and crunch. REED commits to balancing what we build, not dreaming about what we could build. NOVA commits to authoring 10 case branches, not 15. PIXEL commits to animating 40 animations, not 60. BYTE commits to shipping stable builds on two platforms.

**We ship in 24 months.** That's the plan.

---

**CLOCK, Producer**
**2026-02-07**

*Cut scope, not corners. When is this actually shipping? Month 24.*
