# AuroraGrab — releases

Public Windows downloads and update feed for AuroraGrab. Installers are
reachable over HTTPS without an account. The application's development
repository is maintained separately.

## Download

Get the latest `AuroraGrab-2-Setup-<version>.exe` from
[Releases](../../releases/latest).

AuroraGrab 3.0.0 introduces the Aurora interface: Download, Convert, After
Effects and Library. Existing installations check this same public feed for
updates; settings and Library history are retained during the upgrade.

The installer is **not code-signed**, so Windows SmartScreen warns on first
run: choose **More info → Run anyway**. It installs per-user, with no
administrator prompt.

## What each release contains

| File | Purpose |
|---|---|
| `AuroraGrab-2-Setup-<version>.exe` | the installer |
| `AuroraGrab-2-Setup-<version>.exe.blockmap` | lets the updater fetch only the changed blocks |
| `latest.yml` | update manifest: version, size, SHA-512 |
| `SHA256SUMS.txt` | checksums for manual verification |
| `AuroraGrab-3.0.0-source-notices.zip` | bundled-component licenses, exact FFmpeg/yt-dlp core sources and provider provenance |
| `SOURCE_NOTICES_SHA256SUMS.txt` | checksum for that source and notices archive |

The archive's `OPEN_SOURCE_STATUS.md` describes an outstanding verification
gap for complete FFmpeg linked-library sources and provider build scripts.
It is not a verified complete corresponding-source package.

Older releases are kept on purpose: a differential update is computed against
the version you currently have, so removing an old blockmap would force a full
re-download for anyone still on it.

## Verifying a download

```powershell
Get-FileHash .\AuroraGrab-2-Setup-<version>.exe -Algorithm SHA256
```

Compare the result with the matching line in `SHA256SUMS.txt`.
