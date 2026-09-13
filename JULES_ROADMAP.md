# WirePass Implementation Roadmap for Jules

## Phase 1: VpnService Exclusions (Current Priority)
- Locate `GoBackend.java` (or backend implementation) where `VpnService.Builder` establishes routes.
- Add dynamic app exclusion for `com.google.android.captiveportallogin` safely handled with `PackageManager.NameNotFoundException`.
- Verify build passes via `./gradlew assembleDebug`.

## Phase 2: CaptivePortalDetector Component
- Create `CaptivePortalDetector.kt` to monitor Wi-Fi network capabilities.
- Emit state updates: `DETECTED`, `AUTHENTICATING`, `VALIDATED`.
- Test integration with Android `ConnectivityManager`.

## Phase 3: Portal Resolution UI / Custom Tab Binding
- Implement authentication launcher that binds network context directly to physical Wi-Fi.
- Allow users to authenticate without manual tunnel toggling.
