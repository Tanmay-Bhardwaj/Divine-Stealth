# DIVINE STEALTH: REBORN — Technical Plan (v1.0)

Target: PC first (Steam/Epic), 60 FPS mid-range (RTX 3060 / RX 6600-class, 1080p High w/ upscaler). Console export notes in §7.

---

## 1. Engine Choice: Unreal Engine 5.4+ — Justification

| Need | UE5 answer | Unity HDRP comparison |
|---|---|---|
| Open-world streaming | **World Partition + HLOD + Data Layers** (Goodness state variants as data layers — near-free district state swaps) | Addressables/custom streaming: viable but hand-rolled |
| Crowd/traffic at city scale | Mass Entity (MassAI/MassTraffic) proven at city scale in CitySample | DOTS capable but tooling less complete for traffic |
| Cinematic lighting at 60 FPS | Lumen (software mode for mid-spec), Nanite for city geo | HDRP strong, but Nanite-equivalent absent |
| Animation | Motion Matching (Game Animation Sample), Control Rig, Metahuman pipeline for NPC variety | Third-party (Kinematica deprecated) |
| Team scaling | Industry-standard for open-world hires; C++ + Blueprint split fits our team plan | C# hiring easier, open-world specialists rarer |

**Decision:** UE5. Risk (engine bloat, streaming hitches) mitigated in Risk Register R2/R3.

**Key plugins/modules:** MassAI + MassTraffic (crowds/vehicles), StateTree (guard/investigator FSM), Smart Objects (civilian reactions, filming behavior), Chaos Vehicles (custom arcade-plus handling layer), MetaSounds (adaptive audio graph), Wwise *evaluated* as alternative at slice gate, Iris replication OFF (single-player), SaveGame → custom two-partition serializer, DLSS/FSR/XeSS plugin trio, EOS/Steam SDK for achievements/cloud saves.

## 2. Systems Architecture (high level)

```
┌────────────── GAME LAYER ──────────────┐   ┌────────── SIMULATION SERVICES ─────────┐
│ Mission Director (data-driven quests,  │   │ WorldClock/Weather · NewsCycle Service  │
│  oath checkpoints, 3-path validators)  │◀─▶│ Virality Service (Reach curves)         │
│ Player Systems (movement/parkour,      │   │ Evidence Ledger (item lifecycle)        │
│  powers w/ safe-context check, covers) │   │ Suspicion Service (anomaly pipeline)    │
│ Stealth AI (StateTree FSM, perception) │   │ Goodness Service (district state swaps) │
│ Vehicles (Chaos + traffic handoff)     │   │ Faction Tension Matrix                  │
└────────────────────────────────────────┘   │ Investigator AI (Voss query scheduler)  │
                 │                           └─────────────────────────────────────────┘
        ┌────────▼─────────┐
        │ TWO-PARTITION    │  WorldState (persists Oath Break) | StoryState (checkpoint-scoped)
        │ SAVE SYSTEM      │  — see §4
        └──────────────────┘
```

All tuning constants in DataTables (`DT_Suspicion`, `DT_Goodness`, `DT_Economy`) hot-reloadable in dev builds for live balancing during playtests.

## 3. Anti-Exposure Trigger Tech

- **Perception pipeline:** every "act" broadcasts an `AnomalyEvent{score, tags, location}`; witnesses/cameras in range each run the §1.2 math (Spec doc) via the Suspicion Service — O(witnesses) per event, events are rare, cost negligible.
- **Camera analysis system:** cameras are Smart Objects with record buffers (ring buffer of event IDs, not video); "footage" is metadata until a review event (guard shift-end, security chief compile, upload) materializes an Evidence item. Cheap, deterministic, debuggable.
- **NPC phone filming:** Mass Entity tag `Filming` applied via Smart Object query when AnomalyEvent A≥2 fires near ≥3 civilians; 40% conversion; filmed events enter the upload-window timer.
- **Witness memory decay:** Evidence items with `decay_class: memory` tick at midnight; conversion to `stored` on report-filing behaviors (StateTree task on witness NPCs).
- **Data trails:** badge scans/access logs are rows appended to a per-facility `TrailLog`; Voss's scheduler runs correlation queries every N game-days — correlation = 3+ trails matching player pattern hash.
- **Debug tooling (build in slice!):** `dt.exposure.explain` console view — live graph of every Suspicion delta and evidence item with source refs; this powers both QA and the player-facing Exposure Chain screen (same data, curated).

## 4. Save Architecture

- **Partition A — WorldState** (survives Oath Break): Goodness maps, renewed states, economy, safehouses, gear, codex, anchored relationships. Autosaved every 5 min + on Goodness events. Single rolling file + 3 backups.
- **Partition B — StoryState** (checkpoint-scoped): mission progress, Suspicion, evidence ledger, fragile relationships, miracle budget. Written ONLY at Oath checkpoints (mission start, authored mid-beats, district first-entry).
- **Oath Break =** discard current StoryState, load last StoryState checkpoint, keep live WorldState, set Suspicion=20. Because partitions are separate files, the restart is a partial load — target < 5 s on NVMe.
- Versioned schemas + migration table from day one (we WILL rebalance DataTables mid-beta; saves must survive).
- Cloud saves via Steam/EOS; slot count 5 + Perfect Oath dedicated slot (hardcore: single slot, no backups — by design).

## 5. World Streaming Strategy

- One persistent level; **World Partition** grid 256 m cells, HLOD for skyline; interiors as Level Instances streamed on door-approach (banks/courthouse are heavy — pre-stream on mission accept).
- **Goodness variants as Data Layers:** each district has 4 layer sets (state 0/25/50/75+); swap on threshold cross with a dusk/dawn transition mask (never pop in front of the player: swaps queue until the cell is unobserved or a time-skip occurs).
- Traffic/crowd via Mass, LOD rings: full sim 100 m / representative 400 m / statistical beyond. Parked-car and pedestrian density scales with district Goodness (data-driven from the Goodness Service).
- Perf budgets: 6 ms game thread / 7 ms render thread @1080p High on 3060; streaming I/O budget 200 MB/s sustained; hitch budget < 2 ms per cell activation (measured in automated flythrough tests every nightly).

## 6. Risk Register — Top 10

| # | Risk | L×I | Mitigation |
|---|---|---|---|
| R1 | **Suspicion system feels unfair/opaque** (core-fantasy killer) | H×H | Exposure Chain from day 1; `dt.exposure.explain` shared player/QA data; playtest gate: ≥85% "understood why" before alpha exit |
| R2 | Open-world streaming hitches on mid-spec | M×H | Nightly automated flythrough perf tests; HLOD discipline; interiors pre-stream; cut density before cutting 60 FPS |
| R3 | UE5 version churn destabilizes Mass/StateTree | M×M | Lock engine version at slice; upgrade only at milestone boundaries with a 2-week soak branch |
| R4 | Scope: 8 districts unbuildable by team size | H×H | Vertical slice = 1.5 districts; districts share modular kit (80% shared assets); Lexfield/Hearthvale are half-density by design |
| R5 | Restart mechanic rage-quits players | M×H | Retained-Goodness messaging in UI; Pilgrim mode; telemetry on quit-after-restart rate (<15% target); first restart is authored-adjacent in M1 tutorialization |
| R6 | Non-lethal-only combat feels shallow | M×M | Toolkit depth (environment KOs, social outs); mission design review requires 3-path matrix; combat is deliberately the *worst* option, and scoring says so |
| R7 | Dynamic news/virality system becomes noise | M×M | Cap concurrent stories at 3; every story must reference a player-known event; kill feature at alpha if <60% of testers recall a headline unprompted |
| R8 | Save-partition bugs corrupt the "world persists" promise | L×H | Partition fuzz tests in CI; 3 rolling backups; migration tests on every schema change |
| R9 | Cert/console port assumptions leak into PC scope | M×M | Console-isms (memory budget 12 GB, UI safe zones, TRC-friendly save UX) adopted from slice, but no console SKU work before PC beta |
| R10 | VO/localization cost balloons with branching dialogue | M×M | Text-first until alpha; VO only for cinematics + key NPCs; systemic barks synthesized as placeholders until beta lock |

## 7. Console Export Notes (post-PC)

- Memory: keep peak < 12 GB from slice onward (Series S is the binding constraint).
- Input: full gamepad parity is a PC-day-one requirement anyway; radial menus already designed for sticks.
- TRC/XR prep: no user-facing "saving" spinners > 1 s (partition design already complies), suspend/resume-safe services (NewsCycle must serialize timers), activity cards (PS5) map cleanly to mission beats.
- Upscalers: FSR path doubles as the console path; keep a 30 FPS quality mode option with Lumen HW-RT as stretch.

## 8. Build/CI

Perforce (art) + Git mirror for text/data; nightly builds with: automated flythrough perf capture, save fuzz suite, exposure-trigger regression suite (see QA Plan §2), cook-time tracking. Weekly playable build to whole team ("Friday Aethelburg").
