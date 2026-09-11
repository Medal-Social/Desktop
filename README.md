# Medal Social Desktop

Your social inbox, scheduler, and CRM — always one shortcut away.

[![Latest release](https://img.shields.io/github/v/release/Medal-Social/Desktop?label=latest&color=000)](https://github.com/Medal-Social/Desktop/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-black?logo=apple)](https://github.com/Medal-Social/Desktop/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-Intel-black?logo=apple)](https://github.com/Medal-Social/Desktop/releases/latest)
[![Windows](https://img.shields.io/badge/Windows-x64-black)](https://ota.medalsocial.com/download/windows)
[![Linux](https://img.shields.io/badge/Linux-x64-black?logo=linux)](https://ota.medalsocial.com/download/linux)
[![License](https://img.shields.io/badge/license-Proprietary-blue)](./LICENSE)

> Always points to the latest signed release.

---

## Why a desktop app?

- **Deep links open in Medal, not a new browser tab.** Click a `medal://...` link from email or Slack and it lands in your existing window.
- **One window across accounts.** Single-instance enforcement keeps the multi-account model coherent.
- **Window state survives restarts.** Size and position restore on relaunch — Linear-grade polish.
- **Silent auto-updates.** Updates download in the background and apply on next restart. No nagging dialogs.
- **Native notifications, system tray, and desktop shortcuts.** Keep Medal available while working in other apps.

## Download

Choose your platform on the [downloads page](https://www.medalsocial.com/download), inside **Apps & downloads**, or below. These links select the newest available stable installer for each platform. Versioned files and checksums are also available in [Releases](https://github.com/Medal-Social/Desktop/releases/latest).

| Platform | Download | What it is |
|---|---|---|
| macOS (Apple Silicon) | [DMG](https://ota.medalsocial.com/download/macos/aarch64) | Signed and notarized Apple Silicon build |
| macOS (Intel) | [DMG](https://ota.medalsocial.com/download/macos/x64) | Signed and notarized Intel build |
| Windows x64 | [Installer](https://ota.medalsocial.com/download/windows) | Authenticode-signed by Medal Social AS |
| Linux x64 | [AppImage](https://ota.medalsocial.com/download/linux) | Ubuntu 22.04+ and compatible distributions; signed updater payload |

On macOS, open the `.dmg`, drag **Medal Social** to Applications, and launch. On Windows, run the installer.

On Linux, save the AppImage in a permanent location, allow it to run as a program, and launch it once before using browser sign-in. Normal AppImage launching requires FUSE 2; browser callback registration requires `xdg-utils` and `desktop-file-utils`. For example, on Ubuntu 22.04:

```bash
sudo apt install libfuse2 xdg-utils desktop-file-utils
chmod +x Medal-Social_*_x64.AppImage
./Medal-Social_*_x64.AppImage
```

### Verifying the signature

```bash
codesign --verify --deep --strict --verbose=2 /Applications/Medal\ Social.app
spctl --assess --type execute --verbose /Applications/Medal\ Social.app
```

A signed and notarized build will report `accepted` and `source=Notarized Developer ID`. SHA256 checksums for every artifact are listed in `SHA256SUMS.txt` on each release.

On Windows, check the installer in PowerShell:

```powershell
Get-AuthenticodeSignature .\Medal-Social_*_x64-setup.exe
```

The signature status should be `Valid`, with Medal Social AS as the publisher. All four updater payloads also carry Tauri updater signatures, verified automatically by the app. Linux uses this updater signature, rather than a separate GPG signature.

## How it works

The desktop app is a small native shell (built with [Tauri](https://tauri.app)) that loads `https://app.medalsocial.com` over HTTPS. It's the same product you use in your browser, with the additions above. Auto-updates check `https://ota.medalsocial.com` every six hours; the update payload itself is hosted on this repo's Releases page and verified at install time against a public key baked into the binary.

```
Desktop app   →   app.medalsocial.com   ←   apps/web (React)
                                         ↑
                                         Convex backend
                                         
Update check  →   ota.medalsocial.com   →   GitHub Releases (this repo)
                  (Cloudflare Worker)
```

## Desktop 1.9.0

Windows keeps native title-bar controls and follows the app's Light, Dark or System appearance, with Mica on supported Windows 11 systems. Ctrl+T and Ctrl+W preserve tab, pop-out and keep-running behavior. Desktop actions are also available in the app command palette.

Linux x64 joins the release pipeline with an AppImage, native File-menu actions and automatic updates. The website and app list all four desktop downloads.

## Privacy

The desktop app is a thin shell over the hosted Medal Social product. It does not collect telemetry beyond what `app.medalsocial.com` already collects (PostHog product analytics). Auto-updates check the OTA endpoint every six hours with a hashed install ID — no email, account, or personally identifying information is sent.

See the full [Medal Social privacy notice](https://medalsocial.com/privacy).

## Issues and feedback

File issues here. The source code is private; PRs to the public repo are not accepted, but bug reports and feature requests are welcomed via [Issues](https://github.com/Medal-Social/Desktop/issues).

## License

Proprietary. © 2026 Medal Social, LLC. All rights reserved. See [LICENSE](./LICENSE).
