# Medal Social Desktop

Your social inbox, scheduler, and CRM — always one shortcut away.

[![Latest release](https://img.shields.io/github/v/release/Medal-Social/desktop?label=latest&color=000)](https://github.com/Medal-Social/desktop/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-black?logo=apple)](https://github.com/Medal-Social/desktop/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-Intel-black?logo=apple)](https://github.com/Medal-Social/desktop/releases/latest)
[![License](https://img.shields.io/badge/license-Proprietary-blue)](./LICENSE)

> Always points to the latest signed release.

---

## Why a desktop app?

- **Deep links open in Medal, not a new browser tab.** Click a `medal://...` link from email or Slack and it lands in your existing window.
- **One window across accounts.** Single-instance enforcement keeps the multi-account model coherent.
- **Window state survives restarts.** Size and position restore on relaunch — Linear-grade polish.
- **Silent auto-updates.** Updates download in the background and apply on next restart. No nagging dialogs.
- **Native notifications, system tray, global hotkey** *(coming in v1.1+)*.

## Download

Always grab the latest from [Releases](https://github.com/Medal-Social/desktop/releases/latest).

| Platform | File | What it is |
|---|---|---|
| macOS (Apple Silicon — M1, M2, M3, M4) | `Medal-Social-arm64.dmg` | Universal installer for Apple Silicon Macs |
| macOS (Intel) | `Medal-Social-x64.dmg` | Installer for Intel-based Macs |
| Windows | *(coming soon)* | Awaiting Microsoft Trusted Signing certification |
| Linux | *(coming soon)* | AppImage with detached GPG signature |

After downloading, open the `.dmg`, drag **Medal Social** to Applications, and launch.

### Verifying the signature

```bash
codesign --verify --deep --strict --verbose=2 /Applications/Medal\ Social.app
spctl --assess --type execute --verbose /Applications/Medal\ Social.app
```

A signed and notarized build will report `accepted` and `source=Notarized Developer ID`. SHA256 checksums for every artifact are listed in `SHA256SUMS.txt` on each release.

## How it works

The desktop app is a small native shell (built with [Tauri](https://tauri.app)) that loads `https://app.medalsocial.com` over HTTPS. It's the same product you use in your browser, with the additions above. Auto-updates check `https://ota.medalsocial.com` every six hours; the update payload itself is hosted on this repo's Releases page and verified at install time against a public key baked into the binary.

```
Desktop app   →   app.medalsocial.com   ←   apps/web (React)
                                         ↑
                                         Convex backend
                                         
Update check  →   ota.medalsocial.com   →   GitHub Releases (this repo)
                  (Cloudflare Worker)
```

## Roadmap

- **v1.0** — macOS shell with deep-links, single-instance, window state, silent auto-update *(this release)*
- **v1.1** — Native notifications for mentions / DMs / comments
- **v1.2** — System tray menu (Compose, Open Inbox, Toggle Window) and dock unread badge
- **v1.3** — Global hotkey to summon the composer from anywhere
- **v1.4** — Beta release channel + Settings → Apps page in the web app

Windows and Linux builds will join the matrix as their respective signing infrastructure comes online.

## Privacy

The desktop app is a thin shell over the hosted Medal Social product. It does not collect telemetry beyond what `app.medalsocial.com` already collects (PostHog product analytics). Auto-updates check the OTA endpoint every six hours with a hashed install ID — no email, account, or personally identifying information is sent.

See the full [Medal Social privacy notice](https://medalsocial.com/privacy).

## Issues and feedback

File issues here. The source code is private; PRs to the public repo are not accepted, but bug reports and feature requests are welcomed via [Issues](https://github.com/Medal-Social/desktop/issues).

## License

Proprietary. © 2026 Medal Social, LLC. All rights reserved. See [LICENSE](./LICENSE).
