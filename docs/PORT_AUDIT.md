# Port audit and acceptance criteria

## Architecture decision
Use the upstream Simutrans C++ engine and the existing SDL2 Android project as the baseline. Do not replace the engine or add a second touch-input system until runtime tests show a concrete need.

## Confirmed from upstream source
- Android is an existing CMake target; Android builds produce the native shared library and include `src/android/android.cc`.
- `SIMUTRANS_BACKEND=sdl2` selects the SDL2 system backend, software display renderer, and SDL2 sound implementation.
- The Android project uses an SDLActivity-derived Java entry point and loads `SDL2` plus `simutrans`.
- The upstream Android asset preparation script fetches pak64 and pak64.japan. It does not currently establish pak128 as the included default.
- The SDL2 backend already handles SDL touch events. Existing gestures must be tested before adding custom overlays or remapping.

## Build sequence
1. Reproduce the upstream Android build with the current source and submodules on a clean CI runner.
2. Produce an ARM64 debug APK and retain it as a workflow artifact.
3. Confirm installation and first launch on an Android ARM64 device.
4. Confirm assets unpack and a map loads.
5. Test pan, zoom, long-press/right-click, keyboard, Back/Escape, orientation, and UI scale.
6. Test a basic construction action, save, and reload.
7. Select and document the distributable pakset only after checking its size, redistribution terms, and first-run performance.

## Acceptance gate
A successful Gradle task is only a build result. Do not describe the app as playable until installation, map loading, basic touch interaction, construction, and save/reload have been verified. Record commit SHAs, CI logs, APK artifact, and device test notes for each accepted milestone.

## Asset licensing
The engine, paksets, fonts, sound assets, and addons can have different licensing terms. Keep source notices and asset-specific licensing separate; do not assume that a publicly downloadable pakset can be redistributed inside an APK without checking its terms.
