# DIVINE STEALTH: REBORN — QA & Playtest Plan (v1.0)

QA owns two promises: **the Oath is fair** (exposure triggers are deterministic and legible) and **the world persists** (save partitions never betray the player).

---

## 1. Test Strategy Overview

| Track | Cadence | Owner |
|---|---|---|
| Exposure-trigger regression suite (automated) | Every nightly build | QA + tools eng |
| Save-partition fuzz suite (automated) | Every nightly | Build eng |
| Perf flythrough capture (automated) | Every nightly | Build eng |
| Structured playtests (external) | Monthly from Slice M3; biweekly in Beta | UX researcher |
| Full-run "Oathkeeper" playthroughs (manual) | Weekly from Alpha | Embedded QA |
| Accessibility audit | Slice gate, Alpha gate, Beta lock | QA lead |

## 2. Identity-Exposure Trigger Test Cases

Automated where possible (scripted bot performs the act in a controlled arena level with configurable witnesses/cameras; asserts on Suspicion Service + Evidence Ledger output). **Every case asserts three things: correct delta, correct evidence spawn, correct Exposure Chain entry.**

| ID | Scenario | Expected result |
|---|---|---|
| EXP-001 | Nudge with mundane tag, 0 witnesses, 0 cameras | ΔSus 0; no evidence; no chain entry |
| EXP-002 | Nudge, no mundane tag, 2 civilian witnesses | ΔSus district = 2.0×2×1.0; no evidence |
| EXP-003 | 3rd chained Nudge in 30 s, same witness | A=4.0 path; "weird luck" chain entry logged |
| EXP-004 | Raw Mend, daylight, 4 civilians + 2 filming phones | ΔSus ≈ 40.8 district (Spec §1.3 worked example, tolerance ±0.1); 2× Footage(Soft) spawned with 10-min upload windows |
| EXP-005 | Mend WITH med-kit prop + animation, same witnesses | A=1.0 path; NO footage spawn |
| EXP-006 | Veil ×3 in CCTV cluster; force flag RNG to hit | 3× flag events, +5 district each; security-chief compile task scheduled |
| EXP-007 | Overt act (levitation) with 1 recording camera | Hard evidence spawns; Suspicion bypassed; Reach curve starts; phone alert at 25k; **Oath Break at 100k** |
| EXP-008 | Overt act, zero witnesses/cameras (empty rooftop) | No evidence, no Sus (the Oath cares about *knowing*, not doing) — CRITICAL fairness case |
| EXP-009 | Hard footage stolen from DVR before review event | Item voided; no chain entry; achievement hook "Never Happened" |
| EXP-010 | Witness (memory-class) unreported for 4 game-days | Tier decays Hard→Soft→Rumor per schedule |
| EXP-011 | Insight ×4 within 60 s in guard hall | +4 per extra target; guard "watched" bark fires; 4th read in M4 jury = bailiff MF, not OB |
| EXP-012 | Kill with Imminent Mass Casualty flag active | 0 Sus / 0 Goodness penalty; investigation event still spawns |
| EXP-013 | Suspicion reaches exactly 100 via decay-race edge | Oath Break fires once (no double-trigger); Sus post-restart = 20 |
| EXP-014 | Oath Break during a driving cutscene / vendor menu / photo mode | Break defers to next safe frame; no softlock; chain intact |
| EXP-015 | Restart → verify WorldState retained (Goodness, cash floor 80%, codex, anchored NPCs) and StoryState reset (fragile NPCs, evidence ledger empty, budget refreshed) | Field-by-field save-diff assert |
| EXP-016 | Counter-narrative favor on Hard item at Reach 90k | r ×0.4 applied; player can win the race if acted at alert; verify timing math gives ≥ 20 real-min window at base r |
| EXP-017 | Data-trail correlation: 3 facility logs matching pattern | +12 global; Voss query log entry; 2 logs = no fire |
| EXP-018 | Rain + night raw Mend (visibility mods stack) | A = 6.0×0.7×0.7 path; verifies multiplicative mods |

Manual exploratory charters per mission: "try to break the authored temptation beats" (e.g., M4 garage — attempt Veil-bullet from every camera-blind spot; blind spots must genuinely exist and work).

## 3. Telemetry Metrics & Tuning Bands

Dashboards live from Slice playtest #1. Bands are the *design contract*; breaches file auto-tickets.

| Metric | Target band | Alarm |
|---|---|---|
| Avg global Suspicion at mission end | M1: 15–30 · M2: 20–40 · M3: 25–45 · M4: 35–55 · M5: 40–60 | Outside band 2 playtests running |
| % players triggering ≥1 Restart in Act I | 35–60% (it should happen to many, once) | >75% (too punishing) or <20% (toothless) |
| Quit-within-10-min-after-Restart rate | < 15% | > 25% = R5 escalation |
| "I understood why I was caught" (survey) | ≥ 85% | < 75% blocks phase gate |
| Goodness growth curve (city) | 8–12 by M2 · 20–28 by M3 · 30–40 by M4 · 42–55 by M5 | — |
| Approach distribution per mission | No single path > 60% usage | > 75% = other paths under-signposted |
| Miracle budget usage | 60–90% of daily charges spent | < 40% = players afraid of the system (readability bug) |
| Avg police tier at mission end | ≤ 1.0 (stealth fantasy holding) | — |
| Mission replay rate (voluntary) | ≥ 25% by Beta | — |
| Perf: 95th-pct frametime, 3060/1080p | ≤ 16.6 ms | > 18 ms fails nightly |
| Crash-free sessions | ≥ 95% Alpha, ≥ 99.5% RC | — |

## 4. Structured Playtest Protocol

- **Cohorts:** stealth-genre veterans, GTA-sandbox players, narrative-first players (n=8–12 each; the tri-cohort split is mandatory — the game must bridge them).
- **Sessions:** 2.5 h; think-aloud for 1st hour; no hints from moderators on exposure mechanics (tests self-legibility).
- **Key instruments:** post-mission micro-surveys (3 questions, in-build), exposure-comprehension interview ("walk me back through how they caught you" — scored against the actual Exposure Chain log), emotion curve mapping at M1 child-heal beat, M4 bullet beat, M5 rooftop.
- **The Restart study (dedicated):** deliberately expose one cohort mid-M2; measure comprehension, frustration (1–7), and time-to-reengage. Success: median frustration ≤ 4 AND ≥ 80% articulate what they'd do differently.
- **Perfect Oath pilot (Beta):** invite speedrunners; validate No-Exposure% is completable and the timer/verification hooks are cheat-resistant enough for leaderboards.

## 5. Bug Bars

| Phase gate | Blockers | Majors | Save-integrity bugs |
|---|---|---|---|
| Slice | 0 in slice path | ≤ 15 | 0 (hard rule from day one) |
| Alpha | 0 on critical path | ≤ 60 | 0 |
| Beta lock | 0 | ≤ 30 | 0 |
| RC | 0 | < 20, none player-progress-affecting | 0 |

**Save-integrity bugs are always Priority 0.** The game's promise is "the good you did persists" — a WorldState corruption is a broken promise, not a bug.
