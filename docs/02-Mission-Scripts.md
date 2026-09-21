# DIVINE STEALTH: REBORN — Act I Mission Scripts (v1.0)

Format per mission: Briefing → Objectives → Fail Conditions → Walkthrough Beats & Set Pieces → Dialogue Snippet → Cutscene Outline → Identity Risk Beats → Reward Table → Meters Impact.

**Legend:** [P] Primary objective · [S] Secondary/optional · **OB** = Oath Break (Restart trigger) · **MF** = Mission Fail (retry from mission checkpoint) · G = Goodness · Sus = Suspicion

---

## MISSION 1 — "FIRST OATH"

**District:** Oldbridge / The Shallows · **Est. time:** 45 min · **Oath checkpoints:** mission start; after planting documents.

### Briefing
You wake in the Saint Aldric shelter with fragmented memories and a burning certainty: you swore something, once, to someone. Outside, landlord **Dominic Reyle** is evicting 40 families from the Corvus Street tenements to flip the block to a shell company, *Bellwether Holdings*. Sister **Imelda** (shelter director, future `oath_anchored` ally) mentions the signing meeting is in three days.

### Objectives
- [P1] Get hired as a temp at Reyle Property Group (cover identity tutorial).
- [P2] Photograph the Bellwether contract in Reyle's office safe room.
- [P3] Plant the forged linkage file tying Bellwether to the Halbrook Syndicate.
- [P4] Trigger a "lucky" fire alarm during the signing meeting (Nudge tutorial).
- [P5] Escort three families to the shelter while police respond to the alarm.
- [S1] Convince (not intimidate) the notary to delay certification (+3 G, Insight tutorial).
- [S2] Erase the lobby camera's cache before leaving (removes 1 Soft Evidence).
- [S3] Leave $2,000 of Reyle's petty cash in the tenants' relief box (+2 G).

### Fail Conditions
| Type | Trigger |
|---|---|
| MF | Reyle signs the contract (timer expires); temp cover blown twice |
| MF | Any family member injured during escort |
| **OB** | Mend used on the injured child **in the courtyard crowd** without the first-aid cover animation → "impossible recovery" filmed by 2+ phones |
| **OB** | Veil used 3+ times inside the office CCTV cluster and the security chief compiles flagged clips (Hard Proof pipeline) |

### Walkthrough Beats
1. **Wake (tutorial):** movement, Insight on a shelter con-man stealing donations (choose: expose quietly / let it go).
2. **The Job:** interview at Reyle Property Group; Insight highlights the interviewer's boredom — matching her preferred answers = instant hire (social stealth tutorial).
3. **Office infiltration (set piece):** open-plan office, 2 guards, 4 CCTVs, keycard mailroom route vs vent route vs after-hours cleaning-crew route (3-path matrix). Safe room lock: Nudge the aging tumbler ("lucky jam") or pickpocket the key.
4. **The Plant:** slide the forged file into the diligence folder. Optional: read Reyle's email → learn the notary's route (unlocks S1).
5. **Signing day (set piece):** Reyle's conference floor. Player must be *out of the room* when the alarm triggers — Nudge the ancient alarm relay from the stairwell (teaches "plausible coincidence": the relay was flagged faulty in a maintenance email the player can find).
6. **Escort (finale):** three-family convoy on foot through The Shallows while sirens converge on Reyle's tower; a child falls from a fence — **the temptation beat** (Mend safely with first-aid kit from Imelda, or risk it raw).
7. Return to shelter → cutscene → safehouse unlock (a room above Imelda's shelter).

### Dialogue Snippet (Beat 6 — the child)
> **MOTHER:** She's not breathing right— someone— *please!*
> **ASH (player, kneeling):** I know first aid. Give me room.
> **IMELDA (arriving, low):** Your hands are shaking. That's new for you.
> **ASH:** They shake when it matters.
> **IMELDA:** Funny. The kit's untouched and she's already breathing.
> **ASH:** Good kits. Barely need opening.
> **IMELDA:** *(beat)* Whoever you are — Corvus Street doesn't care. But *others will.* Be careful who watches you work.

### Cutscene Outline
- **Opening (90 s):** black screen; overlapping voices of past eras; eyes open in the shelter cot; a news radio drones about evictions. Title card.
- **Mid (20 s, on planting file):** Reyle laughing on the phone, intercut with a family packing boxes — motivation stinger.
- **Closing (60 s):** eviction notice shredded on the news; Imelda hands over the room key; first Oath whisper VO: *"No mortal shall know. Begin quietly."* Goodness meter UI introduced.

### Identity Risk Beats
1. Veil overuse in the CCTV cluster (counter shown after 2nd use).
2. Public Mend on the child (the mission's authored temptation).
3. Sprint-climbing the tower exterior in daylight (borderline: +8 Sus if witnessed).

### Reward Table
| Reward | Value |
|---|---|
| Cash | $3,500 + S3 forfeits $2,000 for +2 G |
| Goodness | +12 Oldbridge, +6 Shallows (base); up to +17/+8 with S1–S3 |
| Suspicion | Authored floor +4 global (the world noticed *luck*) |
| Unlocks | Shelter safehouse; contacts: Imelda (anchored), beat cop Ruiz (fragile); Temp Worker cover identity |
| Grades | Stealth / Influence / Clean Escape (S-rank: zero alerts, S1 done, no Veil flags) |

---

## MISSION 2 — "THE SILENT HEIST"

**District:** Coinwharf · **Est. time:** 60 min · **Oath checkpoints:** mission start; after back-office access gained.

### Briefing
St. Camber's Hospital loses funding in five days. **Victor Sallow**, manager at Merchant & Tide Bank, launders Halbrook money through dormant accounts. Journalist contact **Priya Nair** (The Ledger) has the paper trail but no proof. Plan: redirect one laundering cycle — $2.4 M — into the hospital's charitable trust, anonymously, and hand Priya the evidence.

### Objectives
- [P1] Acquire the auditor cover (steal credentials at the Regulator's mixer OR forge via Fixer contact).
- [P2] Social-engineer entry to the bank's back office during the Thursday audit window.
- [P3] Re-sequence the transfer schedule (network mini-puzzle; Nudge = "packet luck" hint tokens).
- [P4] Trigger the controlled power flicker at 14:02 to mask the transfer log rotation.
- [P5] Escape and dead-drop the ledger copy at Priya's tip line.
- [S1] Route an extra $200k of Sallow's *personal* skim into the trust (+3 G, +1 heist alarm risk).
- [S2] Leave zero footage: Veil ≤ 1 use AND physically loop the vault-corridor camera (Zero Footage bonus, −5 Sus).
- [S3] Plant a resignation-bait email in Sallow's drafts (he flees; Act II thread).

### Fail Conditions
| Type | Trigger |
|---|---|
| MF | Transfer window missed (14:02–14:07); auditor cover blown before P3 |
| MF | Bank enters lockdown with player inside (silent alarm chain) |
| **OB** | Biometric bypass performed **on camera without Veil** — footage shows the scanner accepting a stranger's palm (Hard Proof if uploaded) |
| **OB** | Insight chained on 4 guards in the marble hall — they compare notes, security chief reviews tapes, compiles anomaly reel |

### Walkthrough Beats
1. **The Mixer (social set piece):** regulator's cocktail event; Insight to find the drunk auditor; lift lanyard via bump, or charm the coat-check. No combat possible — pure social stealth.
2. **Bank recon:** rideshare cover drops executives; overheard schedules populate the intel screen.
3. **Back office (set piece):** escorted-visitor rules — player is *legal* until they deviate. Deviation windows: escort's smoke break (4 min), fire-panel test (90 s). Three routes to the transfer terminal: records room crawlspace / service elevator / bluffing past the junior teller with auditor jargon (dialogue check unlocked by reading the audit binder).
4. **Mini-puzzle (P3):** a 6-node packet-routing board; re-order transfer batches so the laundering batch lands in the trust's clearing window. Nudge spends reveal one safe path segment each ("the switch port flaps — how lucky").
5. **The Flicker (P4):** basement breaker Nudge at exactly 14:02 (in-world clock); early/late = log mismatch = silent alarm.
6. **Escape (set piece):** motorbike chase through Coinwharf's colonnades as private security (not police) pursues; goal is *losing* them, not fighting; tram-underpass shortcut is the taught escape.
7. **Dead drop:** Ledger building mail chute; Priya's light flicks on upstairs — she's in.

### Dialogue Snippet (Beat 3 — bluffing the junior teller)
> **TELLER OKAFOR:** Audit floor's closed, sir. Escort only.
> **ASH:** And yet your Basel III liquidity annex is due at three. Shall I note the delay, or the cooperation?
> **OKAFOR:** …You people never smile, huh?
> **ASH:** We smile at clean ledgers. Yours has a 40-basis-point hole in the overnight book.
> **OKAFOR:** That's— that's rounding.
> **ASH:** Then it'll take me five minutes to confirm. Door?
> **OKAFOR:** *(buzzes)* Five minutes. And I'm timing you.

### Cutscene Outline
- **Opening (45 s):** hospital board reading the shortfall memo; a nurse wheels a child past shuttered ward doors; cut to Sallow buying a third watch.
- **Mid (15 s, on P3 success):** the trust account ticker rolls up $2.4 M; a janitor at the hospital sees the pledge board update and crosses himself.
- **Closing (60 s):** Priya's byline: *"Miracle Donor Saves St. Camber's — Regulators Probe Merchant & Tide."* Ash watches from a tram; a stranger beside them: "Whoever did that — hell of a coincidence." Ash: "The best ones are."

### Identity Risk Beats
1. Biometric scanner beat: authored temptation to just *make it work* barehanded.
2. Insight chaining in the guard-dense marble hall (counter UI appears at 2).
3. Escaping upward: the colonnade rooftops are climbable, but a daytime 3-story free-solo above a crowd is a borderline act (+8 Sus per witness cluster).

### Reward Table
| Reward | Value |
|---|---|
| Cash | $12,000 fixer fee (taking any of the $2.4 M halves the G reward — economy rule) |
| Goodness | +15 Coinwharf, +5 city-wide (news story); S1 +3 |
| Suspicion | −5 if S2 Zero Footage; else +6 authored (the "miracle donor" mythos begins) |
| Unlocks | Dr. Ellen Osei (hospital contact, anchored path); **Mend II** (60% heal); Auditor cover; motorbike "Courier 400" |
| Grades | S-rank: Zero Footage + bluff route + on-time flicker |

---

## MISSION 3 — "GHOSTS OF THE GRID"

**District:** Greyspur Docks / The Shallows · **Est. time:** 55 min · **Oath checkpoints:** mission start; after control-box rewire.

### Briefing
Meridian Energy is rolling blackouts across The Shallows to crater property values before a buyout. NGO contact **Tomas Vane** has internal emails but they're inadmissible — stolen. Plan: restore power, make the sabotage *provable* through legitimate discovery, and hand regulators a reason to subpoena.

### Objectives
- [P1] Infiltrate Substation GS-7 in a Meridian maintenance disguise.
- [P2] Rewire the load-shed control box to restore The Shallows feed.
- [P3] Nudge a transformer overload at Meridian HQ **during the board meeting** (their own grid fails on camera — poetic, public, mundane).
- [P4] Leak the email cache to regulators through Vane's NGO via a "misdelivered" FOIA response (launders provenance legally).
- [S1] Re-route the spare feed to St. Camber's backup line (+2 G; Dr. Osei favor).
- [S2] Tag all 6 patrol drones with jammer chips for future ops (unlocks drone-blind routes city-wide).
- [S3] Avoid tripping any drone alarm (Ghost bonus, −4 Sus).

### Fail Conditions
| Type | Trigger |
|---|---|
| MF | Control box rewire fails 3 times (feed locks out 24 h) |
| MF | Caught by drones twice while in disguise (Meridian blacklists the cover) |
| **OB** | Overload executed with *visible arc phenomena around the player* — if the drone footage of "the man the lightning avoids" is compiled (player must jam or Veil the two witness drones) |
| **OB** | Entering the HQ boardroom floor in person during the overload — being *seen where you cannot be* twice in one op flags "impossible presence" testimony chain |

### Walkthrough Beats
1. **The dark district (mood beat):** drive into The Shallows at night — no lights, drum fires, Imelda's generator wheezing. Free-roam vignette: restore a corner clinic's fuse (side G).
2. **Badge & badge-manner:** steal laundry-van uniform or earn one by actually doing a repair shift (the honest route gives a real badge and +1 G).
3. **Substation GS-7 (set piece):** vertical yard of transformers, 6 patrol drones on figure-8s, thermal cameras (crouch-walking near hot transformers masks thermal signature — taught systemically). Control box = wire-matching puzzle under a 90 s patrol window; Nudge can "flicker" a drone's LIDAR for 5 s.
4. **The Overload (P3):** from the substation SCADA, schedule a load spike to hit HQ's demo feed at 15:00 board meeting. Requires two prep steps discovered via intel: HQ's demo bypass breaker (S2 drone photos reveal it) and the meeting time (Vane's emails). Execution is a *remote* act — the game rewards not being there.
5. **The Leak (P4):** dress the cache as a misfiled FOIA response; deliver via courier cover to the regulator's mailroom; Insight the mail clerk to pick the tray that gets opened today.
6. **Lights-on (finale):** stand on the Shallows overpass as the grid reboots block by block — systemic Goodness fireworks; crowd cheers the "grid guys."

### Dialogue Snippet (Beat 4 — Vane, on the plan)
> **VANE:** You want their own tower to brown out mid-meeting? That's… theatrical.
> **ASH:** It's mundane. Overloaded demo feed, deferred maintenance. Their sins, their blackout.
> **VANE:** And the emails?
> **ASH:** Arrive by accident, through a door regulators can legally walk through.
> **VANE:** You engineer coincidences like other people file taxes.
> **ASH:** Everyone should file taxes.
> **VANE:** *(laughs)* Who *are* you?
> **ASH:** Someone who pays what's owed.

### Cutscene Outline
- **Opening (60 s):** Meridian exec on a earnings call — "demand-side optimization" — intercut with an oxygen machine dying in The Shallows.
- **Mid (12 s, on rewire):** one streetlight blinks on over a kid's basketball hoop; a single bounce echoes.
- **Closing (75 s):** board meeting brownout on the news; regulator statement; Shallows block party under working lights. Mara Voss (investigator) first appearance: freeze-frames the substation drone feed — "Who's the sixth technician? There were five on shift."

### Identity Risk Beats
1. The overload arc: doing it on-site with raw Nudge instead of the SCADA schedule = spectacle.
2. Drone witnesses: two drones must be jammed/Veiled/avoided during the rewire.
3. Thermal trick misuse: standing *inside* the transformer heat plume for minutes reads as "the man who doesn't burn" if a worker approaches.

### Reward Table
| Reward | Value |
|---|---|
| Cash | $8,000 NGO "consulting"; optional honest-shift wage $350 |
| Goodness | +14 Shallows, +6 Greyspur; S1 +2; honest badge +1 |
| Suspicion | +5 authored (Voss thread begins); −4 if Ghost bonus |
| Unlocks | **Infrastructure map layer** (city-wide power/camera/utility overlay); Vane (anchored path); Meridian Tech cover; drone jammer schematic |
| Grades | S-rank: Ghost + remote overload + honest badge |

---

## MISSION 4 — "THE WITNESS PROBLEM"

**District:** Crown Terrace / city-wide pursuit · **Est. time:** 70 min · **Oath checkpoints:** mission start; after garage extraction; courthouse morning.

### Briefing
**Elena Marsh**, Halbrook's ex-accountant, can put boss **Cyrus Hale** away — and Hale knows. Two contractor teams are hunting her before Thursday's testimony. Police contact **Sgt. Ruiz** can't protect her officially (leaks inside AVPD). You must keep her alive, keep the evidence chain clean, and keep every miracle deniable — this mission is the Suspicion system's masterclass, with an in-fiction tutorial: Priya explains how "the miracle donor" rumor is being hunted by Mara Voss.

### Objectives
- [P1] Extract Elena from the Pelican Street parking garage (non-lethal only — kills here are near-automatic exposure risk given camera density).
- [P2] Survive the dynamic pursuit to the safehouse (manage Elena's Health & Panic meters; Panic ≥ 100 = she bolts at the next stop).
- [P3] Swap the tampered evidence bag at the courthouse intake before 9:00 (chain-of-custody puzzle: forms, seals, timestamps must match).
- [P4] Attend the trial as a civilian; use Insight (≤ 3 reads) to flag the bribed juror to the prosecutor via Ruiz.
- [S1] Identify and non-lethally disable both contractor spotters *before* the garage extraction (pursuit starts at Tier 1 instead of Tier 3).
- [S2] Talk down the second hit-team's driver (a coerced debtor) instead of ramming him (+3 G, Act II ally seed).
- [S3] Zero injuries to Elena (unlocks her `oath_anchored` friendship).

### Fail Conditions
| Type | Trigger |
|---|---|
| MF | Elena's Health reaches 0 or Panic bolt in an unsecured zone |
| MF | Evidence bag swap fails custody check (trial postponed; retry next game-day) |
| **OB** | **Stopping a bullet with Veil in camera view** — the garage's 14 cameras make raw Veil interception a filmed anomaly ("the round that turned") |
| **OB** | Mend on Elena in the courthouse medical bay (staffed, cameras, sworn witnesses) — "impossible recovery" testimony from medical professionals is auto-Hard |

### Walkthrough Beats
1. **Recon the garage:** camera map overlay (Mission 3 unlock pays off); mark spotters via Insight from the coffee kiosk.
2. **Extraction (set piece):** level-by-level descent with Elena following; contractor pairs use flashlight sweeps; non-lethal toolkit showcase — steam-valve KOs, taser, darts. A contractor opens fire near a pillar: the authored **Veil temptation** (correct play: pull Elena into cover — the game teaches that *positioning* beats miracles).
3. **Pursuit (set piece):** dynamic chase — sedan default; route choices matter (tunnel = fewer cameras, bridge = faster). Elena's Panic rises with collisions/gunfire, falls when player talks to her (dialogue wheel while driving). Rammed? Health events prompt roadside first aid (Mend legal *inside the car*, no windows aligned to cameras — spatial reasoning as gameplay).
4. **Night at the safehouse (breather):** character scene; Elena asks who you are; three dialogue stances (deflect / half-truth / silence) — sets her Act II epilogue.
5. **Custody swap (puzzle set piece):** courthouse intake; the tampered bag has a reprinted seal one digit off; player must requisition the correct form (B-117), Nudge the queue printer jam to buy 40 s, and swap during the clerk's rotation. Pure procedure-thriller, zero combat.
6. **The Trial (finale):** gallery seat; Insight budget of 3 reads across 12 jurors; tells are readable *without* Insight via observation (sweat, glances at Hale's man) — Insight confirms, observation earns. Pass the note via Ruiz; prosecutor moves to strike; Hale's mask cracks on the stand.

### Dialogue Snippet (Beat 4 — safehouse)
> **ELENA:** In the garage. That man fired at us from four meters.
> **ASH:** He was moving. Adrenaline ruins aim.
> **ELENA:** I do forensic accounting. I know when numbers don't add up.
> **ASH:** Then audit this: you're alive, and Thursday you'll be heard.
> **ELENA:** That's not an answer.
> **ASH:** It's the only line item that matters.
> **ELENA:** *(quiet)* Fine. But when this is over, I'm going to sit down and do the math on you.
> **ASH:** When this is over… I hope it comes out even.

### Cutscene Outline
- **Opening (75 s):** Elena burning her old life — shredder, hair dye, one photo she can't destroy; intercut with Hale ordering "the accountant closes her books."
- **Mid (20 s, safehouse dawn):** silent scene — Ash awake all night by the window; Elena pretending to sleep, watching him not-blink.
- **Closing (90 s):** verdict — guilty; Hale led out; Elena exhales in the corridor and looks for Ash — the gallery seat is empty. Mara Voss in the back row, watching the empty seat. Sting: her murder-board now says "MIRACLE DONOR = GARAGE GHOST?"

### Identity Risk Beats
1. The bullet/Veil moment (authored, telegraphed by camera-density UI).
2. Courthouse Mend temptation if Elena arrives injured (avoidable via S3 play).
3. Insight overuse in the jury box — 4th read makes a juror complain of "that staring man" (bailiff escorts player out = MF).

### Reward Table
| Reward | Value |
|---|---|
| Cash | $5,000 (Ruiz's discretionary informant fund; refusing it +1 G) |
| Goodness | +20 city-wide (conviction of Hale — biggest Act I spike) |
| Suspicion | +8 authored (Voss connects two threads) — the game *tells* players the noose narrows by design |
| Unlocks | Sgt. Ruiz contact tier 2 (police response favor); **Suspicion deep-dive codex**; Elena (anchored if S3); safehouse #3 (Crown Terrace flat) |
| Grades | S-rank: Tier-1 pursuit start + zero injuries + ≤ 2 Insight reads at trial |

---

## MISSION 5 — "THE MASK OF MERCY"

**District:** Hearthvale · **Est. time:** 65 min · **Oath checkpoints:** mission start; after mapping the projector rigs; before the rooftop confrontation.

### Briefing
**The Radiant Path** recruits the desperate with staged miracles — Pepper's-ghost projectors, ultrasonic "voices," salted healings. Leader **Brother Solon** is draining savings and isolating families; Imelda's shelter is losing people to the compound. The bitter irony is the design theme: *a real god must dismantle fake divinity without offering the genuine article.*

### Objectives
- [P1] Infiltrate the Path as a recruit ("Seeker" cover; sustained social stealth — daily rituals scored for conformity).
- [P2] Map all 4 projector rigs + the audio bunker (photograph internals for the exposé).
- [P3] Sabotage the rigs to fail *live* during Solon's streamed "Grand Radiance" (reveal wires, speakers, and the kneeling actor mid-air on a lift).
- [P4] Orchestrate the "building inspection" evacuation to pull 30 recruits out legally before Solon's enforcers lock the doors.
- [P5] Rooftop confrontation with Solon — non-lethal showdown (talk-down / taser / environment; he *wants* you to do something impossible on his backup stream).
- [S1] Recover the tithe ledger (families' repayment fund; +4 G).
- [S2] Turn deacon **Marta** (true believer, doubting) with evidence, not humiliation (+3 G; she leads the recruits out — makes P4 trivial).
- [S3] Never once be alone with a camera and a "test of faith" (Solon baits recruits with staged dangers to film reactions) — Untested bonus, −6 Sus.

### Fail Conditions
| Type | Trigger |
|---|---|
| MF | Cover conformity score < 40 at day's end twice (expelled from compound; re-entry via night infiltration only) |
| MF | Fewer than 15 recruits evacuated before lockdown |
| **OB** | **Outshining the fake miracle with a real one** — any overt act during the live stream is instantly Hard Proof (100k+ concurrent viewers; no takedown possible) |
| **OB** | Healing an injured recruit **on Solon's stream** — his hidden cameras cover the infirmary specifically to farm "miracle" content |

### Walkthrough Beats
1. **Intake (social set piece):** surrender your phone (HUD phone disabled — mechanical vulnerability as theme), interview with deacon Marta; Insight shows *her* doubt, not zealotry — plants S2.
2. **Life in the Path (systemic days x2):** chores, sermons, "spontaneous" miracles on schedule. Conformity meter: sing, kneel, donate believably. Explore during 3 authored gaps (laundry duty, generator refuel, night watch).
3. **The rigs (P2):** projector loft (climb), mirror pit under the stage (crawl), audio bunker (keypad — code readable via Insight on the sound deacon's finger-drumming), drone-mounted "angel light" (jammer chip from Mission 3 S2 pays off).
4. **Sabotage (P3, set piece):** three rigs must fail in *sequence*, not at once (staggered failure reads as equipment decay, not sabotage — the game's thesis applied against illusions). Timing mini-game against the liturgy script (stolen from the bunker).
5. **The Grand Radiance (set piece):** live stream; rigs fail one by one — gasp, then laughter, then phones rising *against* Solon; his actor dangles on the visible lift. Solon improvises: "The Adversary is HERE, among us!" — pivots the crowd to hunt a scapegoat: **you** (your conformity slips flagged you). Crowd-evasion sequence with zero powers safe to use (everyone is filming).
6. **Evacuation (P4):** the pre-arranged "city inspector" (Vane's NGO lawyer, coordinated in prep) arrives with a real code-violation order (fire exits chained — genuinely true); Marta (if S2) shepherds recruits out singing — one of the game's tonal high points.
7. **Rooftop (P5, finale):** Solon, backup phone streaming, walks the parapet: "Show them what you are, and I'm a prophet either way. Or let me fall, and you're a murderer's silence." Solutions: talk-down (Insight-informed dialogue tree using his abandonment backstory found in S1 ledger margins), taser as he steps back (timing window), or Nudge the *stream* — his phone battery "dies" (1 charge, no visual anomaly, then tackle-rescue him barehanded like any brave mortal.
8. **Coda:** compound repurposed as a shelter annex (if S1) — Goodness made visible.

### Dialogue Snippet (Beat 7 — rooftop)
> **SOLON:** I built heaven out of projectors and they *loved* me for it. What did the real thing ever give them?
> **ASH:** Nothing they could film.
> **SOLON:** Ha! So there IS a real thing. Show me. One inch off the ground. My flock deserves a genuine article.
> **ASH:** Your flock deserves fire exits that open.
> **SOLON:** Dodge, dodge. I'm standing on the edge of your conscience, friend. Miracle, or murder-by-inaction?
> **ASH:** There's a third thing.
> **SOLON:** Which is?
> **ASH:** A man catching a man. It's older than both of us.

### Cutscene Outline
- **Opening (60 s):** Radiance recruitment ad (in-fiction video, glossy); cut to an empty chair at Imelda's dinner table.
- **Mid (25 s, on P2 complete):** the mirror pit — Ash's reflection fractured across a dozen angled panes; a single held look: the only time the game visually admits what he is.
- **Closing (100 s):** news montage — Solon's arrest, families reunited, tithe checks in envelopes; Ash on the shelter roof at dawn. Mara Voss's murder-board — threads from Missions 1–5 now form a shape; she pins a blurry substation frame in the center. **ACT II title sting:** her voice — "Nobody's this lucky."

### Identity Risk Beats
1. The stream (the entire mission is a no-fly zone for powers — inverting the toolkit).
2. Infirmary Mend bait (telegraphed by discoverable camera intel).
3. Rooftop provocation — the game's thematic thesis rendered as a single choice.

### Reward Table
| Reward | Value |
|---|---|
| Cash | $0 direct (tithe ledger returns money to victims; keeping any voids ALL mission Goodness — the strictest economy rule in Act I, by design) |
| Goodness | +18 Hearthvale, +8 city-wide; S1 +4, S2 +3 |
| Suspicion | +10 authored if talk-down/taser; **+2 only** if battery-Nudge route (elegance rewarded); Voss thread advances regardless |
| Unlocks | Hearthvale district expansion; Marta contact; **Nudge III** (2 charges may be banked overnight); Act II teaser; "Perfect Oath" mode if Act I done with 0 Restarts |
| Grades | S-rank: Untested + Marta turned + battery-Nudge rooftop |

---

## Appendix A — Mission Reward Summary

| Mission | Cash (base) | Goodness (base) | Authored Sus | Key unlock |
|---|---|---|---|---|
| 1 First Oath | $3,500 | +12/+6 | +4 | Safehouse, covers |
| 2 Silent Heist | $12,000 | +15/+5 | +6 (or −5) | Mend II, infra contact |
| 3 Ghosts of the Grid | $8,000 | +14/+6 | +5 (or +1) | Infrastructure map layer |
| 4 Witness Problem | $5,000 | +20 city | +8 | Ruiz tier 2, codex |
| 5 Mask of Mercy | $0 | +18/+8 | +10/+2 | District expansion, Nudge III |

## Appendix B — The Voss Thread (Act I antagonist-investigator)
Mara Voss accumulates a hidden **Insight Score** from mission outcomes (base +1 per mission, +1 per Soft Evidence surviving 3 days, −1 per suppressed story). At Insight Score ≥ 6 at Act I end, Act II opens with her one clue ahead; ≤ 3, one clue behind. She is deliberately **not** removable in Act I — she is the ambient pressure that makes Cover Tracks matter.
