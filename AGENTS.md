# Agent Instructions

## Toolchain
- Use the Gradle wrapper (`./gradlew`), not a system Gradle installation.
- Use JDK 17 as in `.github/workflows/build.yml`; Android SDK versions are defined in `build.gradle`.
- Set `GRADLE_MICROG_VERSION_WITHOUT_GIT=1` for local validation without version tags, matching CI.
- Keep machine-specific SDK paths and `modules.*` overrides in ignored `local.properties`.

## Commands
- Run from the repository root with the environment setting above.
- Prefer the affected module's task; these are concrete examples.

| Task | Command |
|------|---------|
| Build main debug APK | `./gradlew :play-services-core:assembleDefaultDebug` |
| Lint main debug variant | `./gradlew :play-services-core:lintDefaultDebug` |
| Run Nearby crypto test | `./gradlew :play-services-nearby-core:testDebugUnitTest --tests org.microg.gms.nearby.exposurenotification.CryptoTest` |
| Lint Nearby implementation | `./gradlew :play-services-nearby-core:lintDebug` |

## Key Conventions
- Check `settings.gradle` for project names: `sublude` maps paths such as `play-services-nearby/core` to `:play-services-nearby-core`, not `:play-services-nearby:core`.
- Keep client API changes in the corresponding `play-services-*` module and service implementation changes in its `core/` subtree where present.
- Edit Wire inputs under module `src/main/proto/`, not generated sources under `build/`; Gradle regenerates them during builds.
- Preserve the distinction between `applicationNamespace` and `basePackageName` in `build.gradle`; the fork's application ID is not its Google API namespace.
- Keep flavor account-type resources aligned with the shared account type as documented in `play-services-core/build.gradle`.

## References
| Need | File |
|------|------|
| Project overview, APK variants, fork translation link | `README.md` |
| Module mapping and optional modules | `settings.gradle` |
| SDK, dependencies, package identity, versioning | `build.gradle` |
| CI validation | `.github/workflows/build.yml` |
| Release builds and APK variants | `.github/workflows/release.yml` |
| Translation synchronization | `crowdin.yml`, `.github/workflows/crowdin_pull.yml`, `.github/workflows/crowdin_push.yml` |
| License | `LICENSE` |
