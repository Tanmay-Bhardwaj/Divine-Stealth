# DIVINE STEALTH: REBORN — UI/UX Wireframes (v1.0)

Text wireframes + interaction specs. Design language: **diegetic-first, minimal, calm** — the HUD should feel like the god's quiet awareness, not a control panel. Primary in-world device: the protagonist's phone ("the Slate").

---

## 1. In-Game HUD

```
┌────────────────────────────────────────────────────────────────────────┐
│  [district banner, on entry only, 3s]      THE SHALLOWS · Goodness 55 │
│                                                                        │
│   (◔) ← Suspicion ring: HIDDEN unless global ≥ 60                      │
│        or an active evidence event is live. Fills clockwise,           │
│        amber 60–84, red 85–99, cracks visually at 95+.                 │
│                                                                        │
│                         [reticle / context dot]                        │
│                                                                        │
│                              "Hold E — Blend"                          │
│                        (context verbs, max 1 shown)                    │
│                                                                        │
│  ● ● ○ | ◆ | ✚✚          [minimal compass strip, objectives as         │
│  Nudge  Veil Mend         diegetic landmarks, not floating arrows]     │
│  (dots pulse AMBER when safe-context check would fail at cast)         │
└────────────────────────────────────────────────────────────────────────┘
```

**Rules**
- No minimap by default (option to enable). Navigation via compass strip + phone map; GPS voice when driving.
- Suspicion is deliberately hidden below 60: the player *feels* it through world cues first (NPC stares, news chyrons, Voss sightings). At ≥ 60 the ring fades in with a single low choir note — a designed "oh no" moment.
- Evidence alerts arrive as phone notifications (top-right, diegetic): `▲ "It's spreading" — Footage, Coinwharf — Reach 25k` → tap to open counterplay screen.
- Insight view: 6 s desaturation, one NPC highlighted, intent glyphs (● lie / ▲ fear / ■ hostile intent / ✦ doubt) above head. Cooldown as a thin arc around the reticle.
- Camera cones overlay on holding INTEL: blue cones (live), grey (looped/dead), red (currently seeing you).

## 2. Map & Influence Layers (phone or safehouse table)

```
┌──────────── MAP ─ AETHELBURG ────────────────────────────┐
│ LAYERS:  [Goodness ❤]  [Cameras ◉]  [Factions ⚑]  [Ops ✦]│
│                                                          │
│   Goodness layer: district heat — cold blue (0) →        │
│   warm gold (100); Renewed districts get a halo rim.     │
│   Cameras layer: coverage density shading + drone routes │
│   (unlocks city-wide after Mission 3).                   │
│   Factions layer: Halbrook red / Meridian silver /       │
│   AVPD blue / Radiant Path white — border friction       │
│   animates where tension is high.                        │
│                                                          │
│ PIN TYPES: mission ◆, side event ○, rumor ？, safehouse ⌂│
│ FOOTER: clock/day · weather · miracle budget · cash      │
└──────────────────────────────────────────────────────────┘
```

## 3. Contacts Network

Node-graph, org-chart style, drawn as red-string board in safehouses / clean list on phone.

```
            [MEDIA]                    [POLICE]
           Priya Nair ──────┐         Sgt. Ruiz (T2)
           ● favor: kill    │         ● favor: response delay
             story (1/2d)   │         ▽ fragile
                            │
   [HOSPITAL]          ★ YOU ★              [CITY HALL]
   Dr. Osei                 │               (locked — Act II)
   ● favor: quiet bed       │
   ◆ anchored               │
                       [NGO/LEGAL]
                       Tomas Vane ◆ anchored
                       ● favor: legal cover op
```

- Each node: portrait, trust bar (−100…+100), `◆ anchored / ▽ fragile` badge with tooltip explaining Oath Break behavior, one passive perk, one favor button with cooldown.
- Anchoring quests surfaced here ("Make it stick" prompt on fragile contacts).

## 4. Safehouse Management

```
┌──── SAFEHOUSE — SHALLOWS WALK-UP ─────────────────────────┐
│ TABS: [Loadout] [Disguises] [Ventures] [Intel Board] [Rest]│
│ Loadout: 4 gear slots + consumables; presets per approach  │
│   ("Ghost", "Face", "Wheelman").                           │
│ Disguises: mannequin row; Cover Integrity bar per identity;│
│   locked covers show cooldown timer & "burned by" note.    │
│ Ventures: one passive investment slot; yield/week; ethical │
│   flavor choices (clinic co-op vs vending) tint Goodness.  │
│ Intel Board: codex — persists through Restarts (labelled   │
│   "What you know cannot be taken back").                   │
│ Rest: advance time; LYING LOW toggle (2× Suspicion decay,  │
│   consumes 6 h).                                           │
└────────────────────────────────────────────────────────────┘
```

## 5. Garage & Disguise Loadout
- Garage: side-scroll vehicle row; stats (speed/handling/anonymity — vans and sedans have HIGH anonymity, sports cars LOW: fame is a stat, thematically).
- Disguise loadout: outfit + props (clipboard, med kit — the med kit is what legalizes Mend); each shows "grants access: …" zone list.

## 6. Restart Flow — "The Oath Breaks"

```
SEQUENCE (≤75 s total, skippable after first time):
1. Freeze frame of the exposing moment → city audio cuts to silence
2. Cinematic (40 s): screens everywhere replay the proof; choir; VO oath line
3. EXPOSURE CHAIN screen:
   ┌───────────────────────────────────────────────┐
   │        T H E   O A T H   B R E A K S          │
   │  How they knew:                               │
   │   1. Garage cam L2-03 — Veil never applied    │
   │   2. Clip uploaded by guard @ 21:44           │
   │   3. Voss linked it to the substation frame   │
   │  ✦ Hint: cameras marked red are recording you │
   │  KEPT: Goodness · safehouses · gear · codex   │
   │  LOST: story to last Oath · fragile bonds     │
   │            [ Return to the Oath ]             │
   └───────────────────────────────────────────────┘
4. Fade-in at checkpoint; world visibly retains improvements (lights on,
   murals up) — the first thing the player sees is what SURVIVED.
```

## 7. Mission Scorecard (post-mission)
Three vertical grade columns — STEALTH / INFLUENCE / CLEAN ESCAPE (D→S) — plus discovered-approaches tally ("You found 1 of 3 ways in"), replay button, and speedrun timer opt-in. S-rank stamps are wax-seal motif (oath iconography).

## 8. Accessibility Panel (first-boot + pause)
Remap all; toggle/hold; UI scale 80–160%; colorblind palettes (Suspicion also shape-coded: ring cracks, not just reddens); subtitle sizes + speaker tags + sound-cue captions ("[camera whir, left]"); screen-shake/motion-blur/chromatic sliders; Pilgrim mode pitch: "the story, gentler."
