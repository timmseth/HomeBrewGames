# fractalSwing v1.0.0 — First build

- Built 2026-11-06 00:01 · versionCode 1 · applicationId `com.seth.fractalswing`
- Signed with the project's debug keystore (cert SHA-256 `1bf9628b…ef33af`). Later versions install over this one and keep your presets.
- Built from the original prompt only: *"an interactive fractal animation generator you can adjust the swings of in real time with a focus on beautiful visuals and many many configuration options. Sync with audio for visual trippiness."*

## What's in it
- **11 fractal families on the GPU**, each in Julia form (c swings) or Mandelbrot form (z₀ swings): Quadratic, Burning Ship, Tricorn, Multibrot (swinging exponent), Phoenix, Celtic, Ducks, Kali, Newton, Box Fold (2D Mandelbox), Sine.
- **16 swings**, each with centre, amplitude, period, shape (sine / triangle / saw / square / pendulum / bounce / noise / steps), phase, and an optional audio link + amount: c real & imaginary, zoom, rotation, pan X/Y, power, fold, extra, colour offset, colour density, trap X/Y, kaleidoscope angle, feedback zoom & rotation. Plus global swing speed, swing amount, freeze and **Drift** (random-walks every centre).
- **Colour:** smooth iteration, orbit trap (point / cross / ring), stripes, angle; 9 palettes incl. a custom one; density, cycling, saturation / brightness / contrast / gamma, posterize, invert, three inside-colour modes.
- **FX:** kaleidoscope (2–16 wedges) and mirrors, glow, video feedback (trails / screen / echo, with decay, hue rotation and swinging zoom/rotation), chromatic aberration, vignette, grain, scanlines.
- **Audio sync** (Audio tab → switch on; Android asks for the record-audio permission, which only reads what the phone plays): bass / mid / treble / level and a beat detector. Beat → zoom kick, flash, aberration; bass → colour shift; level → brightness; treble → glow; mid → detail. Any swing can ride any signal.
- **12 built-in looks** (Presets tab), your own presets, Randomize / Same fractal new look / Mutate, copy & paste settings via the clipboard.
- **Touch:** drag to pan, pinch to zoom, twist to rotate, tap to hide/show the panel, double-tap resets the view, long-press randomizes. 📷 saves a snapshot to Pictures/fractalSwing. ≡ (top right) opens the panel.
- **Render quality:** Auto adapts the render resolution to hold about 45 fps; or pick a fixed 0.35–1.0.

## Known gaps
- Deep zoom past the slider's top (about 2¹²) pixelates: 32-bit float precision, no perturbation yet.
- Snapshots are saved at the render resolution, not the full screen resolution.
- Some phones block the output visualizer; the Audio tab's status line will say so.
