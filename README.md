# OpenCode Mobile Android build

Automated Android ARM64 release APK build for [alvarolorentedev/opencode-mobile](https://github.com/alvarolorentedev/opencode-mobile), using its existing React Native / Expo Android implementation.

## Build
Go to **Actions → Build unsigned Android APK → Run workflow**. Select an upstream ref (default `main`). Download the `opencode-mobile-unsigned-arm64` artifact. A successful run also publishes a GitHub Release with APK and SHA-256 checksum.

The workflow installs locked dependencies, runs Expo prebuild, removes the generated release signing assignment, builds `assembleRelease`, and verifies the APK is unsigned.

## Important
Unsigned APKs cannot be installed directly on standard Android devices; Android requires APK signatures. This build intentionally does not use or create a signing key.

This repository is a build wrapper, not a full source fork or a decompilation of the iOS TestFlight app. The Android implementation already exists upstream. Preserve upstream license and notices; this project is independent and is not affiliated with Apple or upstream maintainers.
