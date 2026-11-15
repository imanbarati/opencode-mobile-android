# OpenCode Mobile — Android builds

Builds the upstream [OpenCode Mobile](https://github.com/alvarolorentedev/opencode-mobile) app for Android and publishes APKs to **GitHub Releases**.

## Installable APK (what you want)

1. **Actions → Build installable Android APK → Run workflow**
2. Wait for success
3. Download from [Releases](https://github.com/imanbarati/opencode-mobile-android/releases)  
   file: `opencode-mobile-debug-arm64.apk`

This build is **debug-signed** so Android will install it (sideload). It is not Play Store–ready.

## Unsigned build (legacy)

**Build unsigned Android APK** still exists for verification only — those APKs **cannot** be installed until signed.

## Notes

- This repo is a CI wrapper, not a full source fork.
- Upstream is React Native / Expo.
- Preserve upstream license and notices when redistributing.
