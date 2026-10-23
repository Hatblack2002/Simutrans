# Simutrans Android

Android ARM64 port/build workspace for Simutrans, using the upstream Simutrans engine and the existing SDL2 Android project as the baseline.

## Current approach

- Keep the upstream C++ engine; do not fork/rewrite the renderer without evidence that it is necessary.
- Use the existing Android app shell and SDL2 backend.
- Build an `arm64-v8a` debug APK in GitHub Actions first.
- Verify install, first launch, map loading, touch interaction, save and load before calling the port playable.
- Pakset choice is tracked separately: the upstream Android pre-build currently fetches pak64 and pak64.japan. pak128 is not assumed to be bundled.

## Build

The initial CI workflow is intended to assemble the Android project from pinned upstream repositories on a GitHub-hosted runner. The first successful build is a baseline, not proof of gameplay correctness.

## Upstream components

- Engine: https://github.com/simutrans/simutrans
- Android shell: https://github.com/simutrans/simutrans-android-project

The upstream engine is licensed under Artistic License 1.0. Paksets and downloaded assets have separate licensing; keep their licensing and attribution with any redistributable APK.
