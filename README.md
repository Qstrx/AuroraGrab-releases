# AuroraGrab — releases

Download host for [AuroraGrab 2](https://github.com/Qstrx/YTGUI). This
repository contains **no source code**: it exists so the application can fetch
its own updates over plain HTTPS, which requires the installer to be reachable
without credentials.

## Download

Get the latest `AuroraGrab-2-Setup-<version>.exe` from
[Releases](../../releases/latest).

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

Older releases are kept on purpose: a differential update is computed against
the version you currently have, so removing an old blockmap would force a full
re-download for anyone still on it.

## Verifying a download

```powershell
Get-FileHash .\AuroraGrab-2-Setup-<version>.exe -Algorithm SHA256
```

Compare the result with the matching line in `SHA256SUMS.txt`.
