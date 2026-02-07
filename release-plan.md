# REVACHOL NIGHTS -- Release Plan

**Author**: SHIP, Release Manager
**Status**: Pre-Production Release Specification
**Version**: 1.0
**Date**: 2026-02-07

---

## 0. Executive Summary

This is the release plan. Not the marketing plan. Not the "wouldn't it be nice" plan. The **release plan** — the document that defines every step between "code complete" and "live on Steam."

Launch day is boring or it's a disaster. There is no in-between. This document makes it boring.

**Target Platforms:**
- **PC (Steam)** — Primary launch, Q4 2027
- **Nintendo Switch** — Secondary launch, Q1 2028 (3 months post-PC)

**Key Milestones:**
- Code freeze: 8 weeks before launch
- Gold master: 4 weeks before launch
- Steam store page live: 6 months before launch
- Review copies distributed: 3 weeks before launch
- Launch day: Hour-by-hour timeline, on-call rotation, rollback plan ready

**What's the rollback plan?** It's documented. Every step. If the build is broken, we revert to the last known-good build within 2 hours. If the store page is wrong, we have pre-approved backup screenshots. If the review embargo breaks early, we have a comms template ready.

First impressions are permanent. There are no second chances. Let's get it right.

---

## 1. Master Launch Checklist

This is the checklist. Every task has an owner, a deadline, and a verification step. If it's not on this list, it doesn't happen on launch day.

### 1.1 BUILD CHECKLIST

| Task | Owner | Deadline | Verification | Status |
|------|-------|----------|--------------|--------|
| **Code Freeze** | BYTE (Lead Programmer) | Launch -8 weeks | Final commit tagged as `v1.0-freeze` | [ ] |
| **Final Content Lock** | REED (Designer) + NOVA (Writer) | Launch -8 weeks | No new evidence nodes, dialogue, or case branches | [ ] |
| **Final Art Assets** | PIXEL (Art Director) | Launch -8 weeks | All sprites, animations, UI elements final | [ ] |
| **Final Audio Assets** | ECHO (Sound Designer) | Launch -8 weeks | All music stems, SFX, Internal Voice stings final | [ ] |
| **Platform Builds (PC: Win/Linux/Mac)** | BYTE | Launch -6 weeks | All three builds boot, reach main menu, complete one run | [ ] |
| **Switch Build (if approved)** | BYTE | Launch -6 weeks | Switch devkit build boots, 30 FPS stable in handheld | [ ] |
| **Performance Validation (PC)** | BYTE | Launch -5 weeks | 60 FPS on GTX 1050, no hitches during run transitions | [ ] |
| **Performance Validation (Switch)** | BYTE | Launch -5 weeks | 30 FPS minimum in handheld, 60 FPS in docked (if achievable) | [ ] |
| **Memory Profiling (PC)** | BYTE | Launch -5 weeks | <2GB runtime allocation, no leaks after 10 runs | [ ] |
| **Memory Profiling (Switch)** | BYTE | Launch -5 weeks | <1.5GB runtime allocation, no crashes after 5 runs | [ ] |
| **Save System Validation** | BYTE | Launch -4 weeks | Save/load works across 100+ runs, no corruption | [ ] |
| **Localization Check (if applicable)** | NOVA + External | Launch -4 weeks | All UI text displays correctly, no character encoding issues | [ ] |
| **Accessibility Pass** | CRASH (QA Lead) | Launch -4 weeks | Colorblind modes tested, text readability at 1080p+ | [ ] |
| **Gold Master Build (PC)** | BYTE | Launch -4 weeks | Final PC build, no post-gold changes except P0 bugs | [ ] |
| **Gold Master Build (Switch)** | BYTE | Launch -4 weeks | Final Switch build submitted to Lotcheck | [ ] |
| **Clean Machine Test (PC)** | CRASH | Launch -3 weeks | Install on 3 fresh Windows/Linux/Mac machines, verify no missing dependencies | [ ] |
| **Clean Machine Test (Switch)** | CRASH | Launch -3 weeks | Test on retail Switch hardware (not devkit) | [ ] |
| **Day One Patch Preparation** | BYTE | Launch -2 weeks | Hotfix build pipeline tested, patch can deploy in <2 hours | [ ] |
| **Build Signing (PC)** | BYTE | Launch -1 week | Windows build signed with valid certificate (no SmartScreen warnings) | [ ] |
| **Final Virus Scan (PC)** | BYTE | Launch -1 week | Upload to VirusTotal, verify 0 false positives | [ ] |
| **Steam Depot Upload** | SHIP | Launch -1 week | All platform builds uploaded to Steam, branches configured | [ ] |
| **Switch eShop Upload** | SHIP | Launch -1 week | Build uploaded to Nintendo Partner Center (if Lotcheck passed) | [ ] |

### 1.2 PLATFORM CONFIGURATION CHECKLIST

#### Steam (Steamworks)

| Task | Owner | Deadline | Verification | Status |
|------|-------|----------|--------------|--------|
| **Steamworks Account Created** | SHIP | Launch -12 months | Partner account active, Steam Direct fee ($100) paid | [ ] |
| **App ID Assigned** | SHIP | Launch -12 months | Unique Steam App ID reserved | [ ] |
| **Store Page Created** | HYPE (Marketing) + SHIP | Launch -6 months | Store page live in "coming soon" state | [ ] |
| **Store Page Assets Uploaded** | HYPE + PIXEL | Launch -6 months | Header capsule, library assets, screenshots (5+), trailer (2 min) | [ ] |
| **Store Page Text Finalized** | HYPE + NOVA | Launch -6 months | Short description, long description, feature list, system requirements | [ ] |
| **System Requirements Defined** | BYTE | Launch -6 months | Minimum: GTX 1050/8GB RAM. Recommended: GTX 1060/16GB RAM | [ ] |
| **Steam Achievements Configured** | SHIP + REED | Launch -4 months | 20-30 achievements, icons uploaded, API integration tested | [ ] |
| **Steam Cloud Saves Enabled** | BYTE | Launch -4 months | Save files sync via Steam Cloud, tested across 2 machines | [ ] |
| **Steam Trading Cards (Stretch)** | PIXEL + SHIP | Launch -3 months | 5-card set designed, approved by Valve (requires sales threshold) | [ ] |
| **Steam Controller Support** | BYTE | Launch -3 months | Full controller support verified (Xbox/PS/generic), no KB+M required | [ ] |
| **Steam Depot Branches Configured** | SHIP | Launch -2 months | `default` (public), `beta` (opt-in), `rollback` (emergency) | [ ] |
| **Steam Early Access (if applicable)** | HYPE + SHIP | Launch -6 months | Early Access store flag set, pricing tier defined | [ ] |
| **Steam Launch Discount Set** | HYPE + SHIP | Launch -2 weeks | 10-20% launch discount configured, dates locked | [ ] |
| **Steam Build Live** | SHIP | Launch Day, 10:00 AM PST | Default branch points to launch build, depot live | [ ] |

#### Nintendo Switch (eShop)

| Task | Owner | Deadline | Verification | Status |
|------|-------|----------|--------------|--------|
| **Nintendo Developer Account** | SHIP | Launch -18 months | Account approved, NDA signed, dev license active | [ ] |
| **Nintendo Switch SDK Access** | BYTE | Launch -18 months | SDK downloaded, Godot Switch export configured | [ ] |
| **Age Rating (IARC/ESRB/PEGI)** | SHIP | Launch -6 months | Game rated T (ESRB) / 16 (PEGI), certificate received | [ ] |
| **eShop Product Page Created** | HYPE + SHIP | Launch -4 months | Screenshots, trailer, description submitted to Nintendo Partner Center | [ ] |
| **Lotcheck Submission** | SHIP + BYTE | Launch -3 months | Build submitted to Lotcheck, test plan included | [ ] |
| **Lotcheck Pass** | SHIP | Launch -6 weeks | Lotcheck approved, no P1/P2 bugs remaining | [ ] |
| **eShop Pre-Orders (Optional)** | HYPE + SHIP | Launch -2 months | Pre-order page live, placeholder pricing set | [ ] |
| **eShop Launch Discount Set** | HYPE + SHIP | Launch -2 weeks | Discount configured, dates match PC launch window | [ ] |
| **eShop Build Live** | SHIP | Launch Day (Switch), 9:00 AM PST | Build visible in eShop, downloads start | [ ] |

### 1.3 STORE & MARKETING CHECKLIST

| Task | Owner | Deadline | Verification | Status |
|------|-------|----------|--------------|--------|
| **Trailer (Announce)** | HYPE + PIXEL + ECHO | Launch -6 months | 60-90 second trailer, psyche-reshuffle GIF prominent | [ ] |
| **Trailer (Launch)** | HYPE + PIXEL + ECHO | Launch -1 month | 90-120 second trailer, case refraction shown, review quotes (if available) | [ ] |
| **Press Kit Prepared** | HYPE | Launch -3 months | Fact sheet, screenshots, logos, trailer link, contact info | [ ] |
| **Press Outreach (Tier 1)** | HYPE | Launch -3 months | IGN, PC Gamer, Polygon, RPS contacted with review code offer | [ ] |
| **Press Outreach (Tier 2)** | HYPE | Launch -2 months | Indie-focused outlets (IndieGames, Siliconera, NintendoLife) contacted | [ ] |
| **Influencer Outreach** | HYPE | Launch -2 months | 10-15 streamers/YouTubers (roguelike audience) contacted | [ ] |
| **Review Copy Distribution** | SHIP + HYPE | Launch -3 weeks | Steam keys generated, embargo date communicated (Launch -1 week) | [ ] |
| **Review Embargo Enforcement** | HYPE | Launch -1 week | Embargo reminder sent, early review monitoring active | [ ] |
| **Social Media Campaign** | HYPE | Launch -3 months | Twitter/Discord weekly updates, psyche build showcases, GIFs | [ ] |
| **Discord Community Setup** | HYPE | Launch -6 months | Server live, roles configured, beta tester channel ready | [ ] |
| **Reddit Launch Thread** | HYPE | Launch Day, 11:00 AM PST | Post to r/roguelites, r/indiegaming, r/DiscoElysium | [ ] |
| **Launch Announcement (Steam)** | HYPE | Launch Day, 10:05 AM PST | Steam announcement post, changelog, launch discount mentioned | [ ] |

### 1.4 POST-LAUNCH MONITORING CHECKLIST

| Task | Owner | Deadline | Verification | Status |
|------|-------|----------|--------------|--------|
| **Steam Review Monitoring** | HYPE + CRASH | Launch +24 hours | Check every 4 hours, respond to P0 bug reports within 2 hours | [ ] |
| **Reddit/Discord Monitoring** | HYPE + CRASH | Launch +72 hours | Active in Discord, respond to tech support threads | [ ] |
| **Crash Report Triage** | BYTE + CRASH | Launch +24 hours | Steam crash dumps collected, P0 crashes prioritized | [ ] |
| **Day One Patch Decision** | BYTE + CLOCK | Launch +48 hours | If >5% crash rate, deploy hotfix. Otherwise, bundle fixes for Week 1 patch | [ ] |
| **Sales Data Review** | CLOCK + HYPE | Launch +1 week | Steam sales dashboard checked, compare to projections | [ ] |
| **Wishlist Conversion Analysis** | HYPE | Launch +1 week | What % of wishlists converted to sales? Benchmark: 15-25% | [ ] |
| **Review Score Tracking** | HYPE | Launch +2 weeks | Steam reviews (target: 85%+ positive), OpenCritic aggregate | [ ] |
| **Post-Launch Roadmap Communicated** | CLOCK + HYPE | Launch +1 week | Announce patch schedule, planned features (if any) | [ ] |

---

## 2. Build Pipeline Documentation

This section defines the build process from code freeze to gold master. Every step is documented. Every step is testable. If the build breaks, we know where.

### 2.1 Build Environment

**Primary Build Machine:**
- OS: Ubuntu 22.04 LTS (for CI/CD) + Windows 11 (for Windows signing)
- Godot Version: 4.3 (stable release, locked version)
- Export Templates: Godot 4.3 official export templates (Windows, Linux, macOS, Switch)
- Build Tools: Bash scripts, GitHub Actions, Steamworks CLI

**Build Dependencies:**
- Git LFS (for art assets)
- Godot export templates (pre-installed in CI environment)
- Windows Code Signing Certificate (for Windows build)
- Nintendo Switch SDK (for Switch build, requires NDA)

### 2.2 Build Steps (Automated)

**PC Build Pipeline (GitHub Actions)**

```yaml
# .github/workflows/release_build.yml
name: Release Build

on:
  push:
    tags:
      - 'v1.0-gold'
      - 'v1.0-patch-*'

jobs:
  build-pc:
    runs-on: ubuntu-latest
    container:
      image: barichello/godot-ci:4.3
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        with:
          lfs: true

      - name: Setup export templates
        run: |
          mkdir -p ~/.local/share/godot/templates
          cp -r /root/.local/share/godot/templates/4.3.stable ~/.local/share/godot/templates/

      - name: Build Windows
        run: |
          mkdir -p builds/windows
          godot --headless --export "Windows Desktop" builds/windows/revachol_nights.exe

      - name: Build Linux
        run: |
          mkdir -p builds/linux
          godot --headless --export "Linux/X11" builds/linux/revachol_nights.x86_64

      - name: Build macOS
        run: |
          mkdir -p builds/macos
          godot --headless --export "Mac OSX" builds/macos/revachol_nights.app.zip

      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: pc-builds
          path: builds/

  sign-windows:
    runs-on: windows-latest
    needs: build-pc
    steps:
      - name: Download Windows build
        uses: actions/download-artifact@v3
        with:
          name: pc-builds

      - name: Sign Windows executable
        run: |
          signtool sign /f ${{ secrets.CODE_SIGNING_CERT }} /p ${{ secrets.CERT_PASSWORD }} /tr http://timestamp.digicert.com /td sha256 /fd sha256 builds/windows/revachol_nights.exe

      - name: Upload signed build
        uses: actions/upload-artifact@v3
        with:
          name: windows-signed
          path: builds/windows/

  package-steam:
    runs-on: ubuntu-latest
    needs: [sign-windows, build-pc]
    steps:
      - name: Download all builds
        uses: actions/download-artifact@v3

      - name: Package for Steam
        run: |
          mkdir -p steam_upload
          cp -r windows-signed steam_upload/windows
          cp -r builds/linux steam_upload/linux
          cp -r builds/macos steam_upload/macos

      - name: Upload Steam package
        uses: actions/upload-artifact@v3
        with:
          name: steam-package
          path: steam_upload/
```

**Manual Steps (Post-CI):**

1. **Download Steam Package Artifact**
   - Download `steam-package.zip` from GitHub Actions
   - Extract to `steam_upload/` directory

2. **Upload to Steam via SteamCMD**
   ```bash
   steamcmd +login <username> +run_app_build ../scripts/steam_app_build_1001.vdf +quit
   ```

3. **Verify Steam Depot**
   - Log into Steamworks Partner Portal
   - Navigate to "Builds" section
   - Verify all three platform depots (Windows, Linux, macOS) are uploaded
   - Set default branch to new build

4. **Test Steam Build on Clean Machine**
   - Install on a Windows machine without dev environment
   - Launch via Steam client
   - Complete one full run (30-40 minutes)
   - Verify save system works
   - Exit and re-launch, verify save loads

### 2.3 Build Verification Checklist

**Every build must pass this checklist before being marked as "gold."**

| Check | Description | Pass/Fail |
|-------|-------------|-----------|
| **Boot Test** | Game boots to main menu within 10 seconds | [ ] |
| **Run Test** | Complete one full run (5 districts, case conclusion or death) without crashes | [ ] |
| **Save Test** | Save a run mid-district, quit, reload, verify state persists | [ ] |
| **Psyche Shuffle Test** | Start 5 runs, verify all 4 archetypes appear as dominant at least once | [ ] |
| **Performance Test** | Run District 5 (highest enemy count) at 60 FPS on target hardware | [ ] |
| **Audio Test** | Verify all 4 archetype music stems play, no clipping or silence | [ ] |
| **UI Test** | Navigate all menus (main, pause, debrief, meta-case board) without errors | [ ] |
| **Controller Test** | Complete one run using Xbox controller (no KB+M input) | [ ] |
| **Resolution Test** | Test at 1080p, 1440p, 4K (upscaled), verify UI scales correctly | [ ] |
| **Crash Test** | Alt-Tab during combat, verify no crash on return | [ ] |

### 2.4 Build Naming Convention

**Format:** `revachol_nights_v[VERSION]_[PLATFORM]_[BRANCH]`

**Examples:**
- `revachol_nights_v1.0.0_windows_default.exe` (Launch build)
- `revachol_nights_v1.0.1_windows_hotfix.exe` (Day one patch)
- `revachol_nights_v1.0.0_switch_default.nsp` (Switch launch build)

**Version Numbering:**
- **Major.Minor.Patch** (e.g., 1.0.0)
- Major: Full releases (1.0.0 = launch, 2.0.0 = major expansion)
- Minor: Content updates (1.1.0 = new case, new archetype)
- Patch: Bug fixes (1.0.1 = hotfix, 1.0.2 = week one patch)

---

## 3. Platform Configuration Checklists

### 3.1 Steamworks Setup (Complete)

**Store Page Configuration**

| Field | Content | Status |
|-------|---------|--------|
| **App Name** | Revachol Nights | [ ] |
| **Short Description** | A noir detective roguelite where your psyche is the build and the truth depends on who you are. | [ ] |
| **Long Description** | See Appendix A (full store page text) | [ ] |
| **Developer** | Parallax Studios | [ ] |
| **Publisher** | Parallax Studios (or external if signed) | [ ] |
| **Release Date** | Q4 2027 (exact date TBD 2 months before) | [ ] |
| **Pricing** | $19.99 USD (base price, regional pricing auto-adjusted) | [ ] |
| **Languages** | English (launch), French/German/Spanish (post-launch if sales justify) | [ ] |
| **Tags** | Roguelite, Detective, Noir, Action, Indie, 2D, Singleplayer, Psychological, Mystery, Atmospheric | [ ] |
| **Categories** | Single-player, Full Controller Support, Steam Achievements, Steam Cloud | [ ] |

**System Requirements**

| Spec | Minimum | Recommended |
|------|---------|-------------|
| **OS** | Windows 10 64-bit | Windows 11 64-bit |
| **Processor** | Intel i5-4460 / AMD FX-6300 | Intel i5-8400 / AMD Ryzen 5 2600 |
| **Memory** | 8 GB RAM | 16 GB RAM |
| **Graphics** | NVIDIA GTX 1050 / AMD RX 560 | NVIDIA GTX 1060 / AMD RX 580 |
| **DirectX** | Version 11 | Version 12 |
| **Storage** | 1 GB available space | 2 GB available space |
| **Additional** | Gamepad recommended | Gamepad recommended |

**Achievements (Planned)**

*20 achievements at launch, tied to meta-case progression and run challenges.*

| Achievement Name | Description | Rarity Target |
|-----------------|-------------|---------------|
| First Case Closed | Complete your first run | Common (95%) |
| All Four Faces | Unlock all 4 psyche archetypes as dominant | Common (80%) |
| Truth Seeker | Reach Meta-Case Layer 2 | Uncommon (60%) |
| Conspiracy Unveiled | Reach Meta-Case Layer 4 | Rare (30%) |
| The Final Accusation | Complete the meta-case (final ending) | Very Rare (15%) |
| Authority Specialist | Complete 10 runs with Authority as dominant | Uncommon (50%) |
| Empathy Specialist | Complete 10 runs with Empathy as dominant | Uncommon (50%) |
| Logic Specialist | Complete 10 runs with Logic as dominant | Uncommon (50%) |
| Electrochemistry Specialist | Complete 10 runs with Electrochemistry as dominant | Uncommon (50%) |
| Insight Hoarder | Finish a run with 50+ Insight unspent | Uncommon (40%) |
| Perfect Deduction | Complete a run without dying once | Rare (25%) |
| Voices Mastered | Pass 50 Internal Voice checks in a single run | Rare (20%) |
| Case Refraction | See all 10 case conclusions (across multiple runs) | Very Rare (10%) |
| Death is Progression | Die 100 times | Common (70%) |
| Marathon Detective | Complete 50 runs | Rare (20%) |
| Speedrunner | Complete a run in under 15 minutes | Very Rare (5%) |
| Pacifist Route | Complete a run using only Empathy charm/decoy (minimal combat) | Very Rare (3%) |
| Psyche Echo Collector | Accumulate 50 Psyche Echoes | Rare (25%) |
| Memory Anchor | Lock a sub-skill for a run using Psyche Echoes | Uncommon (60%) |
| Revachol's Finest | Complete the game on Moralist difficulty | Very Rare (2%) |

**Achievement Implementation:**
- Godot integration via GodotSteam plugin
- Achievement unlock code in `SaveManager.gd`
- Each achievement has a unique icon (64x64px, uploaded to Steamworks)

**Steam Cloud Saves**

| Setting | Value |
|---------|-------|
| **Cloud Save Enabled** | Yes |
| **Save File Path** | `user://revachol_nights_save.dat` |
| **Max Cloud Storage** | 10 MB (actual save files are <1 MB) |
| **Auto-Upload** | On game exit |

**Controller Support**

| Feature | Status |
|---------|--------|
| **Full Controller Support** | Yes (game playable without KB+M) |
| **Supported Controllers** | Xbox, PlayStation, Steam Controller, generic XInput |
| **Steam Input API** | Enabled (allows custom controller configs) |
| **Default Bindings** | A = Attack, B = Dodge, X = Interact, Y = Psyche Info, LB/RB = Sub-skill quick access |

**Trading Cards (Stretch Goal)**

*Requires 3-month sales threshold (per Valve policy). If eligible, configure 5-card set.*

| Card Name | Art Description |
|-----------|----------------|
| Authority | The detective silhouetted in red, baton raised |
| Empathy | The detective in blue, multiple ghostly echoes |
| Logic | The detective in gold, surrounded by wireframe evidence |
| Electrochemistry | The detective in green, motion-blurred, eyes wide |
| The Case Board | The meta-case board, threads connecting evidence |

### 3.2 Nintendo Switch eShop Setup

**eShop Product Page**

| Field | Content | Status |
|-------|---------|--------|
| **Title** | Revachol Nights | [ ] |
| **Short Description** | A noir detective roguelite where your psyche is the build. | [ ] |
| **Long Description** | See Appendix A (adapted for eShop character limits) | [ ] |
| **Developer** | Parallax Studios | [ ] |
| **Publisher** | Parallax Studios (or external) | [ ] |
| **Release Date** | Q1 2028 (3 months post-PC) | [ ] |
| **Pricing** | $19.99 USD (base price, regional pricing via Nintendo guidelines) | [ ] |
| **Languages** | English (launch) | [ ] |
| **Categories** | Action, Adventure, Indie | [ ] |
| **Rating** | T (ESRB) / 16 (PEGI) | [ ] |

**Switch-Specific Features**

| Feature | Status |
|---------|--------|
| **Handheld Mode** | Fully supported (720p, 30 FPS minimum) | [ ] |
| **Docked Mode** | Fully supported (1080p, 60 FPS target) | [ ] |
| **Joy-Con Support** | Full support (no motion controls) | [ ] |
| **Pro Controller Support** | Full support | [ ] |
| **Sleep Mode Handling** | Game pauses on sleep, resumes on wake without crash | [ ] |
| **Screenshot Feature** | Native Switch screenshot button enabled | [ ] |
| **Video Capture** | 30-second clips enabled (if performance allows) | [ ] |

**Lotcheck Submission Checklist**

*Nintendo's QA process. Typical turnaround: 2-4 weeks. Must pass before eShop release.*

| Requirement | Description | Status |
|-------------|-------------|--------|
| **Boot Time** | Game boots to title screen in <10 seconds (Lotcheck requirement) | [ ] |
| **Sleep/Wake Test** | Game handles sleep mode without crashes (tested 100x) | [ ] |
| **Battery Test** | Game does not drain battery faster than comparable titles | [ ] |
| **Performance Test** | No sustained FPS drops below 30 in handheld mode | [ ] |
| **Memory Test** | No memory leaks after 10+ runs | [ ] |
| **UI Readability** | All text readable in handheld mode (720p screen) | [ ] |
| **Controller Test** | All buttons functional, no unresponsive inputs | [ ] |
| **Error Handling** | Game does not soft-lock on corrupted save data | [ ] |
| **Age Rating Compliance** | No content exceeds T/16 rating (violence, language) | [ ] |
| **User Data Management** | Save data deletion works via Switch system menu | [ ] |

**Lotcheck Test Plan (Required Document)**

Submit to Nintendo with build:
- Expected playtime: 20-40 minutes per run, 30+ hours for meta-case completion
- Critical path: Start run -> complete 5 districts -> case conclusion -> meta-case board
- Save system: Auto-save after each district, manual save in precinct hub
- Known issues: None (if any P3/P4 bugs remain, list with workarounds)

---

## 4. Rollback and Hotfix Procedures

What's the rollback plan? This is it. If launch day goes wrong, we have procedures.

### 4.1 Rollback Scenarios

**Scenario 1: Critical Crash on Launch (>10% of players affected)**

**Symptoms:**
- Steam reviews report crashes on startup
- Crash reports show consistent stack trace (e.g., save file corruption, missing DLL)

**Rollback Procedure:**

1. **Identify Scope** (CRASH + BYTE, 15 minutes)
   - Check Steam crash dump reports
   - Verify crash is reproducible on clean machine
   - Determine if crash is platform-specific (Windows only?) or universal

2. **Decision: Rollback or Hotfix?** (BYTE + CLOCK, 15 minutes)
   - If fix can be deployed in <2 hours: Proceed to hotfix (Section 4.2)
   - If fix requires >2 hours: Rollback to last known-good build

3. **Execute Rollback** (SHIP, 30 minutes)
   - Log into Steamworks Partner Portal
   - Navigate to "Builds" section
   - Set default branch to previous build (e.g., `v1.0.0-beta-final`)
   - Publish change (live within 5 minutes)

4. **Communicate Rollback** (HYPE, 30 minutes)
   - Post Steam announcement: "We've temporarily reverted to a previous build while we fix a critical issue. Your saves are safe. Update coming within 4 hours."
   - Pin message in Discord
   - Tweet update

5. **Deploy Fix** (BYTE, 2-4 hours)
   - Fix bug in codebase
   - Build new version (`v1.0.1-hotfix`)
   - Test on clean machine (30-minute smoke test)
   - Upload to Steam
   - Set as default branch

6. **Post-Mortem** (BYTE + CRASH + CLOCK, within 24 hours)
   - Document what went wrong
   - Why did QA miss this?
   - Add test case to prevent recurrence

**Scenario 2: Store Page Error (Wrong Screenshots, Broken Trailer)**

**Symptoms:**
- Store page displays incorrect images
- Trailer link is broken or shows wrong video

**Rollback Procedure:**

1. **Immediate Fix** (SHIP, 10 minutes)
   - Log into Steamworks
   - Replace incorrect assets with backup assets (pre-approved by HYPE)
   - Publish store page changes (live within 5 minutes)

2. **Verify Fix** (HYPE, 5 minutes)
   - View store page in incognito browser
   - Confirm assets are correct

3. **Communicate (if needed)** (HYPE, 10 minutes)
   - If error was visible for >1 hour, post Steam announcement apologizing for confusion

**Scenario 3: Review Embargo Broken (Review Published Early)**

**Symptoms:**
- A review outlet publishes their review before embargo lift (Launch -1 week)

**Response Procedure:**

1. **Confirm Breach** (HYPE, 5 minutes)
   - Verify review is live and violates embargo agreement

2. **Contact Outlet** (HYPE, 15 minutes)
   - Email editor: "Your review was published before the agreed embargo date. Per our agreement, please take it down until [embargo date]."
   - CC: CLOCK (producer)

3. **Assess Damage** (HYPE + CLOCK, 30 minutes)
   - Is the review positive or negative?
   - Is it from a major outlet (IGN, Polygon) or minor (personal blog)?
   - Decision: escalate to legal or let it slide?

4. **Communicate to Other Outlets (if major breach)** (HYPE, 1 hour)
   - Email all review outlets: "We're aware of an early review. Embargo remains in effect for all others. Thank you for respecting the agreement."

5. **Adjust Marketing Plan** (HYPE, 2 hours)
   - If early review is very positive: amplify it in marketing (embargo breach becomes a non-issue)
   - If early review is very negative: prepare response FAQ for other outlets

**No Rollback Possible.** Embargo breaches cannot be undone. Containment and communication only.

### 4.2 Hotfix Deployment Procedure

**When to Deploy a Hotfix:**
- Critical crash affecting >5% of players
- Game-breaking bug preventing progression (e.g., meta-case board doesn't save)
- Exploit allowing infinite Insight or other economy breaks

**Hotfix Timeline: 2-4 Hours from Discovery to Live**

**Step 1: Identify and Fix (BYTE, 30-60 minutes)**
- Reproduce bug on local build
- Implement fix
- Test fix locally (10-minute smoke test)

**Step 2: Build Hotfix (BYTE, 15 minutes)**
- Tag commit as `v1.0.1-hotfix`
- Trigger CI/CD build (GitHub Actions)
- Download artifacts

**Step 3: Test Hotfix on Clean Machine (CRASH, 30 minutes)**
- Install on Windows machine without dev environment
- Reproduce original bug -> verify fix
- Play for 15 minutes to catch regressions

**Step 4: Upload to Steam (SHIP, 15 minutes)**
- Upload hotfix build to Steam via SteamCMD
- Set as default branch

**Step 5: Verify Live Deployment (SHIP, 10 minutes)**
- Download game via Steam on fresh machine
- Verify hotfix build is live

**Step 6: Communicate Hotfix (HYPE, 20 minutes)**
- Post Steam announcement: "Hotfix v1.0.1 is now live, fixing [specific issue]. Thanks for your patience."
- Pin Discord message
- Tweet update

**Step 7: Monitor (CRASH + HYPE, 4 hours)**
- Watch Steam reviews/discussions for reports of new issues
- If hotfix introduces new bugs, prepare rollback (back to Section 4.1)

**Hotfix Approval Authority:**
- BYTE (implements fix)
- CLOCK (approves deployment)
- SHIP (executes upload)

No hotfix deploys without all three confirming the fix is safe.

### 4.3 Emergency Contact List

**Launch Day On-Call Rotation (24-Hour Coverage)**

| Role | Name | Hours | Contact |
|------|------|-------|---------|
| **Lead Programmer** | BYTE | 8 AM - 8 PM PST | [phone/Discord] |
| **QA Lead** | CRASH | 8 AM - 8 PM PST | [phone/Discord] |
| **Producer** | CLOCK | 8 AM - 8 PM PST | [phone/Discord] |
| **Release Manager** | SHIP | 6 AM - 10 PM PST | [phone/Discord] |
| **Marketing** | HYPE | 8 AM - 8 PM PST | [phone/Discord] |
| **Night Shift (if needed)** | BYTE or CRASH | 8 PM - 8 AM PST | [phone] |

**Escalation Path:**
1. Bug reported on Steam/Discord
2. CRASH triages (P0/P1/P2/P3)
3. If P0 (critical crash/blocker): Immediately contact BYTE + SHIP
4. BYTE investigates, proposes fix or rollback
5. CLOCK approves action
6. SHIP executes
7. HYPE communicates

**Response Time SLAs:**
- **P0 (Critical):** Response within 30 minutes, fix or rollback within 4 hours
- **P1 (High):** Response within 2 hours, fix within 24 hours
- **P2 (Medium):** Response within 24 hours, fix in next patch
- **P3 (Low):** Logged for future patch

---

## 5. Launch Day Timeline (Hour-by-Hour)

Launch day is boring or it's a disaster. This timeline makes it boring.

**Launch Date:** TBD (Q4 2027, exact date set 2 months before)
**Launch Time:** 10:00 AM PST (1:00 PM EST, 6:00 PM GMT)

**Why 10:00 AM PST?**
- Avoids midnight launches (team needs to be awake for monitoring)
- Captures US East Coast lunch hour (high Steam traffic window)
- Allows EU evening playtime (6 PM GMT = post-work hours)

### Hour-by-Hour Schedule

**Launch Day -1 (Day Before)**

| Time (PST) | Task | Owner | Notes |
|------------|------|-------|-------|
| 9:00 AM | Final build verification | CRASH | Boot test, run test, save test on all platforms |
| 10:00 AM | Steam depot upload (final check) | SHIP | Verify default branch points to launch build |
| 11:00 AM | Store page final review | HYPE + SHIP | Check screenshots, trailer, pricing, discount |
| 12:00 PM | Review embargo reminder sent | HYPE | Email all outlets: "Embargo lifts tomorrow at 10 AM PST" |
| 2:00 PM | Discord announcement pinned | HYPE | "Launch tomorrow at 10 AM PST. See you then." |
| 3:00 PM | Team briefing call | CLOCK | Review launch timeline, confirm on-call rotation |
| 5:00 PM | Launch day prep complete | ALL | Go home. Get sleep. Tomorrow is the day. |

**Launch Day**

| Time (PST) | Task | Owner | Notes |
|------------|------|-------|-------|
| **7:00 AM** | Team online check-in | ALL | Discord: confirm everyone is awake and ready |
| **8:00 AM** | Steam build final verification | SHIP | Log into Steamworks, verify build is staged |
| **9:00 AM** | Store page final check | HYPE + SHIP | Verify launch discount is active, "coming soon" flag removed |
| **9:30 AM** | Press kit re-sent to Tier 1 outlets | HYPE | Final reminder: "Review embargo lifts in 30 minutes" |
| **9:45 AM** | Team standby | ALL | Everyone on Discord, ready for 10 AM switch flip |
| **10:00 AM** | **LAUNCH BUILD LIVE** | SHIP | Set Steam default branch to launch build, hit "Publish" |
| **10:01 AM** | Verify build is downloadable | SHIP | Install on clean machine via Steam, confirm it works |
| **10:05 AM** | Steam announcement posted | HYPE | "Revachol Nights is now live! 20% launch discount for the first week." |
| **10:05 AM** | Social media blitz | HYPE | Tweet, Discord announcement, Reddit post to r/roguelites |
| **10:10 AM** | Review embargo lifts | HYPE | Monitor review outlets, watch for early scores |
| **10:30 AM** | First player reports monitored | CRASH | Watch Steam discussions, Discord, Twitter for bug reports |
| **11:00 AM** | Reddit launch thread posted | HYPE | r/roguelites, r/indiegaming, r/DiscoElysium |
| **12:00 PM** | First hour sales check | CLOCK | Steamworks analytics: how many units sold in first hour? |
| **1:00 PM** | Lunch break (team rotates) | ALL | Half the team eats while half monitors |
| **2:00 PM** | Steam review monitoring begins | HYPE + CRASH | Check every review, respond to tech support questions |
| **4:00 PM** | First crash reports triaged | BYTE + CRASH | If any P0 bugs, initiate hotfix procedure |
| **6:00 PM** | End-of-day sales report | CLOCK | Share with team: "We sold X copies in first 8 hours." |
| **8:00 PM** | Day shift ends, night monitoring begins | BYTE (on-call) | Night shift: respond to critical bugs only |

**Launch Day +1 (Day After)**

| Time (PST) | Task | Owner | Notes |
|------------|------|-------|-------|
| 9:00 AM | Morning stand-up | ALL | Review overnight reports, any critical issues? |
| 10:00 AM | Steam review response | HYPE | Reply to top reviews (positive and constructive negative) |
| 12:00 PM | 24-hour sales report | CLOCK | Compare to projections, share with team |
| 2:00 PM | Hotfix decision meeting | BYTE + CLOCK + CRASH | Deploy day-one patch or wait for week-one patch? |
| 4:00 PM | Community FAQ updated | HYPE | Based on common player questions in Discord/Steam |
| 6:00 PM | Day +1 wrap-up | CLOCK | Team debrief: what went right, what went wrong? |

**Launch Week (Days 2-7)**

| Day | Task | Owner |
|-----|------|-------|
| Day 2 | Monitor Steam reviews, continue Discord moderation | HYPE + CRASH |
| Day 3 | Influencer coverage tracking (watch for streamers/YouTubers) | HYPE |
| Day 4 | Week-one patch decision: bundle all P1/P2 fixes | BYTE + CRASH |
| Day 5 | Deploy week-one patch (if needed) | BYTE + SHIP |
| Day 7 | Week-one sales report, compare to projections | CLOCK |
| Day 7 | Post-launch retrospective meeting | ALL |

---

## 6. Post-Launch Monitoring Plan

Launch day is day one. Post-launch is days 2-90. What do we watch? When do we act?

### 6.1 What to Watch

**Metrics (Checked Daily for First Week, Weekly After)**

| Metric | Source | Target/Benchmark | Action Threshold |
|--------|--------|------------------|------------------|
| **Units Sold** | Steamworks Dashboard | (Projection TBD based on wishlist count) | If <50% of projection by day 7, reassess marketing |
| **Wishlist Conversion Rate** | Steamworks | 15-25% industry average | If <10%, investigate (pricing issue? poor reviews?) |
| **Steam Review Score** | Steam Store Page | 85%+ positive | If <75%, investigate common complaints |
| **Refund Rate** | Steamworks | <10% industry average | If >15%, indicates serious quality issue |
| **Average Playtime** | Steamworks | 10+ hours (indicates meta-case engagement) | If <3 hours, players aren't reaching hook |
| **Crash Rate** | Steam Crash Reports | <1% of sessions | If >5%, deploy hotfix immediately |
| **Discord Activity** | Discord Analytics | 100+ messages/day in first week | Low activity = weak community engagement |
| **Reddit Mentions** | Manual Search | Positive mentions in r/roguelites | Negative mentions = PR issue to address |

**Qualitative Signals (Checked Multiple Times Daily)**

| Signal | Source | What to Look For | Action |
|--------|--------|------------------|--------|
| **Common Bug Reports** | Steam Discussions, Discord | Repeated reports of same issue | Triage as P0/P1, fix in hotfix or patch |
| **Confusion About Mechanics** | Steam Discussions, Discord | "I don't understand Case Refraction" | FAQ update, consider in-game tutorial patch |
| **Balance Complaints** | Steam Reviews, Reddit | "Electrochemistry is too hard" or "Authority is OP" | Log for balance patch, monitor frequency |
| **Positive Feedback Themes** | Steam Reviews, Twitter | "The psyche reshuffle is brilliant" | Amplify in marketing, quote in social posts |
| **Negative Feedback Themes** | Steam Reviews, Reddit | "Internal Voices are annoying" | Assess frequency, consider tuning in patch |

### 6.2 When to Act

**Hotfix Triggers (Deploy Within 4 Hours)**
- Crash rate >5%
- Save corruption reports from multiple users
- Game-breaking progression bug (meta-case doesn't unlock)
- Exploit allowing infinite Insight or similar economy break

**Week-One Patch Triggers (Deploy Within 7 Days)**
- 3+ P1 bugs confirmed
- 10+ P2 bugs confirmed
- Balance issues reported by >20% of reviews
- Performance issues on common hardware (GTX 1050 drops below 60 FPS)

**Month-One Patch Triggers (Deploy Within 30 Days)**
- 10+ P2 bugs confirmed
- 30+ P3 bugs confirmed
- Quality-of-life requests from community (e.g., "add colorblind mode")
- Balance tuning based on aggregate playtesting data

**No Patch Triggers (Log for Future Consideration)**
- P3 bugs with easy workarounds
- Feature requests outside original scope
- Localization requests (queue for post-launch if sales justify)

### 6.3 Post-Launch Communication Plan

**Cadence:**
- **First 48 Hours:** Update Discord/Steam every 4 hours with status (even if status is "all good")
- **First Week:** Daily update post summarizing bugs fixed, patch status
- **First Month:** Weekly update post with patch notes, roadmap (if applicable)
- **After Month 1:** Updates as patches deploy, no fixed cadence

**Communication Templates (Pre-Written)**

**Template 1: Hotfix Deployed**
```
HOTFIX v1.0.1 NOW LIVE

We've deployed a hotfix addressing the following critical issues:
- [Bug 1 description]
- [Bug 2 description]

If you're still experiencing issues, please let us know in the Steam discussions or our Discord.

Thank you for your patience, detectives.
```

**Template 2: Known Issue Acknowledgment**
```
KNOWN ISSUE: [Bug Description]

We're aware of [issue]. Our team is investigating. Expected fix: [hotfix/week-one patch/month-one patch].

Workaround (if available): [steps]

We'll update you as soon as we have more information.
```

**Template 3: Week-One Patch Announcement**
```
WEEK-ONE PATCH v1.0.2 LIVE

Thank you for an incredible first week. Here's what we've fixed:

BUG FIXES:
- [List of bugs]

BALANCE CHANGES:
- [List of balance tweaks]

QUALITY OF LIFE:
- [List of QOL improvements]

Full patch notes: [link]

Your feedback has been invaluable. Keep it coming.
```

### 6.4 Community Management Guidelines

**Steam Discussions**
- HYPE and CRASH monitor daily
- Respond to tech support threads within 4 hours (business hours)
- Do NOT engage with hostile/toxic posts (report to Steam moderators)
- Pin FAQ thread covering common questions

**Discord**
- Dedicated channels: #tech-support, #feedback, #bug-reports, #general
- HYPE and CRASH moderate, with volunteer community mods after week 1
- Respond to bug reports within 2 hours
- Weekly "State of the Game" post summarizing patch status

**Reddit**
- HYPE monitors r/roguelites, r/indiegaming, r/DiscoElysium
- Respond to major threads (>100 upvotes) within 24 hours
- Do NOT argue with negative reviews; acknowledge feedback professionally

**Twitter**
- HYPE posts updates, patch notes, community highlights
- Retweet positive player experiences, fan art, streamer clips
- Respond to @ mentions within 24 hours (business hours)

---

## 7. Age Rating and Compliance

### 7.1 ESRB Rating (North America)

**Expected Rating:** T (Teen, 13+)

**Content Descriptors:**
- Violence (combat, noir detective themes)
- Blood (minimal, stylized)
- Mild Language (noir dialogue, no F-bombs)
- Use of Alcohol and Drugs (Electrochemistry archetype references substance use)

**Rating Process:**
- Submit game build + content questionnaire to ESRB 3 months before launch
- Provide 1-hour gameplay video showing all content types
- Typical turnaround: 1-2 weeks
- Cost: ~$800 for digital-only release

**Compliance Notes:**
- No graphic violence (stylized 2D combat, no gore)
- Drug references are thematic, not glorified (Electrochemistry is framed as risky)
- Language stays within T rating (no F-word, minimal strong profanity)

### 7.2 PEGI Rating (Europe)

**Expected Rating:** PEGI 16

**Content Descriptors:**
- Violence
- Bad Language
- In-Game Purchases (if post-launch DLC planned)

**Rating Process:**
- Submit to IARC (International Age Rating Coalition) via console submission portals
- IARC auto-generates PEGI, ESRB, and other regional ratings
- Cost: Included in platform fees (Steam, Nintendo)
- Turnaround: Immediate (automated system)

**Compliance Notes:**
- PEGI is stricter than ESRB for drug references; PEGI 16 is appropriate
- No changes to content needed for PEGI compliance

### 7.3 Other Regional Ratings

**Australia (ACB):** Expected MA15+ (Mature Accompanied)
**Germany (USK):** Expected USK 16
**Japan (CERO):** Expected CERO C (15+)

**Strategy:** Use IARC system to auto-generate all regional ratings. No separate submissions needed unless targeting physical retail (not planned for v1.0).

### 7.4 Content Compliance Checklist

| Compliance Area | Requirement | Status |
|----------------|-------------|--------|
| **Violence** | No graphic gore, no realistic depictions of injury | [ ] |
| **Language** | No F-word, minimal strong profanity (damn, hell OK) | [ ] |
| **Sexual Content** | None (not applicable to this game) | [ ] |
| **Drug References** | Thematic only, not glorified, fits noir genre | [ ] |
| **Gambling** | None (RNG is gameplay mechanic, not gambling) | [ ] |
| **User-Generated Content** | None (single-player, no UGC systems) | [ ] |
| **Online Interactions** | None (no multiplayer, no chat) | [ ] |
| **In-Game Purchases** | None at launch (DLC possible post-launch) | [ ] |

---

## 8. Review Copy and Embargo Management

### 8.1 Review Copy Distribution

**Target Outlets (Tier 1 - Priority)**

| Outlet | Contact | Notes |
|--------|---------|-------|
| IGN | [email] | Major reach, roguelike audience |
| PC Gamer | [email] | PC-focused, covers indies |
| Polygon | [email] | Narrative-focused, Disco Elysium comparisons likely |
| Rock Paper Shotgun | [email] | UK-based, strong indie coverage |
| Eurogamer | [email] | EU reach, covers detective games |
| GameSpot | [email] | Major reach, video review likely |

**Target Outlets (Tier 2 - Indie-Focused)**

| Outlet | Contact | Notes |
|--------|---------|-------|
| IndieGames.com | [email] | Pure indie focus |
| Siliconera | [email] | Niche/quirky games |
| NintendoLife | [email] | Switch coverage (if Switch launch concurrent) |
| Destructoid | [email] | Enthusiast audience |
| GamesRadar+ | [email] | Broad coverage |

**Target Influencers (Streamers/YouTubers)**

| Creator | Platform | Audience | Notes |
|---------|----------|----------|-------|
| NorthernLion | Twitch/YouTube | 1M+ (roguelike specialist) | Key influencer for genre |
| Wanderbots | YouTube | 500K+ (indie games) | Covers detective/mystery games |
| Retromation | Twitch/YouTube | 300K+ (roguelikes) | Daily roguelike content |
| Aliensrock | YouTube | 1M+ (puzzle/strategy) | Logic-focused audience |
| [5-10 more creators TBD] | | | |

**Review Code Distribution Timeline**

| Milestone | Date | Action |
|-----------|------|--------|
| **Review Code Batch 1** | Launch -3 weeks | Tier 1 outlets (6-10 codes) |
| **Review Code Batch 2** | Launch -2 weeks | Tier 2 outlets (10-15 codes) |
| **Influencer Codes** | Launch -2 weeks | 10-15 streamers/YouTubers |
| **Embargo Reminder** | Launch -1 week | Email all recipients: "Embargo lifts [date/time]" |
| **Embargo Lift** | Launch Day, 10:00 AM PST | Reviews go live |

**Review Code Generation (Steam)**
- Generate 50 Steam keys via Steamworks (cost: $0, keys deducted from sales count)
- Track code assignments in spreadsheet: [Outlet, Contact, Code, Date Sent, Review Published?]

### 8.2 Embargo Policy

**Embargo Date:** Launch Day, 10:00 AM PST (same time as public launch)

**Why Launch-Day Embargo?**
- Avoids early negative reviews killing pre-launch buzz
- Allows outlets to publish alongside launch for maximum traffic
- Aligns review coverage with launch discount window

**Embargo Agreement (Email Template)**

```
Subject: Revachol Nights Review Code - Embargo Info

Hi [Contact Name],

Thank you for your interest in covering Revachol Nights! Attached is your Steam key for review purposes.

EMBARGO DETAILS:
- Review Embargo Lifts: [Launch Date], 10:00 AM PST / 1:00 PM EST / 6:00 PM GMT
- You may publish your review, video, or coverage at or after this time.
- Streaming/video content before embargo: Please check with us first.

GAME INFO:
- Genre: Noir detective roguelite
- Playtime: 20-40 min per run, 30+ hours for full meta-case
- Key Hook: Your psyche is your build, and the truth changes with it.
- Press Kit: [link]

If you have questions or need assets, contact [HYPE email].

Thank you, and we look forward to your coverage!

Best,
[SHIP/HYPE signature]
Parallax Studios
```

**Embargo Enforcement**
- No legal penalties for breaking embargo (not enforceable)
- Consequence: Outlet removed from future review code lists
- If major outlet breaks embargo, assess response per Section 4.1 (Rollback Procedures)

### 8.3 Press Kit Contents

**Press Kit URL:** [website.com/press] (hosted 6 months before launch)

**Contents:**
- **Fact Sheet** (PDF)
  - Game title, developer, publisher, platforms, release date, pricing
  - Genre, key features, elevator pitch
  - Links to trailer, screenshots, logo pack
- **Screenshots** (10+ high-res PNG, 1920x1080)
  - Combat (all 4 archetypes showcased)
  - Meta-case board
  - Precinct hub
  - Dialogue/Internal Voice example
  - Case refraction moment (evidence glowing in archetype color)
- **Trailer** (2 minutes, MP4 + YouTube link)
  - 60-second version for social media
  - 90-second version for store pages
- **Logos** (PNG, transparent background)
  - Game logo (full color, white, black)
  - Studio logo
- **Key Art** (high-res, 4K)
  - Hero image: Detective silhouette with four archetype reflections
- **Developer Bios** (REED, NOVA, BYTE, PIXEL, ECHO bios, 100 words each)
- **Contact Info**
  - Press inquiries: [HYPE email]
  - General inquiries: [studio email]

---

## 9. Risk Assessment and Contingency Plans

What could go wrong? Everything. What's the plan for each? Here.

### 9.1 Launch Day Risks

**Risk 1: Steam Servers Down at Launch Time**

**Likelihood:** Low (Valve infrastructure is stable)
**Impact:** High (cannot launch on schedule)

**Contingency:**
- Monitor Valve's status page starting at 9:00 AM PST
- If Steam is down at 10:00 AM, delay launch by 1 hour increments
- Communicate delay immediately via Twitter/Discord: "Steam is experiencing issues. Launch delayed to [new time]. We'll keep you updated."
- If Steam is down for >4 hours, postpone launch by 24 hours

---

**Risk 2: Critical Bug Discovered at 9:00 AM (1 Hour Before Launch)**

**Likelihood:** Medium (QA is thorough, but bugs slip through)
**Impact:** Critical (cannot launch broken build)

**Contingency:**
- CRASH and BYTE assess severity (15 minutes)
- If P0 bug: Delay launch, deploy hotfix, reschedule for +24 hours
- If P1 bug with workaround: Launch on schedule, post workaround in Steam announcement, deploy patch within 48 hours
- Communicate delay via all channels if launch is postponed

---

**Risk 3: Review Embargo Broken by Major Outlet (IGN, Polygon, etc.)**

**Likelihood:** Low (major outlets respect embargoes)
**Impact:** Medium (early negative review could dampen launch)

**Contingency:**
- See Section 4.1 (Rollback Procedures, Scenario 3)
- Contact outlet, request takedown
- If review is positive: amplify it in marketing
- If review is negative: prepare FAQ addressing concerns

---

**Risk 4: Influencer Posts Negative Video at Launch**

**Likelihood:** Medium (cannot control influencer opinions)
**Impact:** Medium (negative video with large reach hurts sales)

**Contingency:**
- HYPE monitors YouTube/Twitch for coverage
- If negative video highlights legitimate issues: acknowledge in community post, commit to patch
- If negative video is based on misunderstanding: politely reach out to creator with clarification, offer to discuss
- Do NOT argue publicly or brigade negative content (damages reputation further)

---

**Risk 5: High Refund Rate (>15%) in First 48 Hours**

**Likelihood:** Low (if QA is thorough)
**Impact:** High (indicates serious quality issue + financial loss)

**Contingency:**
- CRASH reviews refund reasons via Steamworks (if available)
- Common refund reason: crashes -> hotfix immediately
- Common refund reason: "not fun" -> investigate via reviews/Discord, assess if design issue or expectations mismatch
- If refund rate >20%, consider temporary discount increase to offset loss

---

**Risk 6: Switch Lotcheck Fails 1 Week Before Planned Switch Launch**

**Likelihood:** Medium (Lotcheck is strict)
**Impact:** High (delays Switch launch by 4-6 weeks)

**Contingency:**
- Switch launch is already planned for +3 months post-PC (Q1 2028)
- If Lotcheck fails, delay Switch launch to Q2 2028
- Communicate delay via Twitter/Discord: "Switch version delayed to ensure quality. PC version unaffected."
- Use extra time to address Lotcheck issues, re-submit

---

**Risk 7: Sales Significantly Below Projections (Week 1)**

**Likelihood:** Medium (market is unpredictable)
**Impact:** Medium-High (financial pressure, marketing budget exhausted)

**Contingency:**
- CLOCK and HYPE review marketing spend vs. return
- If sales are <50% of projection: increase discount (20% -> 30%), extend discount duration (1 week -> 2 weeks)
- Reach out to influencers who haven't covered yet with free codes
- Post-launch content tease (free update, new case, etc.) to generate buzz
- Assess if pricing is issue ($19.99 -> $14.99 price drop after 1 month)

---

### 9.2 Post-Launch Risks

**Risk 8: Negative Review Bomb (Coordinated Negative Reviews)**

**Likelihood:** Low (game is single-player, no controversial DRM/political content)
**Impact:** Medium (hurts Steam review score, discourages purchases)

**Contingency:**
- Identify if review bomb is legitimate (bug/issue) or coordinated attack
- If legitimate: address issue in patch, post response
- If coordinated attack: report to Steam (Valve has review bomb detection)
- Do NOT engage with review bombers directly (feeds the fire)

---

**Risk 9: Exploit Discovered (Infinite Insight, Duplication Glitch, etc.)**

**Likelihood:** Medium (players find creative exploits)
**Impact:** Medium (breaks game economy, but single-player = lower stakes)

**Contingency:**
- BYTE investigates exploit, implements fix
- Deploy hotfix within 48 hours
- Post community announcement: "We've fixed an exploit. If you used it, your save is still valid—no punishment. It's a single-player game."
- Do NOT punish players for exploits in single-player games (bad PR)

---

**Risk 10: Key Reseller Sites (G2A, etc.) Selling Stolen Keys**

**Likelihood:** Low (if key distribution is carefully tracked)
**Impact:** Medium (financial loss, reputation damage)

**Contingency:**
- Monitor key reseller sites for suspicious listings
- Revoke stolen keys via Steamworks
- Post warning: "Only buy from official sources (Steam, eShop). Keys from unauthorized resellers may be revoked."
- Track all review/influencer codes to identify source of stolen keys

---

## 10. Success Metrics and Post-Launch Goals

What does success look like? Define it. Measure it.

### 10.1 Success Metrics (Launch Window: First 30 Days)

| Metric | Target (Conservative) | Target (Optimistic) | Actual | Notes |
|--------|----------------------|---------------------|--------|-------|
| **Units Sold (PC)** | 10,000 | 25,000 | [ ] | Based on wishlist conversion + marketing reach |
| **Wishlist Conversion** | 15% | 25% | [ ] | Industry average: 15-20% |
| **Steam Review Score** | 80% Positive | 90% Positive | [ ] | "Very Positive" or higher |
| **Average Playtime** | 8 hours | 15 hours | [ ] | Indicates meta-case engagement |
| **Refund Rate** | <10% | <5% | [ ] | Lower = better quality perception |
| **Revenue (PC, net of Valve cut)** | $140K | $350K | [ ] | $19.99 base price, 30% Valve cut |
| **Streamer/YouTube Coverage** | 10 videos | 30 videos | [ ] | Major influencer coverage |
| **Discord Members** | 500 | 1,500 | [ ] | Community size indicator |

### 10.2 Post-Launch Goals (First 90 Days)

**Short-Term Goals (Month 1)**
- Maintain "Very Positive" Steam review score
- Deploy 1-2 patches addressing P1/P2 bugs
- Reach 15K units sold (PC)

**Medium-Term Goals (Month 2-3)**
- Switch launch (if Lotcheck passed)
- Deploy balance patch based on community feedback
- Reach 25K total units sold (PC + Switch)

**Long-Term Goals (Month 4-6)**
- Evaluate post-launch content (new case, new archetype, etc.) based on sales performance
- If sales justify: announce DLC or free content update
- If sales underperform: focus on community engagement, sales during seasonal events

### 10.3 Post-Launch Roadmap (Tentative)

**Month 1 Post-Launch:**
- Week 1 Patch: Bug fixes, balance tweaks
- Week 4 Patch: Quality-of-life improvements (e.g., colorblind mode, rebindable keys)

**Month 2 Post-Launch:**
- Switch Launch (if Q1 2028 timeline holds)
- PC Patch: Performance optimizations based on player hardware data

**Month 3+ Post-Launch:**
- Evaluate DLC (new case, new archetype) if sales >20K units
- Evaluate localization (French, German, Spanish) if sales >30K units
- Evaluate console ports (PS5, Xbox) if sales >50K units

**Stretch Goal: Year-One Anniversary Update**
- Free content update (new case, new meta-case layer, or new difficulty mode)
- Anniversary sale (50% off)
- Community event (speedrun competition, fan art showcase)

---

## 11. Appendix A: Full Store Page Text (Steam)

**Short Description** (300 characters max)
```
A noir detective roguelite where your psyche is the build and the truth depends on who you are. Every death reshuffles your personality—and the murder you're solving changes with it.
```

**Long Description** (Full HTML, ~1000 words)
```
EVERY TIME YOU DIE, YOUR PERSONALITY RESHUFFLES—AND THE MURDER CHANGES WITH IT.

You are a detective in Revachol, a city where every revolution failed and the rain never stops. You're solving the murder of Lena Hargate. The problem? Every time you die, your psyche fractures and reassembles in a new configuration—and the truth you're chasing changes with it.

YOUR PSYCHE IS YOUR BUILD

Forget skill trees. Your personality IS your loadout. Four archetypes—Authority, Empathy, Logic, Electrochemistry—determine your combat abilities, your evidence access, and your dialogue options. Every run deals you a different psychological profile. Every profile sees a different truth.

- AUTHORITY: Heavy melee, crowd control, power-based evidence. You see the case as a struggle for dominance.
- EMPATHY: Evasion, enemy telegraphs, emotional evidence. You see the case as a tragedy of broken relationships.
- LOGIC: Ranged attacks, environmental traps, forensic evidence. You see the case as a puzzle to be solved.
- ELECTROCHEMISTRY: Speed, combos, risky rewards, substance-related evidence. You see the case as chaos barely contained.

CASE REFRACTION: THE TRUTH IS SUBJECTIVE

The same murder. Four different killers. All of them are right.

Case Refraction means the evidence you can perceive depends on your psyche. An Authority-dominant run sees bruises and power struggles. An Empathy-dominant run sees micro-expressions and fear. The murder doesn't change. Your lens does. And every lens reveals a truth the others cannot see.

ONE RESOURCE, TWO HUNGERS

Insight is the currency of survival and understanding. Spend it on combat upgrades to survive deeper districts, or spend it on interrogations and evidence analysis to uncover the case. You cannot afford both. Every safe room is a gut-check: Are you a detective or a survivor?

THE META-CASE: A CONSPIRACY ACROSS RUNS

Across dozens of runs, a larger pattern emerges. Contradictory conclusions from different psyche builds start to connect. A conspiracy board in your precinct accumulates evidence fragments, witness statements, and impossible truths. The real question isn't who killed Lena Hargate. It's why the truth keeps changing—and what that reveals about you.

FEATURES

- 4 Psyche Archetypes with 24 sub-skills, creating hybrid builds every run
- Dead Cells-tier 2D combat with archetype-specific verbs and combos
- Case Refraction system: the mystery is real, the truth is subjective
- Internal Voices: mid-combat psychological interruptions (Disco Elysium meets action)
- 20-40 minute run loops with meta-progression across runs
- 10 authored case conclusions, each psychologically coherent
- Lo-fi noir aesthetic: CRT scanlines, 2000s nostalgia, rain-soaked neon
- Archetype-reactive music (stems shift with your dominant psyche)
- Full controller support

REVACHOL NIGHTS is for players who love roguelites but crave narrative depth. If you've put 200 hours into Dead Cells or Hades and wished the story hit harder, this is your game. If you've loved Disco Elysium but wanted something you could play in 30-minute sessions, this is your game.

First impressions are permanent. The city remembers. The case never closes.

Who are you this time, detective?
```

**Feature List (Bullet Points)**
- Psyche-Based Combat: 4 archetypes, 24 sub-skills, hybrid builds every run
- Case Refraction: The truth changes with your psychological profile
- Tight 2D Action: Dead Cells-tier responsiveness with archetype-specific combat
- Meta-Progression: Cross-run conspiracy board tracking contradictory truths
- Internal Voices: Mid-combat skill checks that interrupt the action
- Noir Aesthetic: Rain-soaked city, CRT scanlines, 2000s tech nostalgia
- Archetype-Reactive Music: Layered stems shift with your dominant psyche
- 20-40 Minute Runs: Perfect for roguelike veterans and session-based play
- 10 Case Conclusions: Every ending is authored, every truth is valid
- Full Controller Support: Play with keyboard+mouse or gamepad

---

## 12. Appendix B: Launch Day Checklist (Printable)

**LAUNCH DAY CHECKLIST**
**Date:** [TBD]
**Launch Time:** 10:00 AM PST

### PRE-LAUNCH (9:00 AM - 10:00 AM)

- [ ] Team online and standing by (Discord check-in)
- [ ] Steam build verified (SHIP logs into Steamworks)
- [ ] Store page final check (HYPE + SHIP: discount active, screenshots correct)
- [ ] Press kit re-sent to Tier 1 outlets (HYPE)
- [ ] Social media posts scheduled (HYPE: Twitter, Discord, Reddit queued)

### LAUNCH (10:00 AM)

- [ ] **SET STEAM BUILD LIVE** (SHIP: default branch -> launch build, hit Publish)
- [ ] Verify build is downloadable (SHIP: install on clean machine)
- [ ] Steam announcement posted (HYPE: "We're live!")
- [ ] Social media blitz (HYPE: Twitter, Discord, Reddit)

### POST-LAUNCH (10:00 AM - 6:00 PM)

- [ ] Monitor Steam discussions (CRASH + HYPE: every 30 minutes)
- [ ] Monitor Discord #tech-support (CRASH: respond within 2 hours)
- [ ] Monitor crash reports (BYTE: triage any P0 bugs)
- [ ] First-hour sales check (CLOCK: Steamworks analytics at 11:00 AM)
- [ ] Reddit launch thread posted (HYPE: r/roguelites at 11:00 AM)
- [ ] Steam review responses (HYPE: reply to top reviews by 2:00 PM)
- [ ] End-of-day sales report (CLOCK: share with team at 6:00 PM)

### HOTFIX PROTOCOL (IF NEEDED)

- [ ] Bug identified and severity assessed (CRASH + BYTE)
- [ ] Fix implemented and tested (BYTE: 30-60 minutes)
- [ ] Hotfix build uploaded (SHIP: 15 minutes)
- [ ] Hotfix announced (HYPE: Steam/Discord/Twitter)

---

## 13. Conclusion

This is the release plan. Every step from code freeze to live on Steam. Every platform configuration documented. Every rollback procedure ready. Every launch day hour accounted for.

What's the rollback plan? It's documented.
What's the hotfix procedure? It's documented.
What happens if Steam is down at launch? It's documented.
What happens if a review embargo breaks? It's documented.

First impressions are permanent. Launch day defines a game's trajectory. We have one chance to get this right.

Is it on the checklist? If not, it doesn't happen.

Test the build on a CLEAN machine. Verify every platform configuration. Monitor every metric. Respond to every P0 bug within 2 hours.

Launch day is boring or it's a disaster. This plan makes it boring.

Let's ship this.

---

**SHIP, Release Manager**
**2026-02-07**

*What's the rollback plan?*
