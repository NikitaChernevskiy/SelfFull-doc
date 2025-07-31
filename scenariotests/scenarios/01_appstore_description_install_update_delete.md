# SelfFull universal Mobile App Standards: Install / Update / Uninstall Requirements  
v1.0 – 31 July 2025

---

## Why We Need This Document  
This specification gives designers, developers, DevOps, QA, and compliance teams a **single, measurable contract** for the entire app-lifecycle on storefront devices. By defining what “good” looks like for installation, over-the-air updates, and full removal, we eliminate ambiguity, shorten release cycles, and ensure that SelfFull never breaks a user’s device storage, privacy expectations, or productivity flow. The document also provides auditors with concrete evidence that SelfFull complies with Google Play Core, Apple App Store, and platform data-retention rules from day one. Ultimately, it protects our brand and users while saving the company time and money.

---

## Installation Requirements (1 – 15)

1. **Storefront discoverability**  
   Searching “SelfFull” in the App Store or Play Store returns the official listing within the first five results, showing the correct publisher “SelfFull, Inc.”, icon, and version tag.

2. **Supported OS bands**  
   App installs cleanly on **iOS 14 + / iPadOS 14 + / macOS 11 + (M-series)** and **Android 8.0 (API 26)+** reference devices.

3. **Bundle size cap**  
   Download payload ≤ 150 MB over cellular to avoid store download prompts; larger assets must ship via on-demand or install-time asset packs.

4. **Code signing**  
   Every build is signed with a production certificate; signature verification passes during install with no “Untrusted Developer” dialogs.

5. **First-launch latency**  
   Cold start ≤ 5 s on Pixel 5 and iPhone SE (2nd gen) when opened immediately after installation.

6. **Permissions gating**  
   No runtime permission prompts appear **before** the first screen renders; all optional permissions are deferred until feature use.

7. **Integrity checks**  
   Installation passes Google Play Integrity API and Apple App Attest checks on first run; failures block login and log actionable analytics.

8. **Store receipt verification**  
   Store receipt or purchase token is validated on first launch and logged to telemetry.

9. **Rollback safety**  
   The previous public version remains available for download for at least 30 days after a new version ships.

10. **Network resilience**  
    Installation resumes automatically after transient network loss (e.g., toggling airplane mode up to 60 s during download).

11. **Battery impact**  
    Install process draws < 8 % battery on reference devices; metrics captured via Android Battery Historian and iOS Instruments.

12. **Storage check**  
    Installer blocks with friendly message if free space < 2× bundle size; resumes automatically after space is freed.

13. **Anti-tamper**  
    The APK/AAB or IPA fails to install if modified; QA verifies SHA-256 digest matches manifest.

14. **Accessibility post-install**  
    Upon first launch, app registers dynamic-text categories and VoiceOver/TalkBack labels are discoverable.

15. **Analytics event**  
    Emit `installation_complete` with device model, OS, and store region; confirm ingestion within 5 minutes.

---

## Update Requirements (16 – 30)

16. **In-app update compliance (Android)**  
    Integrate Google Play Core In-App Updates (flexible + immediate) and surface the prompt when update is available.

17. **App Store phased release (iOS)**  
    Use App Store “Phased Release” at 1 %→5 %→10 %→20 %→50 %→100 % over 7 days unless critical-fix flag is set.

18. **Silent auto-update**  
    When automatic updates are enabled, SelfFull updates in the background and relaunches into the last-viewed screen.

19. **Versioning scheme**  
    Semantic versioning `MAJOR.MINOR.PATCH`; `CFBundleShortVersionString` / `versionName` must match store listing exactly.

20. **Delta size optimisation**  
    Differential update package ≤ 40 % of the full install size.

21. **Session continuity**  
    After update, user session, preferences, and cached content remain intact; no forced re-login unless major version bump.

22. **Schema migrations**  
    Mobile DB migrations execute idempotently; failure triggers automatic rollback and telemetry alert.

23. **Update progress UX**  
    Flexible update shows a progress bar inside the SelfFull UI without obscuring interactive elements.

24. **Deferred reminder**  
    If a user postpones the update three times, app triggers a persistent, dismissible banner until updated.

25. **Background download limits**  
    Updates download over cellular only if payload < 50 MB; otherwise Wi-Fi is enforced.

26. **Crash-free first launch**  
    Crash-free sessions after update ≥ 99.8 % in production analytics.

27. **Integrity re-check**  
    Post-update receipts or tokens are revalidated before allowing access to the dashboard.

28. **Roll-forward enforcement**  
    App blocks downgrades except when user joins TestFlight or Internal-Testing track.

29. **Accessibility regression test**  
    Updates must maintain or improve WCAG AA compliance (contrast, labels).

30. **Analytics event**  
    Emit `update_complete` with old/new version numbers; verify ingestion in dashboard.

---

## Uninstall / Off-boarding Requirements (31 – 45)

31. **System-level delete only**  
    App can be removed via standard OS gestures; no proprietary uninstaller.

32. **Data purging (Android)**  
    All files under `getFilesDir()` and cache directories are deleted; no residual data on external storage.

33. **Keychain & prefs (iOS)**  
    Sensitive identifiers are not stored in a keychain group that survives uninstall; QA verifies fresh anonymous ID after reinstall.

34. **Push token invalidation**  
    Uninstall triggers a `NotRegistered` response from FCM/APNs; backend stops sending notifications within 24 h.

35. **Server-side cleanup**  
    Backend schedules GDPR “Right to Forget” purge for orphaned accounts with no device attached for > 30 days.

36. **Cache quota reset**  
    After reinstall, disk usage starts ≤ 100 KB, confirming caches were cleared.

37. **Offload support (iOS)**  
    Offloading retains user documents but removes binary; reinstall restores prior documents.

38. **Background task cleanup**  
    No leftover background fetch or WorkManager jobs remain after uninstall.

39. **Analytics ingestion**  
    Backend ingests store analytics “App Deletions” daily and reconciles with MAU churn.

40. **Reinstall experience**  
    Fresh reinstall presents Welcome/onboarding, not last-session dashboard, unless user logs in.

41. **Local notifications purge**  
    Scheduled local notifications are cancelled at uninstall; none fire after reinstall unless rescheduled.

42. **Shared storage hygiene (Android)**  
    If exporting to `Documents/SelfFull`, place a `.nomedia` marker and warn users files remain until manually deleted.

43. **Compliance logs**  
    Device-side uninstall events are captured by MDM Remove-Application command for managed devices.

44. **Legal artefacts**  
    EULA and Privacy Policy versions linked to the uninstalled build are archived for seven years.

45. **Re-registration metric**  
    Measure % of users who reinstall within 14 days; target ≤ 5 % uninstall-then-reinstall churn.

---