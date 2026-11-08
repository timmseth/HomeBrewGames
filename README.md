# HomeBrewGames

Seth's self-built games, ready to sideload. No stores, no ads, no tracking.

## Layout
```
Android/
  <Game>/
    README.md        about, how to play, install, permissions
    index.html       landing page (web version, or "coming soon")
    CHANGELOG.md
    docs/            design docs
    <version>/       the APK for that version + BUILD-NOTES.md
```
Signing keystores never go in this repo.

## Games

| Game | Platform | Latest | Web | |
|---|---|---|---|---|
| [**Dive**](Android/Dive/) | Android 8.0+ | [v1.3.0 APK](Android/Dive/1.3.0/dive-v1.3.0.apk) | [coming soon](Android/Dive/index.html) | A zen, tilt-controlled flOw-like descent into a fractal sea, with dynamic difficulty, a Spore-style creature Shaper, idle harvesters and a music-visualizer autopilot. |

## Installing an APK
1. Download the `.apk` on your Android phone.
2. Open it and allow **install unknown apps** for your browser or file manager when asked.
3. Updates install over older versions and keep your progress.

Each game's README lists the APK's SHA-256 so you can verify the download.
