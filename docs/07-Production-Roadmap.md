# DIVINE STEALTH: REBORN — Production Roadmap (v1.0)

Total plan: **18 months** to PC launch (3-mo Vertical Slice → 9-mo Alpha → 6-mo Beta/Polish/Cert). Team ramps 12 → 28 → 34.

---

## Phase 1 — Vertical Slice (Months 1–3)

**Goal:** One-and-a-half districts (Oldbridge + Shallows edge), **Missions 1 & 2 fully playable**, all core systems present at "proves the fantasy" quality. Slice must answer: *is being a secret god fun for 3 hours?*

| Month | Engineering | Design | Art/Audio |
|---|---|---|---|
| 1 | Project spine: World Partition city block, character controller + parkour v1, save partitions v1, Suspicion Service v1 with `explain` tool | GDD lock, Mission 1 whitebox, tuning DataTables authored | Aethelburg style frames, modular kit v1 (Oldbridge), Ash blockout |
| 2 | Powers (all 4) + safe-context check, guard StateTree FSM, camera/evidence pipeline, driving v1 | Mission 1 scripted end-to-end, Mission 2 whitebox, HUD v1 | Oldbridge art pass 1, VFX deniability tests, temp music states |
| 3 | Virality/news v1, contacts/favors, Oath Break flow, perf pass to 60 FPS on 3060 | Mission 2 scripted, side events ×4, first external playtest (n=12) | Lighting/audio beds, Oath Break cinematic previz, UI art pass |

**Slice gate criteria (go/no-go):**
- Missions 1–2 completable via ≥ 2 approaches each; Oath Break fires correctly from ≥ 6 distinct triggers.
- ≥ 85% of testers articulate why they got caught (Exposure Chain comprehension).
- 60 FPS on 3060/1080p High in the slice area; hitch budget met.
- "Fun signal": ≥ 70% of testers voluntarily replay a mission segment.

**Team (12):** 4 eng (systems, AI, gameplay, tools), 3 design (lead, mission, systems), 3 art (env, character, VFX/UI), 1 audio, 1 producer.

---

## Phase 2 — Alpha (Months 4–12)

**Goal:** All 8 districts traversable (4 at full density), **all 5 Act I missions playable start-to-finish**, all systems feature-complete, economy/Goodness/Suspicion balanced in first pass. "Content complete for Act I, ugly is OK."

**Milestones (3-month beats):**
- **A1 (M4–6):** Coinwharf + Greyspur built; Missions 3 whitebox→scripted; drone AI, infrastructure map layer; vehicle handling v2; investigator (Voss) scheduler v1; monthly playtests begin (n=20).
- **A2 (M7–9):** Crown Terrace + courthouse interior; Mission 4 (pursuit tech: dynamic chase manager, Elena companion AI — highest-risk feature, scheduled early in the beat); witness/custody puzzle systems; news/virality v2 with counterplay; economy first balance lock.
- **A3 (M10–12):** Hearthvale + cult compound; Mission 5 (conformity sim, stream events, crowd-hunt sequence); Goodness data-layer swaps for all districts; full contact/favor graph; **Alpha gate:** finish-to-finish Act I playthrough by external testers, all 10 risk register items re-scored.

**Alpha exit criteria:** critical path completable without dev intervention; restart-rage metric < 20% quit-after-restart; average Suspicion at mission end within tuning bands (see QA Plan §3); crash-free sessions ≥ 95%.

**Team (28):** +6 eng (AI, vehicles, UI, tools, 2 content), +5 design (2 mission, quest, economy, UX), +4 art, +1 audio, +1 QA lead + embedded QA pair.

---

## Phase 3 — Beta, Polish & Certification (Months 13–18)

**Goal:** Content lock → polish to the Quality Bar → ship PC.

- **M13–14 (Beta content lock):** all side content in; VO recording (cinematics + 8 key NPCs); localization text lock (FIGS + BRPT + JP planned); accessibility audit against GDD §7 checklist.
- **M15–16 (Polish):** 2 full polish passes per mission (S-rank pathing, camera, readability); perf hardening (min-spec GTX 1660/30 FPS path); photo mode; speedrun timer + No-Exposure% category hooks; Steam Deck verified pass.
- **M17 (Release candidate):** bug bar — 0 blockers, < 20 majors; Steam/Epic cert (achievements, cloud saves, overlay, refunds-safe save UX); press/creator preview build with spoiler locks on Act II teaser.
- **M18 (Launch):** day-0 patch window, live telemetry dashboards (QA Plan §3 metrics), hotfix rota for 4 weeks; post-launch roadmap announce (cosmetic DLC + Perfect Oath leaderboards; console port kickoff decision gated on 60-day PC KPIs).

**Team (34):** +4 QA, +1 build/release eng, +1 community. Console port team (6) spins up post-launch, targeting +9 months to PS/Xbox with the §7 Technical Plan constraints already honored.

---

## Budget shape & assumptions (indicative)

- 18 months, average loaded cost $14k/person-month, average headcount ~24 → **≈ $6.0 M dev** + $1.2 M contingency (20%) + marketing/localization/QA-external ≈ $1.8 M → **≈ $9 M total**.
- Break-even at $39.99 (Steam net ~$27): ~335k units — aligned with the "moral-twist GTA" hook and stealth-genre comps for a strong single-player debut.
- Scope levers if funding tightens (pre-agreed, in order): Lexfield to vignette-only → JP loc post-launch → Mission 5 crowd-hunt simplification → cut photo mode (last resort; it markets itself).

## Definition of Done (per mission, used across phases)
Whitebox → Scripted (all beats firing) → 3-path validated → Art pass 1 → Audio pass → Balance pass (meters within bands) → Polish pass ×2 → Cert-clean. Tracked on a public-to-team Kanban; no mission skips a stage.
