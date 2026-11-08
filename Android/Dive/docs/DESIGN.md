# Dive — design plan

## Original prompt (verbatim)

> make a geometric version of Flow that runs on android and is controlled via tilt. tap and hold to dive deeper. tap to attack the thing closest to you and eat it to grow like the beginnings of spore. use points from eating to resculpt yourself in a crator creator like spore. the levels are infinite zen with calm synth music (generated lofi chill) and there is always a bigger and smaller "fish" in the ocean. etc. help me design first.

Refinements agreed in conversation before v1.0.0:
- It's a **DDA game** (dynamic difficulty adjustment, after Jenova Chen's flOw thesis).
- You can go **up or down at any time**.
- Camera is **top-down** while swimming; **hold both thumbs** to swing into a **flight-sim chase cam** and pitch the phone to dive/climb.
- "It would be really really cool if the ocean was a **sea of fractals** at some level, or that vibe at least."
- Seth: "if you have any ideas to change things that you think will make it better, that's totally okay… make the best choice."

The design was refined by a five-role agent team (DDA, controls & camera, world & ecosystem & Shaper, audio, graphics) and integrated into one build.

---

## v1.0.0 — playable alpha

### Pillars
1. **Flow channel first.** Challenge should track skill so the player is never bored or anxious.
2. **Zen stakes.** You never die. Being bitten costs segments (they regrow) and DNA.
3. **Always a bigger and a smaller fish.** Spawns are sized relative to you. At mass ×8 the whole world renormalizes around you ("scale ×2"), so growth never runs out.
4. **The deep is a fractal sea.** Calm teal shallows give way to glowing fractal sheets (kaleidoscope, then coral filigree) that you pass through as you dive.

### Controls
| Action | Input |
|---|---|
| Swim | Tilt, **or drag anywhere** for a floating virtual joystick (it takes over from tilt while held; its base follows your thumb). Tilt can be switched off. |
| Eat (zen) | Swim your mouth into anything smaller than you; no tap needed. Drift gently and prey won't notice you until you're close (stealth). Swimming fast or lunging spooks it from farther away. |
| Strike | Optional tap: lunges at the edible nearest **where you tapped** (or toward that spot). Needed for skittish darters and for biting similar-sized or bigger creatures. |
| Dive view (flight) | **Press & hold still ~0.4 s to toggle** (ring fills). Only a finger that hasn't moved from where it touched can toggle; a finger that moves becomes the joystick. |
| Dive / climb | In dive view: joystick **drag up = climb, down = dive**, left/right turns; or tilt (tip away = dive). Invert option flips both. |
| Strike in flight | Tap, same as cruise. |
| Leave flight | Press & hold again. Camera swings back overhead; screen-up becomes your heading. |
| Shaper | Tap the spiral shell in the top-right (it pulses when you can afford something). |
| DDA overlay | Triple-tap the top-left corner. |

Tap/hold/chord timing, steering physics (thrust, drag, lateral slip) and camera constants follow the controls spec. The camera is one orbit rig: elevation 80° in cruise and 20° in flight, blended with smootherstep, so it never passes through the creature.

### DDA (two layers)
- **Player-chosen:** depth sets base challenge `B(d) = d / (d + 120)`. Bands are 40 m: Sunlit, Twilight, Indigo, Violet, Abyss, then Fractal Deep 1…∞.
- **Hidden in-band:** an offset `aOff` (capped at half a band step, so it can never mask a band change) moves challenge toward the flow channel `T(S) = 0.08 + 0.84·S ± 0.10`.
  - Easing runs 2× faster than hardening, with hysteresis.
  - Lever values are stamped onto creatures only when they spawn, so nothing on screen visibly changes.
- **Skill S** is an Elo-style estimate built from:
  - hit rate
  - eats per minute (opportunity-gated)
  - damage per minute
  - near-miss vs bite ratio
  - hunger
  - tilt smoothness
  - fleeing after bites
- **Levers:**
  - prey evade speed and awareness
  - predator count, aggression, chase speed and give-up time
  - bigger / similar / smaller spawn mix
  - food density
  - strike-assist cone and range
  - bite damage, DNA loss and regen
- **Nudges:** a red orb (go deeper) appears when you're bored or maxed out. A blue orb (go up) appears when you're anxious or bitten twice in 20 s. Eating an orb carries you 40 m. If you ignore nudges, their cooldown grows.
- **Music intensity** = `0.1 + 0.5·Cs + 0.3·threat + 0.1·anxiety` (attack 1.5 s, release 6 s). Layers come in at pad → keys → bass and kick → hats and snare → arpeggio.

### World and creatures
- **Player.** Spine of segments: the core plus 2–11 more. Size = mass^⅓.
  - Eating whole prey (ρ < 0.8) adds 8% of its mass. Biting similar-sized creatures (ρ 0.8–1.25) takes a segment. Nibbling bigger creatures gives a little DNA and draws aggro.
  - Lost segments show as ghost outlines and regrow after 5 s without being hit.
  - **Core breach:** float up 40 m, 6 s invulnerable, full regrow.
- **NPC archetypes:**
  - Mote: boid schools
  - Darter: skittish zig-zag
  - Grazer: ring-segment drifter
  - Lurker: dim ambusher that lunges
  - Hunter: octahedral chaser with jaws; also hunts smaller NPCs
  - Leviathan: gentle giant chain
  - Drifter: jelly that stings for DNA. From band 4 it becomes a recursive jelly with tiny jellies on its tentacles.
  - Branchling: L-system fractal coral from band 3; tips are grazeable and regrow
- **Readability:** danger (bigger than you) is warm magenta/coral; prey is in the band's cool hue; similar-sized creatures are pale.
- **Part carriers** wear a pulsing golden ring. Eating or biting one unlocks its part.

### Shaper (creator)
- Pauses the game into a 3D showroom you rotate by dragging.
- Pick a segment with ◀ ▶. Resize it. Add or remove segments (cost 25 × count).
- Change body and accent colours (8 swatches each).
- Parts:

| Part | Cost | Max | Effect | Where |
|---|---|---|---|---|
| Jaws | 40 | 1 | bite reach | core |
| Fins | 30 | 3 pairs | speed and turn | not the core |
| Tail | 35 | 1 | lunge | last segment |
| Eyes | 45 | 2 pairs | targeting range and cone | core or segment 1 |
| Spike | 50 | 6 | thorns: biters lose a segment | any segment |
| Plate | 60 | 4 | that segment takes 2 bites | any segment |
| Glow | 80 | 2 | lures small prey toward you | any segment |

- Part size runs ×0.6–1.6 (cost scales with size^1.5). Removing a part refunds 75%.
- Start unlocked: Jaws, Fins, Tail. Eyes appear on carriers in bands 0–1, Spikes in 1–2, Plates in 2–3, Glow in 3+.
- The Shaper also holds settings: pitch invert, haptics, calm motion, recenter tilt, music volume.

### Audio
Everything is synthesized on-device (AudioTrack, float, 44.1 kHz):
- 72 BPM with swing.
- Jazzy 9th/13th progressions on e-piano and pad, with sub bass and soft drums.
- Vinyl crackle and tape wobble.
- A feedback-delay-network reverb that grows with depth, plus a low-pass that closes as you dive. The key drops at band changes.
- Every bite plays an in-key pluck quantized to the 16th-note grid (smaller prey sounds higher).
- Flight adds a whoosh and widens the stereo.

### Graphics
- **Background:** GLES 3.0. A half-res fractal-sea background (stacked 2D fractal sheets every 26 m, crossed analytically per ray) is upsampled with dither.
- **Creatures:** instanced flat-shaded geometry with barycentric neon edges, rim light and exp² fog matched to the background water colour.
- **Glow:** additive halo billboards.
- **Plankton:** point sprites that streak in flight.

### v1.0.1 changes (before first test)
- **Zen eating** (Seth asked whether tapping ruins the zen): contact-eating plus stealth makes the whole game playable with tilt alone; tap is now an optional skill lunge, whose hit rate still feeds the DDA.
- Top-down contact rule: things that overlap on screen within a vertical slab count as touching.
- Fixes from code review: a resting finger no longer blocks taps; a tap can't trigger flight; spawns mostly at your own depth; fins face outward; Shaper relayouts live; no predators in the first seconds; orbs and core breach work during flight; calibration doesn't jerk; heading wraps; 24-bit depth buffer; bigger prism/halo budgets for coral; spawns hidden beyond the fog in flight; plankton no longer sinks away; strict-GLSL smoothstep fix.
- Economy tuned (−25% DNA, slower mass growth), validated by a headless 15-minute bot simulation at three skill levels plus a no-tap run.

---

## v1.1.0 — Seth's first-test feedback + 10 bang-for-buck improvements

Seth (after playing v1.0.1): "This is pretty awesome." Asked for: one-hand play in portrait, feeding that doesn't miss, dive mode that toggles on hold instead of holding the whole time, and a more Spore-like drag-and-drop creator; then "identify 10 best bang for buck improvements and do it."

1. **One-hand dive toggle**: press & hold anywhere (~0.4 s, ring fills) switches between top-down and dive view; no two-thumb chord, no holding.
2. **Tap-to-aim**: a tap lunges at the edible nearest the tap point (bigger creatures only when tapped directly); empty taps lunge toward that spot.
3. **Hungrier mouth**: anything smaller touching your head is eaten; small prey within ~2.4 radii of your mouth are drawn in; lunge bites test the swept mouth path so fast lunges can't skip prey; bite reach +40%.
4. **Spore-style drag-and-drop Shaper**: drag a part card up out of the palette and drop it on your body (snaps to the nearest valid segment, glowing green; red if it can't fit); drag attached parts to move them; drag them off the body to remove (75% refund); tap a part to select/resize; drag empty space to rotate. Settings moved behind a gear.
5. **Ready-to-eat glow**: prey within reach of your mouth pulses softly.
6. **Eat juice**: spark burst streams into you, "+N" DNA popups, core pulse.
7. **Combo melody**: eats within 1.6 s of each other climb the current chord's pentatonic.
8. **Living body**: segments undulate with a travelling wave scaled by speed; fins beat faster when you swim fast.
9. **Adaptive quality**: if frames run slower than ~22 ms for 4 s, the fractal background steps down (fewer layers → lower resolution → cheap mode).
10. **Gentle first minute**: 45 s grace with no predators at session start.

---

## v1.2.0 — joystick, smoother controls, +10

Seth: "controls need to be a little bit smoother and let's give people a virtual joystick anywhere they touch with a nonmoving from initial touch being the only one that toggles"; then "add 10 improvements, let's make it better, then ship it."

**Joystick and smoothing:** floating joystick from any touch point (deadzone 12%, eased magnitude, base follows past 56 dp); still finger = only toggle; second-finger tap still lunges; Tilt on/off setting. Smoothing: tilt filter τ 0.05→0.10 s, steering slew-limited, turn gain 5→3.5 with τ 0.16 s, dive-view turns smoothed, climb/dive τ 0.4 s, bank τ 0.3 s, lunge heading eases, softer camera follow and dive-camera yaw.

**+10:**
1. Pause menu (Back or returning to the app): Resume, Shaper, Recenter, Tilt toggle, Leave.
2. Journal: deepest dive, biggest scale, creatures eaten, DNA earned, time in the sea (persisted).
3. Discovery: first visit to each band → "Discovered: …" + 20×band DNA.
4. Edge arrows for off-screen chasing predators (red, pulsing), golden-ring carriers of locked parts (gold) and nudge orbs (red/blue).
5. Heartbeat haptic that quickens with predator threat.
6. Leviathan wake: gentle giants shed food as they swim.
7. Bubble trail when swimming fast, diving or lunging.
8. Shaper part descriptions on pick-up/select.
9. 🎲 Mutate: free random colours and body proportions.
10. Orb labels "↓ deeper" / "↑ shallower".

---

## v1.2.1 — farther cameras + Settings screen

Seth: "the camera needs to be farther away and extra farther in the first person mode"; "make things like that in a settings menu with a value."

- Camera defaults: top-down 1.5× higher; dive view 2× farther behind and a little higher (elevation 20°→24°). Fog thinned proportionally; spawn/despawn ring, plankton volume and population cap scale with the visible area so nothing pops in.
- **Settings screen** (pause menu → Settings, or Shaper → ⚙ Settings), every value live and persisted, with Reset to defaults:
  camera top-down 0.5–2.5× (1.5), dive view 0.5–3× (2.0), field of view 40–80° (50), tilt on/off, tilt sensitivity 0.5–2× (1.0), joystick size 30–100 dp (56), joystick deadzone 0–30% (12), hold-to-switch 250–900 ms (420), steering smoothing 0–250 ms (120), turn speed 0.5–2× (1.0), invert dive/climb, haptics, calm motion, music 0–100% (80), graphics Auto/High/Medium/Low.

---

## v1.3.0 — The Brood (idle), autopilot, music visualizer

Seth: "Make an autopilot mode" → "maybe we make autopilot like an idle game where you're upgrading the ability to send things to go out and bring you food? They attach to things and pull them in?" → "improve the harmonics and music and visuals in autopilot mode… make it play to your music with the accompanying visuals like a music visualizer, complete with options… nice for running during work." Music sources: "Spotify integration would be cool but if it's easier start with pick a folder on device. Both would be best." Confirmed the phone-audio mode reads audio output, not the microphone.

**The Brood**
- New part **Brood Pod** (45 DNA, up to 4, unlocked from the start). Each pod houses 2 **harvesters**: they swim out, latch onto prey with a glowing tether and reel it into your mouth. Predators can eat a harvester on a job; it regrows from its pod.
- **Brood tab** in the Shaper with 7 upgrade tracks (cost = base × 1.6^level): Reach (+20% range), Speed (+15%), Grip (prey up to your own size), Haul (+10% DNA), Instinct (target golden rings, avoid predator-guarded prey, dodge predators), Regrowth, Drift (offline gathering hours/efficiency).
- **Offline:** returning shows "While you drifted (Xh Ym): +N DNA · M hauled in" with a welcome chime. Base 1 h at 10%; Drift raises hours (+1.5 h/level) and efficiency (+8%/level). Harvested food never teaches the DDA.

**Autopilot** (AUTO pill top-right, pause menu, Settings)
- The creature grazes at stealth speed, flees chasers, keeps distance from big creatures, and (by setting) follows hint orbs / holds depth / keeps descending. Touching the joystick takes over; it resumes 3 s after release. DDA skill learning pauses while autopilot is on.
- Optional **auto-evolve** buys pods, segments and Brood upgrades when it can comfortably afford them.
- **Cinematic camera:** slow orbit with breathing elevation and distance. HUD fades (AUTO pill, popups and toasts stay).

**Music & visualizer**
- Music source: **Dive lofi** (generated), **Phone audio** (Android Visualizer on the output mix — plays along with Spotify etc.; reads output, never the mic, but needs the RECORD_AUDIO permission), or **Folder** (pick a folder; plays its audio files shuffled, two levels deep, with the visuals synced).
- Reactive visuals: fractal sea brightens and hue-shifts with the music and shows even in the shallows in visualizer mode; beat pulses on the background, your glow, harvesters and plankton; a light ring bursts from you on strong beats; small FOV kick (off with Calm motion). Built-in lofi drives the same pulses from its own beat and chord changes.
- Options: Reactivity 0–2×, Visual intensity 0–100%, Next track, live status line.
- Lofi engine upgrade: e-piano voice-leading, slow key modulation by 4ths, generative motif melody; a lusher ambient **drift** arrangement while autopilot drives (2-bar chords, no drums, fuller pad, longer reverb); harvester latch/reel sounds and the welcome-back chime; music mutes (SFX stay) when your own music plays.

### Assumptions and known gaps (alpha)
- Android Back closes the Shaper/overlay, otherwise opens the pause menu (as of v1.2.0). Progress autosaves every 15 s and on pause.
- The scale renormalization at mass ×8 is intentionally invisible apart from a toast.
- Some planned parts of the deep are left for later: the raymarched Mandelbox floor and the "Powers of Ten" creature-fractal at 400 m+.
- Not yet profiled on a phone. If the background is heavy, the fallback is fewer fractal layers (`FRACTAL_LAYERS 3`) or `BG_CHEAP`.
