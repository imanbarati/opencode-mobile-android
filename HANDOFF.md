# HANDOFF — OpenCode Mobile Android

## Target
- GitHub repository: https://github.com/imanbarati/opencode-mobile-android
- Purpose: produce an unsigned Android ARM64 release APK from the app associated with the TestFlight invitation https://testflight.apple.com/join/M9eFEE1q
- Upstream selected for the Android implementation: https://github.com/alvarolorentedev/opencode-mobile
- Upstream observed version: 1.0.145 (checked 2026-11-10)

## Important distinction
The upstream project already contains a React Native / Expo Android app. This is a cross-platform Android implementation, not a reverse-engineering/decompilation of the iOS IPA. Preserve upstream attribution, license, and notices. Do not imply Apple TestFlight binaries were converted.

## Current repository state
This repo is initially empty. It is being initialized with:
- README.md
- HANDOFF.md
- .github/workflows/android-unsigned.yml

The workflow checks out upstream source into a separate directory, installs Node dependencies, runs Expo Android prebuild, disables the release build signing configuration, runs Gradle assembleRelease, checks that apksigner does not report a valid signature, uploads the APK as a workflow artifact, and publishes a GitHub Release.

## Build target
- Android ARM64 (arm64-v8a), matching upstream release architecture.
- APK output: opencode-mobile-unsigned-arm64.apk
- No keystore, passwords, or signing secrets should be needed.
- Unsigned APK is not directly installable on stock Android. A signed APK is required for installation; do not claim otherwise.

## Build steps / verification
1. Open Actions → Build unsigned Android APK.
2. Run workflow, optionally specifying upstream ref.
3. Inspect logs for npm install, Expo prebuild, Gradle build, zipalign, and unsigned verification.
4. Download artifact or GitHub Release.
5. Verify APK with Android build-tools apksigner; expected result is verification failure due to absent signature. Ensure the workflow explicitly tests for that expected failure.
6. Test by signing a copy with a test key only if installation is requested later.

## Follow-up engineering
- Decide whether to keep this as a build mirror or create a full source fork. The current GitHub integration supports file-level commits but not repository fork/import in this session.
- Pin upstream to a reviewed commit SHA for reproducible releases; do not use a moving main branch for long-term releases.
- Add upstream license and third-party notices only when retrieved and copied accurately.
- Add CI validation for dependency install and Expo config.
- Add checksums (SHA-256) for every APK release.
- Review package ID before distribution. Upstream defaults to app.getopencode; changing the application ID is an explicit product/distribution decision.
- Keep the app clearly independent and not affiliated with OpenCode maintainers or Apple.

## Status
Repository existence and admin/push access were confirmed. The initial commits and workflow are being created. No APK build is considered complete until a successful Actions run produces an artifact and a GitHub Release.