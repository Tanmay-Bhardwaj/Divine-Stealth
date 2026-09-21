# Suspicion & Evidence Simulation — Playable Prototype

A zero-dependency, single-file web demo (`index.html`) of the **Identity-Secrecy system** from
[System Design Specs §1–§3](../docs/03-System-Design-Specs.md), running live:

- **Anomaly pipeline:** `A = base × mundane(×0.3) × visibility(night ×0.7) × repetition`, weighted per witness type (civilian 1.0 / guard 1.6 / camera 1.4), district → global at ×0.25.
- **Evidence ledger:** memory-class testimony (decays nightly Hard→Soft→Rumor→gone), recorded footage with a 10-minute upload window, logistic **Reach** curves — Hard proof at 100k Reach = **Oath Break**.
- **Counterplay:** steal footage before upload, discredit witnesses, 1/day media takedown favor (spread ×0.4).
- **Miracle budget** (3 Nudge / 1 Veil / 1 Mend, dawn refresh), Veil's 35% "glitch flag" review roll, Insight chain penalties, phone-filming bystanders (40% conversion when A≥2 near 3+ civilians).
- **The Oath Breaks:** Exposure Chain screen showing exactly how they knew; **Goodness persists, Suspicion resets to 20** — the two-partition save model in miniature.

## Run

```bash
python3 -m http.server 8000 --directory prototype
# open http://localhost:8000
```

No build step, no dependencies — open `index.html` in any browser.

## How to play (the design thesis in 90 seconds)

1. Fix **faulty** streetlights with Nudge (`1`) — mundane explanation exists, zero Suspicion, +2 Goodness.
2. Help incidents the **mortal way** (hold `E`) — slower, but invisible.
3. Try Mend (`3`) on an injured NPC **without** the med-kit (`Q`) in a crowd — watch phones come up, footage spawn, and the counterplay race begin.
4. Press `5` in front of the crowd if you want to see the Oath Break and the Exposure Chain.
5. Press `T` for the designer view (`dt.exposure.explain` equivalent — true values behind the hidden HUD).

The intended lesson mirrors the GDD: *the strongest play is the one that produces no event at all.*
