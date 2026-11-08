# Dive

**A zen, tilt-controlled descent into an endless ocean that becomes a sea of fractals.**

You are a small neon creature. Eat what's smaller, avoid what's bigger, and spend the DNA you earn reshaping yourself
in a Spore-style creator. Dive as deep as you dare: depth is difficulty, and a hidden director (dynamic difficulty
adjustment, after Jenova Chen's *flOw*) keeps you in your flow channel. Generated lofi plays along with every bite.
Or flip on **autopilot**, let your Brood of harvesters fetch food for you, and leave it running as a music visualizer.

| | |
|---|---|
| **Latest** | [v1.3.0](1.3.0/) · [download APK](1.3.0/dive-v1.3.0.apk) (1.0 MB) |
| **Platform** | Android 8.0+ (API 26), OpenGL ES 3.0, portrait |
| **Package** | `com.seth.dive` |
| **Web version** | [coming soon](index.html) |
| **Size** | about 1 MB, no third-party libraries, no ads, no network |

## Install (sideload)
1. Download [`dive-v1.3.0.apk`](1.3.0/dive-v1.3.0.apk) on your phone.
2. Open it. If asked, allow your browser or file manager to **install unknown apps**.
3. Newer versions install over older ones and keep your progress (same signing key).

SHA-256 of `dive-v1.3.0.apk`:
`b318d44541be0c853d3368cb7b3086878a614fc34ff545fc539b043820f1379e`

**Permissions:**
- **Vibrate:** haptics.
- **Record audio:** only if you turn on the *Phone audio* or *Folder* visualizer. It reads the sound your phone is already playing so the visuals can react. The microphone is never used, and nothing is recorded or sent anywhere.

## How to play
| Action | How |
|---|---|
| Swim | Tilt the phone, **or drag anywhere** for a floating joystick |
| Eat | Swim into anything smaller than you. Drift gently and prey won't notice you |
| Lunge | Tap. You lunge at whatever is nearest to where you tapped |
| Dive view | Press and **hold still** about 0.4 s to switch between top-down and the flight-style dive camera |
| Dive or climb | In dive view, drag down to dive and up to climb (or tip the phone) |
| Shaper | Tap the spiral shell at the top-right |
| Autopilot | Tap the **AUTO** pill next to the shell |
| Pause / Settings | Android Back |

**Colors:**
- Cool-colored creatures are prey. Warm magenta/coral ones are bigger than you.
- A golden ring marks a creature carrying a part you haven't unlocked.
- Red orbs take you deeper; blue orbs take you up.

## Features
- **Endless, scale-relative ocean.** Spawns are sized relative to you, so there is always a bigger and a smaller fish. Grow 8× and the world quietly rescales around you.
- **Zen stakes.** You never die. Bites knock off segments, which regrow. Lose your core and you float up a zone.
- **Two-layer DDA.**
  - Depth sets the base challenge.
  - A hidden director nudges prey speed, predators and assists toward your flow channel.
  - The music swells with the challenge.
  - Triple-tap the top-left corner for the live overlay.
- **8 creature types:**
  - schooling motes
  - skittish darters
  - grazers
  - ambush lurkers
  - hunters (they eat each other too)
  - leviathans that shed food in their wake
  - stinging jellies (recursive in the abyss)
  - fractal coral
- **Spore-style Shaper.** Drag parts onto your body: jaws, fins, tail, eyes, spikes, plates, glow and Brood Pods. Unlock parts by eating golden-ring carriers. There's also a free 🎲 Mutate button.
- **The Brood (idle).** Brood Pods hold harvesters that tether prey and reel it in. Seven upgrade tracks. They keep gathering while the app is closed.
- **Autopilot and music visualizer.** A cinematic drifting camera with visuals that react to Dive's own music, to whatever your phone is playing, or to a folder of your music.
- **Generated lofi.** Swung, jazzy chords and an ambient drift arrangement. Every bite plays a note in key, on the beat.
- **Settings for everything:** camera distances, field of view, tilt, joystick, timing, haptics, music and graphics quality.

## Docs
- [Design document](docs/DESIGN.md): the full design and every version's rationale
- [Changelog](CHANGELOG.md)
- [v1.3.0 build notes](1.3.0/BUILD-NOTES.md)

## About
Built with Kotlin and the Android framework only, including a custom OpenGL ES 3 renderer and an on-device synth.
Designed and iterated with Claude (Anthropic) through Seth's `/ideatoapk` pipeline. The source repo is private.
