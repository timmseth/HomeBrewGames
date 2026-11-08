# fractalSwing — design plan

## Original prompt (verbatim)

> /ideatoapk an interactive fractal animation generator you can adjust the swings of in real time with a focus on
> beautiful visuals and many many configuration options. Sync with audio for visual trippiness

(That chat was interrupted before anything was delivered; v1.0.0 was built from this prompt alone in a later session.)

## v1.0.0 — assumptions and choices

- **"Swings"** = oscillators. Each animatable parameter is a `Swing`: value = centre + amplitude · shape(t / period + phase)
  + audioAmount · audioSignal. Shapes: sine, triangle, saw, square (soft), pendulum (lingers at the extremes), bounce,
  noise (smooth random), steps. 16 swings: c real/imag, zoom (log₂), rotation, pan X/Y, power, fold scale, extra
  (Newton relaxation / box-fold min radius), colour offset, colour density ×, trap X/Y, kaleidoscope angle, feedback
  zoom and rotation. Global swing speed, swing amount, freeze, and a **drift** that random-walks every centre.
- **Fractals** (GPU, GLSL ES 3.0, one compiled program per family, `highp`): Quadratic, Burning Ship, Tricorn,
  Multibrot (swinging exponent), Phoenix, Celtic, Ducks and Kali (orbit-average colouring), Newton (perturbed cubic,
  swinging relaxation), 2D Box Fold (Mandelbox), Sine. Each in **Julia form** (pixel = z₀, c swings) or
  **Mandelbrot form** (pixel = c, z₀ swings).
- **Colour**: smooth iteration (sqrt-spread), orbit trap (point / cross / ring), stripe average, angle; cosine
  palettes (Rainbow, Aurora, Ocean, Fire, Candy, Neon, Ice, Mono, Custom with RGB frequency/phase), density, cycling,
  saturation / brightness / contrast / gamma, posterize, invert, inside colouring (solid / trap tint / stripe tint).
- **Pipeline**: fractal → render-scale FBO → post pass (12-tap glow, video feedback against the previous frame with
  zoom/rotation/decay/hue-rotation in trails (max), screen or echo (mix) mode, beat flash) → blit to screen (radial
  chromatic aberration, vignette, scanlines, grain, dither). Render scale 0.3–1.0; Auto adapts to hold ~45 fps.
- **Audio sync**: Android Visualizer on the output mix (session 0; needs RECORD_AUDIO, reads only what the phone
  plays). Bass / mid / treble / level with adaptive normalisation; spectral-flux beat detector. Global mappings:
  beat → zoom kick, flash, aberration; bass → colour shift; level → brightness; treble → glow; mid → detail. Any swing
  can add any signal (Audio link + amount).
- **Touch**: drag pans, pinch zooms, twist rotates, tap toggles the panel, double-tap resets the view, long-press
  randomizes. The panel (bottom sheet, tabs Fractal / Swings / Colour / FX / Audio / Presets) has ~150 controls.
- **Presets**: 12 built-in (Julia Pendulum, Ducks Pond, Kali Cathedral, Burning Drift, Power Bloom, Newton Petals,
  Phoenix Breath, Box Fold Tunnel, Mandel Dive, Sine Silk, Feedback Storm, Celtic Lace), user presets in app prefs,
  Randomize / Same fractal new look / Mutate, copy / paste settings as JSON via the clipboard.
- **Snapshots**: 📷 saves a PNG of the current frame to Pictures/fractalSwing (render resolution).
- Orientation follows the sensor; the current settings autosave and restore.

### Known gaps
- Float precision: zoom past about 2¹² (the slider's top) pixelates; no perturbation/arbitrary precision.
- Snapshots are at the render resolution, not the screen's.
- No 3D (raymarched) fractals yet; everything is a 2D plane.
- Audio capture can be blocked by some phones/apps (the Audio tab says so).
- Not yet run on a phone: shaders validated with glslang, Kotlin type-checked offline.
