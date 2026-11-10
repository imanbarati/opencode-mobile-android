# OpenCode Mobile — Android build mirror

This repository builds an Android APK from the upstream OpenCode Mobile project.

- Upstream source: https://github.com/alvarolorentedev/opencode-mobile
- Upstream license and notices remain authoritative; see the upstream repository before redistributing.
- This repository contains build automation and handoff documentation. It is not a full source-code fork yet.

## Build an unsigned APK

1. Open **Actions → Build unsigned Android APK**.
2. Select **Run workflow**.
3. Wait for the job to finish.
4. Download the `opencode-mobile-unsigned-arm64.apk` artifact, or use the generated GitHub Release.

The workflow checks out the upstream source at the selected ref, installs dependencies, generates the native Android project with Expo, disables release signing, builds the ARM64 release APK, and verifies that the APK is unsigned.

## Install caveat

An unsigned APK cannot be installed directly by Android. Android requires APK signatures. This artifact is intended for inspection, signing with your own key, or further packaging. Do not confuse an unsigned APK with a signed debug APK.

## Build inputs

The workflow defaults to upstream `main`. You can supply a tag or branch through the workflow input.

## Scope

This is a build/port handoff wrapper around the existing React Native/Expo Android implementation. It does not claim that the iOS TestFlight binary itself was decompiled or translated.