<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Official download channel for the IT-Community sync agent.<br>Syncs on-premises SQL Server (ERP) to cloud MySQL portals — without opening a single inbound port.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center"><a href="https://mavksoft.github.io/it-community-sync-agent-releases/"><img src="https://img.shields.io/static/v1?label=docs&message=mavksoft.github.io/it-community-sync-agent-releases&color=blue" alt="docs"></a></p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <strong>🇬🇧 English</strong> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **This repository publishes official binary releases only** — the source code is private. Signed downloads, checksums and auto-update feeds.

## Download

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/it-community-sync-agent-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **Installer (recommended)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — installs agent, service and watchdog |
| <img src='https://raw.githubusercontent.com/mavksoft/it-community-sync-agent-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **Portable zip** | `SyncAgent-<version>.zip` in every release — also used by remote updates |
| <img src='https://it-community.online/assets/logo.png' width='15' style='vertical-align:-2px'> **Product site** | [it-community.online](https://it-community.online) · Panel: mapeo.it-systems.es |

## What it is

A **Windows Server** agent that syncs on-premises **SQL Server** databases (IESA / Gesfincas ERP and similar) to cloud **MySQL** portals — securely and **without opening a single inbound port** on the client's server.

```
Local SQL Server
      │  (read-only · optional controlled write)
      ▼
IT-Community Sync Agent   ← headless Windows service (SYSTEM)
      │  Secure WebSocket (WSS · verified TLS · token)
      ▼
Relay sync-point.es       ← authenticated (X-Relay-Key)
      │
      ▼
Web portal / Mapeo        → MySQL destination · control panel
```

<p align="center"><img src="./screenshots/website.png" width="640" alt="screenshot"></p>

## Features

- **Zero inbound ports** — the agent only opens outbound connections; the client's firewall is untouched.
- **True incremental** — Change Tracking / rowversion, per-table delta checkpoints; nothing unchanged is re-copied.
- **Genuinely headless** — runs as a Scheduled Task under SYSTEM, no user session or open RDP; self-restarting watchdog included.
- **Cloud-managed** — panel at mapeo.it-systems.es with live status, remote configuration, log viewer and write on/off.
- **Signed auto-update** — SHA-256-verified download with automatic rollback if the new version fails to start.
- **Monitoring** — online/offline badges and email alerts before scheduled syncs.

## How to use it

1. Download `IT-Community-Sync-Agent-Setup-<version>.exe` from the latest release.
2. Run it **as administrator** — it installs the agent, creates the Scheduled Task (SYSTEM) and the watchdog automatically.
3. When done, open `agent.exe` once to register credentials.
4. Manual alternative: unzip to `C:\Sincronizador\agent`, run `agent.exe` to register credentials, then `instalar_servicio.bat` as administrator.
5. From the Mapeo panel, monitor status, edit configuration and toggle remote writes.

## Requirements

Windows Server (or Windows 10/11) · Access to the source SQL Server instance · Outbound HTTPS/WSS connectivity only — no inbound ports.

## What's in this repository

- `IT-Community-Sync-Agent-Setup-<version>.exe` — full installer (agent + service + watchdog)
- `SyncAgent-<version>.zip` — portable package, also used for remote updates from the panel
- `SyncAgent-<version>.sha256` — checksum for verification

[Latest release](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## FAQ

**Do we need to open ports or NAT on the client's firewall?**  
No. The agent only makes outbound WSS/TLS connections to the relay — it works behind any standard corporate firewall.

**What happens if the server reboots or the agent dies?**  
The Scheduled Task starts it at boot and the watchdog relaunches it if it crashes; the panel flags the agent offline if it stops responding.

**Can it write back to the ERP?**  
Writing is optional and controlled — toggled from the Mapeo panel.

## Support

- Product: [it-community.online](https://it-community.online)
- Management panel: mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
