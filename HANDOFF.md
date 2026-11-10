# HANDOFF — OpenCode Mobile Android

## Target
- Repository: https://github.com/imanbarati/opencode-mobile-android
- Upstream Android app: https://github.com/alvarolorentedev/opencode-mobile
- TestFlight reference: https://testflight.apple.com/join/M9eFEE1q
- Upstream package version observed 2026-11-10: 1.0.145

## Findings
The upstream app already has a React Native / Expo Android implementation (Expo SDK 58, React Native 0.88). This is not a decompile or conversion of an iOS IPA. The upstream `scripts/build-android-release.mjs` requires keystore credentials, so it must NOT be used for the unsigned build.

## Workflow
`.github/workflows/android-unsigned.yml` checks out upstream source at a selected branch/tag/SHA, runs `npm ci`, Java 21 setup, Expo Android prebuild, strips the release buildType signingConfig assignment, then runs Gradle `assembleRelease` for arm64-v8a. It copies the APK, verifies `apksigner verify` fails (expected), checks zipalign, generates SHA-256, uploads an Actions artifact, and publishes a GitHub Release.

## Build / verification
1. Actions → Build unsigned Android APK → Run workflow.
2. Input `upstream_ref`: main, tag, or commit SHA.
3. Wait for successful job and download `opencode-mobile-unsigned-arm64`.
4. Confirm release APK exists, `apksigner verify` fails, zipalign passes, and checksum matches.
5. Do not claim build success until Actions reports success and artifact/release is present.

## Caveats
- An unsigned APK cannot be installed on a stock Android device. Installation requires signing.
- This repo is a build wrapper, not a complete source fork.
- Do not commit keystores, passwords, tokens, or signing secrets.
- Preserve upstream licensing and third-party notices. Check the current upstream license before redistributing.
- Upstream default Android package ID is `app.getopencode`; changing it can affect deep links, app data, and notifications.
- Pin upstream to a reviewed commit SHA after validating the first successful build for reproducibility.

## Next steps for the next agent
Fix any CI/prebuild/Gradle errors; verify artifact and release; calculate/compare SHA-256; pin upstream SHA; only create an installable signed variant if explicitly requested and with clear signing disclosure.
