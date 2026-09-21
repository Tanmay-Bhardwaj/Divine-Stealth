# DIVINE STEALTH: REBORN — System Design Specifications (v1.0)

Engineering-facing spec. All values are launch defaults; every constant lives in `DT_Tuning` data tables for live rebalance.

---

## 1. Identity-Secrecy System — The Math

### 1.1 Model overview

Three layers, from fuzzy to fatal:

```
WITNESS EVENTS ──▶ SUSPICION (scalar heat) ──▶ warns/pressures
        │
        └────────▶ EVIDENCE ITEMS (discrete) ──▶ VIRALITY/REACH ──▶ PROOF ──▶ Oath Break
```

- **Suspicion** is analog dread — it gates NPC behavior and investigator activity but *cannot alone* end the run until it hits 100.
- **Evidence** is discrete and fixable — each item can be found, stolen, discredited, or decayed.
- **Proof** = Suspicion ≥ 100 global, OR any **Hard** evidence item's Reach ≥ 100,000.

### 1.2 Anomaly scoring (per witnessed act)

Every player act in perception range of a witness/camera computes an **Anomaly Score A (0–10)**:

```
A = base_act_score
  × context_mod      (plausible mundane explanation present? ×0.3 : ×1.0)
  × visibility_mod   (night 0.7 | rain 0.7 | crowd_occlusion 0.8 | clear day 1.0)
  × repetition_mod   (1.0 + 0.5 × same_witness_repeat_count)
```

| Act | base_act_score |
|---|---|
| Nudge with in-scene mundane explanation | 0.5 |
| Nudge, no explanation (light dies for no reason) | 2.0 |
| Chained Nudges (3rd+ within 30 s, same witness) | 4.0 |
| Insight stare (3rd+ target within 60 s) | 1.5 per extra target |
| Mend with first-aid cover prop + animation | 1.0 |
| Mend raw (visible instant recovery) | 6.0 |
| Veil flagged on footage review (35% roll per use) | 3.0 |
| Elite-human parkour above crowds, daylight | 2.5 |
| Non-lethal takedown, unwitnessed body found | 1.0 |
| Kill | 6.0 (plus Goodness penalty) |
| **Overt act** (levitation, projected force, crowd control) | 10.0 — bypasses Suspicion, spawns Hard evidence directly |

### 1.3 Suspicion accumulation

```
ΔSus_district = A × witness_weight
ΔSus_global   = ΔSus_district × 0.25   (0.5 if the district is Renewed—people talk more when they care)

witness_weight: civilian 1.0 | guard/police 1.6 | journalist 2.2 | camera(recorded) 1.4 | Voss herself 3.0
```

Worked example (Mission 1 courtyard): raw Mend (6.0) in clear day (×1.0), no cover (×1.0), seen by 4 civilians and filmed by 2 phones:
`ΔSus_district = 6.0×(4×1.0) + 6.0×(2×1.4) = 24 + 16.8 = 40.8` → district spikes ~41, global +10, and two "Footage (Soft)" items spawn. One raw mistake ≈ warning band. Two ≈ Proof territory. That's the intended lethality curve.

### 1.4 Decay & mitigation

| Mechanism | Effect |
|---|---|
| Passive decay | −6 global, −10 district per game-day (midnight tick) |
| Lying low (safehouse ≥ 6 game-hours) | decay doubled that day |
| Renewed district (Goodness 100) | +2 extra decay/day in that district |
| Counter-narrative (Media favor) | −8 global, once per 2 game-days |
| Discredit witness (dialogue/evidence) | remove testimony item + −4 district |
| Destroy footage before upload window (10 min) | item never spawns |
| Restart | Suspicion resets to **20** (not 0) |

### 1.5 Evidence item schema & lifecycle

```json
{
  "id": "EV-0412",
  "type": "footage | testimony | data_trail | physical",
  "tier": "rumor | soft | hard",
  "source": "cctv_garage_L2_cam3",
  "act_ref": "veil_intercept_bullet",
  "created_at": "d14_21:42",
  "location": "AVPD evidence server | witness memory | phone(npc_2231)",
  "reach": 0,
  "decay_class": "memory | stored | uploaded",
  "counters_available": ["steal", "corrupt_file", "discredit", "takedown_favor", "outwait"]
}
```

**Lifecycle rules**
- `memory` decay: one tier per 2 game-days (Hard→Soft→Rumor→null) unless converted to `stored`/`uploaded` (report filed, interview given, clip uploaded).
- `uploaded` items gain **Reach** by logistic curve: `Reach(t) = K / (1 + e^(−r(t−t₀)))`, K = ceiling by tier (rumor 5k, soft 40k, hard 500k), r = 1.1/game-hour base, ×2.2 if a news cycle story references it, ×0.4 after successful counter-narrative.
- **Hard item Reach ≥ 100k → PROOF → Oath Break.** UI surfaces any Hard item at Reach ≥ 25k as a phone alert ("It's spreading") — always ≥ 20 real-minutes of counterplay at base r.
- Data trails (badge scans, access logs) never decay; they must be **cleaned** (terminal minigame or Fixer favor $4k) and only matter when an investigator query correlates 3+ trails to the player's pattern (+12 global Sus per correlation event).

### 1.6 Sample Suspicion event log (telemetry format)

```
[d09 13:58] ACT nudge ctx=breaker_room mundane=TRUE A=0.5 wit=0 cams=0     ΔSus 0.0    | G:38 S:22/100
[d09 14:02] ACT nudge ctx=main_hall   mundane=TRUE A=0.5 wit=3 cams=1     ΔSus 2.2g/8.6d
[d09 14:03] ACT insight_chain n=4     A=3.0 wit=4(guard)                  ΔSus 4.8g/19.2d  WARN chain_counter
[d09 14:06] EV_SPAWN EV-0311 footage(soft) src=hall_cam2 window=10:00 → player_looped=TRUE  EV VOID
[d09 14:11] ACT parkour_day A=2.5 wit=6 cams=0 vis=1.0                    ΔSus 3.8g/15.0d
[d09 14:11] STATE global=32.8 → below warn band (60). HUD ring: hidden
[d10 00:00] DECAY −6g −10d (lying_low=FALSE)
[d10 09:14] INVESTIGATOR voss_query trails=2/3 → no correlation. next_query d12
```

---

## 2. Goodness Meter — Formula & District Rules

### 2.1 Core formula

```
G_district(t+1) = clamp( G_district(t) + Σ(event_scores) − decay_neglect , 0, 100 )
G_city = Σ( G_district × pop_weight )      pop_weights sum to 1.0
decay_neglect = 1 per 4 game-days with zero positive events in district (min floor: highest threshold crossed — thresholds are ratchets, cosmetic states never regress below 25/50/75 bands)
```

| Source | Score |
|---|---|
| Main mission outcome | +8…+20 (authored) |
| Side event resolved non-lethally | +1…+4 |
| Redistribution | +1 per $25k routed to public good |
| Environmental fix | +2 |
| Collateral harm | −5…−15 |
| Unjustified kill | −10 (and Suspicion +25) |
| Failed protection event | −3 |

### 2.2 Threshold effects (per district)

| G | World changes | System changes |
|---|---|---|
| 25 | Street crime spawn −30%, cleaner props swap in | +1 side-quest slot |
| 50 | New businesses open (vendor discounts 10%), NPC barks shift hopeful | District unlock triggers eligible |
| 75 | Community events spawn, murals, allies volunteer intel (free rumor/day) | 1 free contact favor/week from district |
| 100 | **Renewed:** cosmetic overhaul (lighting warm-shift, foliage, music layer) | +2 Suspicion decay/day here; permanent |

### 2.3 Restart interaction
Goodness is written to the **WorldState save partition** (see Technical Plan §4) and is *never* rolled back by Oath Break. Design intent: the player's legacy is the city, not the plot position.

---

## 3. Miracle Budget

| Stage | Nudge/day | Veil/day | Mend/day | Unlock |
|---|---|---|---|---|
| Start | 3 | 1 | 1 | — |
| Goodness(city) ≥ 20 | 4 | 2 | 1 | shrine vignette #1 |
| Mend II (M2) | 4 | 2 | 2 (60% heal) | mission |
| Goodness(city) ≥ 40 | 5 | 2 | 2 | shrine vignette #2 |
| Nudge III (M5) | 6 (2 bankable) | 3 | 3 | mission |

- Refresh at dawn (06:00). Unused charges lost (except banked Nudges post-M5).
- **Safe-context check** (run at cast): `no_witness_LOS && no_active_camera_25m && mundane_explanation_tag_present` → zero Suspicion. Otherwise the anomaly pipeline (§1.2) runs. The HUD dot pulses amber when the check would fail — pre-cast readability, no surprise punishments.

---

## 4. Stealth & Detection AI

### 4.1 Guard FSM

```
UNAWARE ──stimulus──▶ CURIOUS(2.5s look) ──persists──▶ INVESTIGATING(walk to point, 12s search)
   ▲                                                        │found nothing
   └──────────────── returns ◀──────────────────────────────┘
INVESTIGATING ──sees player hostile/restricted──▶ ALERTED(radio in 3s unless interrupted) ──▶ COMBAT/SEARCH
```

| Parameter | Value |
|---|---|
| Vision cone | 90° FOV; 22 m day / 12 m night / 6 m foliage; ID (face-match vs disguise) at ≤ 8 m |
| Peripheral | 180° at 4 m (silhouette only) |
| Hearing | footsteps run 8 m / walk 3 m / crouch 0; glass 15 m; gunshot 30 m; taser 6 m |
| Radio interrupt window | 3.0 s (takedown or dart cancels the alert broadcast) |
| Search duration | 45 s solo, 90 s in pairs, then decay to CURIOUS-patrol for 5 min ("uneasy" state: vision +20%) |
| Disguise blend | matching disguise suppresses restricted-zone detection *unless*: sprinting, ≤ 8 m face-ID by a guard who has met that cover before, lingering ≥ 20 s in a guard's cone |

### 4.2 Camera model
- Types: fixed CCTV (cone 70°, 18 m), PTZ (sweep 120°/8 s), drones (Mission 3+, moving cone + thermal), NPC phones (spawn when Anomaly A ≥ 2 event occurs within 15 m of ≥ 3 civilians; 40% of civilians film).
- Record buffer 10 min → local cache → upload window. Player counters: loop (device minigame, 30 s), cut feed (spawns "outage" data trail), Veil (blur 4 s, 35% flag risk), physical theft of DVR.
- **Camera-density UI:** holding the intel button overlays live camera cones (unlocked Mission 3 map layer city-wide; before that, per-building after scouting).

### 4.3 Police response tiers

| Tier | Trigger | Response |
|---|---|---|
| 0 | — | Ambient patrols |
| 1 | Reported misdemeanor | 1 cruiser investigates, 90 s to arrive |
| 2 | Alarm / assault report | 2 cruisers, cordon check |
| 3 | Pursuit active | roadblocks eligible, spike strips, +1 heli spotlight at night |
| 4 | (Act II+) | tactical unit |

Evasion: exit line-of-sight 20 s + change vehicle or disguise → tier decays 1 per 60 s.

---

## 5. Economy Balance

### 5.1 Income vs sink curve (Act I pacing)

| Milestone | Expected cash-on-hand | Gate designed to afford |
|---|---|---|
| Post-M1 | $4–6k | Disguise kit #2 ($1.5k), taser recharge kit ($400) |
| Post-M2 | $15–18k | Veil battery ($8k) or safehouse #2 down-payment |
| Post-M3 | $24–30k | Safehouse #2 ($15k Shallows walk-up), drone jammer ($12k) |
| Post-M4 | $30–38k | Vehicle upgrade tier, Crown Terrace flat ($28k, discounted by Ruiz favor) |
| Post-M5 | $35–45k | Full non-lethal kit maxed; Act II buffer |

- Side content income ceiling: $2.5k/game-day (prevents grind-trivializing).
- **Redistribution rule:** mission illicit funds are earmarked; player skim > 10% halves that op's Goodness; Mission 5 tithe money is 0%-tolerance (authored).
- Investment: each owned safehouse hosts one passive venture (laundromat, clinic co-op…) yielding 2–5%/game-week of invested principal, capped at $5k/week total in Act I.
- Money floor on Restart: `max(current × 0.8, 5000)`.

### 5.2 Costs table (headline)

| Item | Cost |
|---|---|
| Disguise kits | $500–4,000 |
| Sleep darts (4) | $240 |
| Taser recharge | $400 |
| Veil battery (+1 max charge, 1 mission) | $8,000 |
| Drone jammer | $12,000 |
| Bribe (clerk → official) | $1,000–20,000 |
| Media placement / takedown favor (cash route) | $5,000 |
| Vehicles | $6,000 (used sedan) – $90,000 (sports) |
| Safehouses | $15,000–120,000 |
| Fixer trail-clean | $4,000 per data trail |

---

## 6. Save System — State Model

Two-partition model (full architecture in Technical Plan §4):

```yaml
# SAMPLE SAVE-FILE STATE OUTLINE (slot_02.dsave, human-readable projection)
meta:
  version: 1.0.3
  playtime: "14:22:31"
  last_oath_checkpoint: "M4_courthouse_morning"
world_state:            # PERSISTS THROUGH OATH BREAK
  clock: { day: 14, time: "08:12", weather: rain_light }
  goodness:
    oldbridge: 41   shallows: 55   coinwharf: 38   greyspur: 29
    lexfield: 12    crown_terrace: 22   hearthvale: 5   veritas_row: 18
    city: 33.7
  renewed_districts: []
  economy: { cash: 31250, investments: [{venue: laundromat_ob, principal: 8000}] }
  safehouses: [shelter_room, shallows_walkup]
  gear: [taser, darts_4, veil_battery, jammer_chip_x6, disguises: [temp, auditor, meridian_tech]]
  codex_intel: [reyle_network, sallow_accounts, gs7_layout, garage_cameras, path_rigs_partial]
  relationships_anchored: { imelda: 74, vane: 51, osei: 44 }
story_state:            # RESET TO CHECKPOINT ON OATH BREAK
  act: 1
  mission_progress: { M4: "beat_5_custody_swap" }
  suspicion: { global: 47, districts: { crown_terrace: 62, coinwharf: 31, ... } }
  evidence_active:
    - { id: EV-0412, tier: soft, type: footage, reach: 8200, decay: uploaded }
    - { id: EV-0398, tier: rumor, type: testimony, location: witness_memory }
  relationships_fragile: { ruiz: 38, priya: 55, elena: 61, marta: 0 }
  miracle_budget: { nudge: 2/5, veil: 1/2, mend: 2/2, banked: 0 }
  voss_insight_score: 4
  flags: [m2_zero_footage, m3_ghost, honest_badge]
```

Checkpoint writes: at every mission start, one authored mid-mission beat, and on district-first-entry. Autosave of WorldState every 5 min + on any Goodness event.
