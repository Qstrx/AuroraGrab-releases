# AuroraGrab — releases

Public Windows downloads and **update feed** for AuroraGrab. This repository
holds release files only; the application's source is maintained in a
separate private repository. Everything here is reachable over HTTPS without
an account, which is what lets installed copies update themselves.

## Download

Get the latest `AuroraGrab-2-Setup-<version>.exe` from
[Releases](../../releases/latest). The current version is **3.0.3**.

The installer is **not code-signed**, so Windows SmartScreen warns on first
run: choose **More info → Run anyway**. It installs per-user, with no
administrator prompt. After that, AuroraGrab keeps itself up to date from
this repository.

## How updates work

Every installed copy carries an `app-update.yml` that names this repository
and the `latest` channel — nothing else, and no credentials.

1. AuroraGrab checks shortly after it starts and then about every five hours.
   It reads `latest.yml` from the newest **published** release here. Drafts
   and prereleases are never offered, and an older version is never offered
   as an update.
2. When a newer version is available, it downloads only the blocks that
   changed, by comparing the blockmap of the installed version with the new
   one.
3. The downloaded installer is accepted only if its SHA-512 matches the one
   in `latest.yml`.
4. Installation never starts while a download or conversion is running.
   Settings and Library history are kept.

## What each release contains

| File | Purpose |
|---|---|
| `AuroraGrab-2-Setup-<version>.exe` | the installer |
| `AuroraGrab-2-Setup-<version>.exe.blockmap` | lets the updater fetch only the changed blocks |
| `latest.yml` | update manifest: version, size, SHA-512 |
| `SHA256SUMS.txt` | checksums for manual verification |
| `verification-<version>.md` | verification report, from 3.0.2 |
| `AuroraGrab-3.0.0-source-notices.zip` | bundled-component licenses, exact FFmpeg/yt-dlp core sources and provider provenance, from 3.0.0 |
| `SOURCE_NOTICES_SHA256SUMS.txt` | checksum for that source and notices archive (3.0.0 release) |

The archive's `OPEN_SOURCE_STATUS.md` describes an outstanding verification
gap for complete FFmpeg linked-library sources and provider build scripts.
It is not a verified complete corresponding-source package.

## Verifying a download

```powershell
Get-FileHash .\AuroraGrab-2-Setup-<version>.exe -Algorithm SHA256
```

Compare the result with the matching line in `SHA256SUMS.txt`.

## Rules for this repository

Installed copies depend on this repository exactly as it is, so:

- **Keep old releases and their blockmaps.** A differential update is
  computed against the version a user has; removing its blockmap forces a
  full re-download.
- **Never change the files of a published release.** Clients that already
  read the old `latest.yml` would reject the new bytes. A fix ships as a
  higher version.
- **Never reuse a version number**, and do not rename or transfer this
  repository: every installed copy has its name built in.
- **Publish through the release workflow.** It builds once, verifies the
  installer and creates a draft here; a maintainer installs the draft over the
  previous version before publishing it. Only then does the feed offer it.
