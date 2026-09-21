# DIVINE STEALTH: REBORN — Game Design Document (v1.0)

**Owner:** Game Director · **Status:** Approved for Vertical Slice · **Scope:** Act I (5 missions) + full open-world systems

---

## 1. Vision Statement

*Divine Stealth: Reborn* is a third-person open-world action-adventure where the player is a **god reincarnated on modern Earth**, sworn to improve the world **without ever being identified as divine**. It delivers GTA-class sandbox freedom — driving, parkour, infiltration, a living city — but inverts the power fantasy: your abilities are enormous in origin and *tiny in expression*. The mastery loop is not "how much force can I apply" but "how invisible can my hand be."

**Three design pillars:**

1. **The Invisible Hand** — every major problem has 3+ non-lethal, influence-based solutions; the best solution is the one no one ever notices happened.
2. **Mortals Must Not Know** — exposure, not death, is the fail state; a coherent, mathematically legible evidence system makes the threat fair and readable.
3. **The World Remembers Good** — world improvements (Goodness) persist across restarts; the city visibly heals, giving even failure meaning.

**Defining Twist:** On identity **Proof**, the game plays "The Oath Breaks" cinematic and restarts from the last **Divine Oath checkpoint** — *world Goodness changes are retained; story progress and some relationships reset* (see §5.4).

---

## 2. Product Overview

| Field | Value |
|---|---|
| Working title | Divine Stealth: Reborn |
| Genre | Open-world action-adventure · stealth · driving · social-sim |
| Camera | Third-person over-shoulder; first-person optional for driving/investigation |
| Player count | Single-player |
| Platforms | PC first (Steam, Epic); PS5/Xbox Series ports post-launch (see Technical Plan §7) |
| Engine | Unreal Engine 5.4+ (justification in Technical Plan §1) |
| Session length | 20–60 min mission arcs; 5–15 min side activities |
| Campaign length | Act I ≈ 10–14 h critical path; 30–40 h completionist |
| Monetization | Premium ($39.99 target), cosmetic-only DLC post-launch, no MTX in-loop |
| Rating target | ESRB T / PEGI 16 (non-lethal focus, mild violence, mature themes) |

---

## 3. Core Gameplay Loop

```
┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│  SCOUT   │──▶│   PLAN   │──▶│ EXECUTE  │──▶│ COVER TRACKS │──▶│ MEASURE      │──▶│ RISK         │
│ intel,   │   │ approach,│   │ stealth, │   │ erase        │   │ IMPACT       │   │ MANAGEMENT   │
│ disguise,│   │ loadout, │   │ driving, │   │ evidence,    │   │ Goodness ↑,  │   │ Suspicion    │
│ social   │   │ miracle  │   │ hacking, │   │ witnesses,   │   │ unlocks      │   │ decay, heat, │
│ stealth  │   │ budget   │   │ subtle   │   │ media spin   │   │              │   │ Proof risk   │
└──────────┘   └──────────┘   │ miracles │   └──────────────┘   └──────────────┘   └──────┬───────┘
      ▲                       └──────────┘                                                │
      └───────────────────────────── loop continues ◀─────────────────────────────────────┘
                          (Proof reached → "The Oath Breaks" → Restart at last Oath checkpoint)
```

**Minute-to-minute:** move, drive, tail, eavesdrop, disguise, non-lethal takedown, hack, Nudge.
**Mission-to-mission:** pick targets, build cover identities, recruit contacts, unlock districts.
**Meta:** raise city Goodness 0→100 per district; keep global Suspicion below Proof; complete Act I.

---

## 4. Key Systems (with concrete numbers)

> Full math and tuning tables in [System Design Specs](03-System-Design-Specs.md). This section gives design intent + headline values.

### 4.1 Identity-Secrecy System

The heart of the game. Three linked resources:

| Resource | Range | What it represents |
|---|---|---|
| **Suspicion** | 0–100 (global) + 0–100 per district | How much the world *wonders* about you |
| **Evidence Items** | discrete objects (footage, logs, testimony) | Concrete proofs that can be found, copied, destroyed |
| **Proof Threshold** | Suspicion ≥ 100 **or** 1 "Hard Proof" item goes public | The Oath breaks → Restart |

**Headline tuning values (defaults; see Spec doc for full tables):**

- Witness sees a *borderline* act (impossible reflex catch): **+8 Suspicion** (district), +2 global.
- Witness sees an *overt* act (visible telekinesis): **+40 district / +20 global**, spawns Evidence item "Testimony (Soft)".
- CCTV records a borderline act: spawns Evidence "Footage (Soft)" — **+12 district** if uploaded within 10 min game-time.
- CCTV records an overt act: spawns **"Footage (Hard Proof)"** — if it reaches a network/social feed → instant Restart.
- Insight used on 3+ NPCs within 60 s: targets feel "watched," **+4 Suspicion each** beyond the 2nd.
- Suspicion decay: **−6/game-day global**, −10/game-day district (doubled while "lying low" in a safehouse ≥ 6 game-hours).
- **Warning band:** HUD Suspicion ring becomes visible at **≥ 60 global** (hidden below that — see §8).
- **Investigator spawn:** at 75 global Suspicion, a persistent Investigator NPC (journalist "Mara Voss" in Act I) starts tailing evidence.

**Witness memory decay:** an unrecorded witness's testimony downgrades one tier per 2 game-days (Hard→Soft→Rumor→gone) unless they file a report, get interviewed, or upload media. Convincing, bribing, or discrediting a witness removes the item non-violently. *Harming witnesses tanks Goodness (−15) and doubles their story's virality if they survive.*

**Miracle Budget:** the god's daily allotment of probability manipulation.
- **Base: 3 Nudges + 1 Veil charge + 1 Mend per game-day**, refreshed at dawn.
- Upgrades (via Goodness milestones) raise cap to 6 / 3 / 3 by end of Act I.
- Every use beyond the *safe context check* (no direct witness LOS, no active camera, plausible coincidence available) adds Suspicion — the budget is the leash that keeps the fantasy subtle.

### 4.2 Goodness Meter (World State)

- **Per-district score 0–100**; city score = weighted mean (population-weighted).
- Sources: mission outcomes (+8 to +20), side events (+1 to +4), economic redistribution (+1 per $25k routed to public good), environmental fixes (+2 each).
- Losses: collateral harm (−5 to −15), lethal force without mass-casualty justification (−10), failed protection events (−3).
- **Visible world changes** at thresholds: 25 = fewer street crimes, cleaner streets; 50 = new small businesses, NPC dialogue shifts, district unlock triggers; 75 = community events, allies volunteer intel; 100 = "Renewed" district state (cosmetic overhaul + passive Suspicion decay +2/day there).
- **Persists through Restarts.** This is the player's true save file — the world itself.

### 4.3 Reputation & Networks

- **Cover identities** (max 4 active): Journalist, NGO Worker, Rideshare Driver, Fixer. Each has a Cover Integrity score 0–100; blowing a cover (caught in a restricted area while wearing it) locks it for 3 game-days and −20 Integrity.
- **Contacts network** (node graph UI): Media, Police, Hospital, Bank, City Hall branches. Contacts unlock via missions/side quests; each offers 1 passive perk (e.g., Police contact: −25% response escalation speed) and 1 active favor per game-day (e.g., "kill a news story" — consumes favor, removes 1 Soft Evidence).
- Relationship values −100…+100; **some relationships reset to their Act-start value on Restart** (flagged `oath_fragile: true`), others persist (`oath_anchored`, earned via their personal side quests).

### 4.4 Combat & Stealth

- **Non-lethal toolkit:** taser (2 charges), sleep darts (4), chokehold takedown (silent, 2.2 s), environmental KOs (breaker boxes, steam valves), thrown distractions (coins, phone-ping spoof).
- Lethal weapons exist in-world (can be picked up in emergencies) but: **any kill = +25 district Suspicion, −10 Goodness**, unless the "Imminent Mass Casualty" flag is active (then 0/0 but still spawns investigation).
- **Stealth AI states:** Unaware → Curious (2.5 s look) → Investigating (walks to stimulus) → Alerted (searches, radios) → Combat. Vision cone 90°, range 22 m day / 12 m night / 6 m through foliage; hearing radius 8 m footsteps, 30 m gunshot, 15 m glass break. Full FSM in Spec doc §4.
- **Social stealth:** matching disguise + calm walk speed = "blend"; running, bumping, restricted zones, or lingering ≥ 20 s near a suspicious guard breaks blend.

### 4.5 Driving & Traversal

- Vehicle classes: sedan, sports, van (equipment capacity), motorbike (chase escapes), bus/tram (fast-travel + social stealth). Arcade-plus handling model (grip forward, hand-brake drift, damage states affect steering).
- Parkour: vault, climb (2.5 m auto, 4.5 m with ledges), balance beams, zipline (placed gear). **No flight, no super-jumps** — traversal reads as elite-human, never superhuman.
- Traffic obeys police response tiers; at Response Tier 3+, roadblocks and spike strips appear (see Spec doc §5).

### 4.6 Economy

- Income: cover-job wages ($150–400/shift), side jobs ($300–1,200), redistributed illicit funds (mission-based, $10k–250k — **taking > 10% for yourself caps Goodness gain of that op at half**), investments (safehouse-run, 2–5%/game-week).
- Sinks: safehouses ($15k–120k), disguise kits ($500–4k), tech (Veil battery $8k, drone jammer $12k), vehicles ($6k–90k), influence ops (bribes $1k–20k, media placements $5k).
- Target pacing: player affords 2nd safehouse by Mission 3, full non-lethal kit by Mission 4. Full balance curve in Spec doc §6.

### 4.7 Dynamic City Systems

- **Day/night** (48 real-minutes/day default), weather (rain reduces camera ID range 30%, crowds −40%).
- **News cycle:** every game-day, top 3 "stories" ranked by virality score; player actions generate story candidates; Media contacts can suppress/boost.
- **Social media virality:** uploaded clips gain Reach (views) on a logistic curve; player can slow it (DMCA-style takedown favor, counter-narrative) before Reach ≥ 100k converts Soft → Hard evidence.
- **Factions:** Halbrook Syndicate (crime), Meridian Corp (finance/energy), AVPD (police), The Radiant Path (cult), city hall. Tension matrix shifts with Goodness/missions.

---

## 5. World & Setting: Aethelburg

A fictional Atlantic-coast metropolis, pop. 3.1 M, founded on river trade, now split between glass towers and rusting docks.

### 5.1 Districts (Act I map)

| District | Character | Act I role | Unlock |
|---|---|---|---|
| **Oldbridge** (old town) | Cobblestones, shelters, markets | Start; Mission 1 | Start |
| **Veritas Row** (media district) | Studios, billboards, the Ledger newspaper | Cover identity hub | Start |
| **The Shallows** (slums) | Dense housing, blackout zone | Missions 1 & 3 | Start |
| **Coinwharf** (financial core) | Banks, Meridian tower | Mission 2 | Goodness(Oldbridge) ≥ 25 |
| **Greyspur Docks** (industrial) | Substations, warehouses | Mission 3 | Mission 2 complete |
| **Lexfield** (university zone) | Campus, labs, protests | Side content, recruits | Goodness(city) ≥ 30 |
| **Crown Terrace** (government quarter) | Courthouse, city hall | Mission 4 | Mission 3 complete |
| **Hearthvale** (suburban sprawl) | Cul-de-sacs, cult chapters | Mission 5 | Mission 4 complete |

### 5.2 Side Content

Random crimes to interrupt (mugging, arson — non-lethal resolution scored), corruption tips (photograph the handoff), rescue events (bridge jumper, trapped worker — Mend risk/reward), environmental hazards (chemical leak), street races (pink-slip-free, reputation stakes), delivery jobs, investigation quests (multi-clue mini-mysteries).

### 5.3 Protagonist & Powers

**"Ash"** (player-nameable) — a nameless god of thresholds and second chances, reborn in a shelter cot with fractured memories of Babylon, Kyoto, Lisbon 1755. Ordinary build, forgettable face (deliberate design: see Art Brief). Bound by the **First Oath**: *"No mortal shall know my true nature."*

| Power | Effect | Cost | Exposure rules |
|---|---|---|---|
| **Nudge** | Tiny probability shift: lock jams, guard sneezes/looks away, light flickers, dice/RNG bias, network packet "luck" | 1 Nudge charge | Safe if a mundane explanation exists in-scene; chained Nudges (>2 in 30 s in one witness's view) read as "weird" (+6 Suspicion) |
| **Insight** | 6 s read of one NPC: lie/intent/fear icons | Free, 45 s cooldown | 3+ targets/minute makes NPCs uneasy (+4 each) |
| **Mend** | Heal self/other 40% HP over 10 s | 1 Mend charge | Must be paired with visible first-aid animation & med kit prop, else witnesses log "impossible recovery" (Soft Evidence) |
| **Veil** | 4 s blur on all cameras in 25 m | 1 Veil charge | Blur itself is an anomaly: security reviewing footage rolls 35% chance to flag "glitch" (+5 district Suspicion per flagged use) |

**Hard Rule (design law):** Levitation, projected force, crowd mind-control, on-camera healing without cover = **overt act** → Hard Proof pipeline → Restart if it goes public. There are *no upgrades that soften this*; the leash never comes off.

### 5.4 Restart ("The Oath Breaks")

1. Trigger: Suspicion ≥ 100 global **or** Hard Proof reaches public Reach threshold.
2. 40 s non-skippable-first-time cinematic: the city's noise cuts out; every screen in view shows the proof; a choir swells; the god closes their eyes — *"They know. So they must forget — and so must the story."*
3. Fade to the last **Divine Oath checkpoint** (auto-set at mission start and one mid-mission "major choice" beat).
4. **Retained:** all district Goodness, money ≥ floor (80%), safehouses, gear, `oath_anchored` relationships, codex knowledge (player intel screens keep discovered info — knowledge is the anti-frustration reward).
5. **Reset:** story progress to checkpoint, `oath_fragile` relationships, active Evidence items, Suspicion → 20 (not 0 — the world keeps a faint unease).
6. **Fairness feature:** the restart screen shows the **Exposure Chain** — the exact 3–5 events that produced Proof — with one hint ("The garage camera on Level 2 was never Veiled.").

---

## 6. Mission Design Framework

Every main mission must satisfy:

- ≥ 3 viable approaches (social, technical, physical) — validated in design review with a "3-path matrix."
- ≥ 1 optional objective that trades risk for Goodness.
- Explicit **Identity Risk beats** (moments the mission tempts an overt power).
- Fail conditions listed as: Mission Fail (retry from mission checkpoint) vs **Oath Break (Restart)**.
- Post-mission **Scorecard:** Stealth / Influence / Clean Escape grades (D–S), driving replayability & speedrun categories.

Act I missions are fully scripted in [Mission Scripts](02-Mission-Scripts.md).

---

## 7. Difficulty, Accessibility, Replayability

- Modes: **Pilgrim** (Suspicion gains −30%, budget +1 each), **Mortal Guise** (default), **Perfect Oath** (post-game: 1 Restart = run over, leaderboard).
- Accessibility: full remap, hold/toggle options, camera-shake & motion-blur sliders, colorblind-safe Suspicion/Goodness palettes (shape-coded icons), subtitles with speaker tags & directional indicators, mission-critical audio cues mirrored visually.
- Replayability: alternate approaches per mission, hidden objectives (e.g., Mission 2 "Zero Footage" bonus), New Game+ carries Goodness map inverted (start in a healed city, watch it decay if idle — thematic remix).

---

## 8. UI/UX Requirements (summary — wireframes in doc 04)

- **HUD minimalism:** Suspicion ring hidden until ≥ 60 global or during active evidence events; Goodness shown only on district entry banner + map; miracle budget as 3 small dots bottom-left; diegetic phone for objectives.
- **Menus:** Map (influence layers: Goodness heat, camera coverage, faction control), Contacts graph, Safehouse management, Garage, Disguise loadout.
- **Restart flow:** cinematic → Exposure Chain review → checkpoint load, total ≤ 75 s, skippable after first occurrence.

---

## 9. Quality Bar ("Best Game" Requirements)

| Bar | Measurable target |
|---|---|
| Tight controls | Input-to-animation start ≤ 80 ms; driving at 60 FPS locked on mid-spec |
| Meaningful choices | Every main mission passes the 3-path matrix; ≥ 2 visible world changes per Goodness threshold |
| Fair restart | ≥ 85% of playtesters rate Restart "understood why" (survey); Exposure Chain always names root cause |
| Polish | < 1 blocker per 10 h at beta; consistent art review gates per district |
| Replayability | ≥ 40% of playtesters replay a mission for a better grade in exit surveys |

---

*Companion documents: [Mission Scripts](02-Mission-Scripts.md) · [System Specs](03-System-Design-Specs.md) · [UI Wireframes](04-UI-Wireframes.md) · [Art/Audio](05-Art-Audio-Briefs.md) · [Technical Plan](06-Technical-Plan.md) · [Roadmap](07-Production-Roadmap.md) · [QA Plan](08-QA-Playtest-Plan.md)*
