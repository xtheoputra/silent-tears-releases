# Silent Tears Releases

Official Windows installers for Silent Tears, an offline security monitor for Windows 10 and 11 PCs, for people who want to see who signs in, what runs and what connects on their own machine.

**Status:** Released. Current version **0.9.0** (2026-10-15). Product site: [silent-tears-web.vercel.app](https://silent-tears-web.vercel.app).

## Overview

This repository hosts release installers only. The application source is private and is not published here; there is nothing to build or contribute to in this repository.

Silent Tears runs in the background on the PC it protects. It reads Windows itself (processes, sign-ins, network connections, event logs, registry, services, scheduled tasks), writes every finding to hash-chained local logs, joins related events into cases and maps them to MITRE ATT&CK techniques. Its analyst panel, AEGIS, explains each finding and proposes a response; a person confirms before anything is terminated, blocked, quarantined or isolated.

It sends no telemetry. The only data it can send off the machine is an optional Telegram notification, which is off by default.

## Features

What version 0.9.0 does:

- Sign-ins and sessions, including remote sessions, failed sign-ins, locked accounts and RDP logons (the Security event log needs Administrator).
- New processes and their parent chain, with an encoded-command decoder and Authenticode signature checks.
- Persistence in 28 locations, including scheduled tasks, WMI event subscriptions, Image File Execution Options, Winlogon and COM hijacking.
- Inbound and outbound connections, suspicious ports, call-home timing patterns, and per-process DNS queries once the Windows DNS client channel is switched on.
- An offline file scanner that reads file structure (packed sections, macros, alternate data streams, deceptive names) with a reversible quarantine. It has no signature feed and no cloud lookup.
- A correlation engine with 12 attack-chain rules and an offline catalogue of 150 MITRE ATT&CK techniques.
- AEGIS, an analyst panel that reads through read-only tools and acts only after a confirmation button is pressed.
- Hash-chained logs, a session ledger and a configuration manifest that make later edits to the evidence visible.
- Optional, off by default: Telegram notifications, camera photos on signs of someone physically at the keyboard, ransomware canary files, automatic blocking.

Silent Tears is not an antivirus. Keep your main antivirus enabled.

## System requirements

- Windows 10 or Windows 11, 64-bit.
- Administrator rights once, to install into Program Files. The application then runs as a standard user.
- No Python or other runtime is needed: the installer includes a private Python 3.12 runtime, every dependency and the Visual C++ Runtime when it is missing.
- The user interface is in **Indonesian**.

## Download

| Version | Date | File | Size | SHA-256 |
| --- | --- | --- | --- | --- |
| 0.9.0 | 2026-10-15 | [`SilentTears-Setup-0.9.0.exe`](https://github.com/xtheoputra/silent-tears-releases/releases/download/v0.9.0/SilentTears-Setup-0.9.0.exe) | 126,823,627 bytes | `072e8ac6f2b91f9126665d5796717ea200c3376b651a62d77c7828898684f83b` |

All releases are listed on the [Releases page](https://github.com/xtheoputra/silent-tears-releases/releases).

### Verify the download

In PowerShell, from the folder that holds the installer:

```powershell
Get-FileHash .\SilentTears-Setup-0.9.0.exe -Algorithm SHA256
```

The `Hash` value must equal the SHA-256 above. If it does not, delete the file and do not run it.

### Unsigned installer

The installer is not code-signed yet. Windows SmartScreen shows "Unknown publisher" and may say "Windows protected your PC". After verifying the SHA-256, choose **More info**, then **Run anyway**.

## Install and uninstall

1. Run `SilentTears-Setup-0.9.0.exe` and accept the Administrator prompt.
2. The application installs per machine into Program Files.
3. Settings, evidence logs and snapshots are stored per user in `%LOCALAPPDATA%\SilentTears`.

Uninstall from **Settings → Apps**. Uninstalling removes the autostart entry and any ransomware canary files that are still intact, and keeps the evidence logs.

## Privacy

- No telemetry, no accounts and no cloud lookups.
- Telegram notifications are optional and off by default.
- The camera is off by default, asks for consent when switched on, and stores photos on the PC, DPAPI-encrypted when Windows makes DPAPI available.
- Use Silent Tears only on a PC you own or have explicit permission to monitor.

## Roadmap

- A code-signed installer, once a code-signing certificate is in place.
- A pilot on PCs other than the author's before version 1.0.0.
- An English user interface.

## Security

To report a vulnerability, see [`SECURITY.md`](SECURITY.md). Please do not open a public issue for security problems.

## License

Proprietary — © 2026 Harasta Rahman Tri Putra (xTheo Labs). All rights reserved. See [`LICENSE`](LICENSE).

The installer bundles third-party components under their own licences, including Python, Qt for Python (PySide6), psutil, pywin32, requests, OpenCV and NumPy. IP-to-country data is from the [db-ip.com IP to Country Lite](https://db-ip.com/db/download/ip-to-country-lite) database (CC-BY-4.0).

---

Built by [xTheo Labs](https://xtheo-labs.vercel.app) · [@xtheoputra](https://github.com/xtheoputra)
