# Dive v1.3.0 — The Brood, autopilot, music visualizer

- Built 2026-11-03 02:42 · versionCode 6 · applicationId `com.seth.dive`
- Signed with the repo debug keystore (cert SHA-256 `3bb5bcc8…1ee6f2`). It installs over v1.2.1 and keeps your save.

## The Brood (idle)
- New part **Brood Pod** (45 DNA, up to 4). Drag it onto a body segment in the Shaper's Body tab. Each pod holds 2 **harvesters**: they swim out, latch onto prey with a glowing tether, and reel it into your mouth.
- Predators can eat a harvester while it's out on a job. It regrows from its pod.
- **Brood tab** in the Shaper has 7 upgrades:
  - **Reach:** longer tether range.
  - **Speed:** harvesters swim and reel faster.
  - **Grip:** they can haul heavier prey, up to your own size.
  - **Haul:** more DNA from harvested food.
  - **Instinct:** they go for golden-ring carriers first, skip prey a predator is guarding, and dodge predators.
  - **Regrowth:** lost harvesters come back faster.
  - **Drift:** they keep gathering while the app is closed, for longer and more efficiently.
- **Coming back** shows "While you drifted (2h 10m): +N DNA · M hauled in" with a welcome chime. Offline gathering starts at 1 h and 10% efficiency, and Drift raises both.

## Autopilot
- Tap the **AUTO** pill (top-right, next to the shell). It's also in the pause menu and Settings.
- Your creature grazes quietly, flees hunters, keeps clear of big creatures, and handles depth based on the Autopilot depth setting (follow the hint orbs, hold depth, or keep descending).
- Touching the screen takes over. Autopilot resumes 3 s after you let go.
- **Cinematic camera:** a slow orbit that gently rises and falls. The HUD fades out.
- **Optional auto-evolve** spends DNA on pods, segments and Brood upgrades for you.
- The difficulty system stops learning your skill while autopilot drives.

## Music and visualizer
- **Settings → Music & visualizer:**
  - **Dive lofi:** the built-in generated music.
  - **Phone audio:** visuals follow whatever your phone is playing, such as Spotify. It reads the audio output, not the microphone, but Android shows a "record audio" permission prompt for it.
  - **Folder:** pick a music folder and Dive plays its tracks on shuffle (subfolders up to two levels deep). Next track is in Settings.
- **The visuals react to the music:**
  - The fractal sea brightens and shifts color, and in this mode it shows even near the surface.
  - Beats pulse your glow, the harvesters and the plankton.
  - On strong beats a ring of light bursts from you.
  - Small field-of-view kicks on beats. Calm motion turns these off.
- **Options:** Reactivity 0–2×, Visual intensity 0–100%, plus a live status line.

## Built-in music upgrades
- **Drift arrangement** while autopilot drives: chords change every two bars, drums fade out, a fuller pad, longer reverb, and a generative melody whose phrases repeat with small variations.
- Smoother voice-leading on the electric piano.
- The key slowly modulates by fourths, so long sessions keep evolving.
- New sounds: a pluck when a harvester latches on, an in-key note when food is reeled in, and the welcome-back chime.
- Dive's own music mutes while yours plays. Sound effects stay on.

## Known gaps
- Phone-audio capture: some phones or apps block it. The status line will say so; use a folder instead.
- Not yet tested on a real phone. Offline checks:
  - harvesters haul about 10 creatures/min with 2 pods
  - audio peaks -2.9 dBFS with no NaNs
  - beat detection caught 59 of 60 beats at 120 BPM
