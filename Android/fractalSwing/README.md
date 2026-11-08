# fractalSwing

**An interactive fractal animation generator. Every parameter is on a swing you tune live, and it all moves to your music.**

Eleven fractal families render in real time on the GPU. The Julia constant, zoom, rotation, pan, exponent, colour,
orbit trap, kaleidoscope and video feedback each ride their own **swing**: an oscillator with a centre, amplitude,
period, shape, phase and an optional audio link. Pick a built-in look, drag the sliders while it runs, randomize or
mutate, and switch on audio sync so beats kick the zoom, bass shifts the colour and treble feeds the glow.
It's a visualizer you play.

| | |
|---|---|
| **Latest** | [v1.0.0](1.0.0/) · [download APK](1.0.0/fractalSwing-v1.0.0.apk) (0.9 MB) |
| **Platform** | Android 8.0+ (API 26), OpenGL ES 3.0, portrait or landscape |
| **Package** | `com.seth.fractalswing` |
| **Web version** | [play in your browser](play/index.html) (WebGL2; same shaders as the app) |
| **Size** | about 0.9 MB, no third-party libraries, no ads, no network |

## Install (sideload)
1. Download [`fractalSwing-v1.0.0.apk`](1.0.0/fractalSwing-v1.0.0.apk) on your phone.
2. Open it. If asked, allow your browser or file manager to **install unknown apps**.
3. Newer versions install over older ones and keep your presets (same signing key).

SHA-256 of `fractalSwing-v1.0.0.apk`:
`871f6f9e7206076cd3e399ca53d0043fdb40f50db1d8e64c05a94660e2df67e6`

**Permissions:**
- **Record audio:** only if you switch on audio sync. It reads the sound your phone is already playing (Spotify, YouTube, anything) so the visuals can react. The microphone is never used, and nothing is recorded or sent anywhere.

## How to use
| Action | How |
|---|---|
| Pan | Drag |
| Zoom | Pinch (wheel on the web) |
| Rotate | Twist with two fingers |
| Hide / show the controls | Tap the fractal, or the ≡ button top-right |
| Reset the view | Double-tap |
| Random look | Long-press (or 🎲) |
| Snapshot | 📷 saves a PNG to Pictures/fractalSwing |

**The panel** has six tabs:
- **Fractal:** family, Julia/Mandelbrot form, iterations, bailout, spin, swing speed and amount, drift, kaleidoscope, mirrors, freeze.
- **Swings:** one card per parameter. Centre, amplitude, period, shape (sine, triangle, saw, square, pendulum, bounce, noise, steps), phase, audio link and amount.
- **Colour:** colour-by mode, palette (9, one custom), density, cycling, saturation, brightness, contrast, gamma, posterize, invert, orbit-trap shape and mix, stripes, inside colouring.
- **FX:** glow, video feedback (trails / screen / echo, decay, hue rotation), chromatic aberration, vignette, grain, scanlines, render quality.
- **Audio:** listen switch, reactivity, beat sensitivity, and the beat / bass / level / treble / mid mappings.
- **Presets:** 12 built-in looks, your own saved presets, randomize, mutate, reset, and copy/paste settings as JSON.

## Features
- **11 fractal families**, each in Julia form (c swings) or Mandelbrot form (z₀ swings): Quadratic, Burning Ship, Tricorn, Multibrot (swinging exponent), Phoenix, Celtic, Ducks, Kali, Newton, Box Fold (2D Mandelbox), Sine.
- **16 swings**, all live: c real/imaginary, zoom, rotation, pan X/Y, power, fold, extra, colour offset, colour density, trap X/Y, kaleidoscope angle, feedback zoom and rotation.
- **Colour engine:** smooth iteration, orbit trap (point / cross / ring), stripe average, angle; cosine palettes; inside colouring modes.
- **FX pipeline:** kaleidoscope (2–16 wedges) and mirrors, glow, video feedback, chromatic aberration, vignette, grain, scanlines, dithered output.
- **Audio sync:** bass / mid / treble / level and a beat detector. Beat → zoom kick, flash, aberration; bass → colour shift; level → brightness; treble → glow; mid → detail. Any swing can ride any signal.
- **Presets:** Julia Pendulum, Ducks Pond, Kali Cathedral, Burning Drift, Power Bloom, Newton Petals, Phoenix Breath, Box Fold Tunnel, Mandel Dive, Sine Silk, Feedback Storm, Celtic Lace.
- **Adaptive quality:** Auto holds about 45 fps by scaling the render resolution; or pick a fixed 0.35–1.0.
- **Web version:** the same shaders in WebGL2, with the same panel, presets and settings format (copy a look on the phone, paste it in the browser). Audio on the web comes from the microphone or, on desktop Chrome/Edge, another tab's audio.

## Docs
- [Design document](docs/DESIGN.md): the original prompt, every assumption and the pipeline
- [Changelog](CHANGELOG.md)
- [v1.0.0 build notes](1.0.0/BUILD-NOTES.md)

## About
Built with Kotlin and the Android framework only: an OpenGL ES 3 fragment-shader renderer with a feedback FBO chain,
and `android.media.audiofx.Visualizer` for the audio sync. Designed and iterated with Claude (Anthropic) through
Seth's `/ideatoapk` pipeline. The source repo is private.
