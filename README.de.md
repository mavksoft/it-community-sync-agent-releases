<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Offizieller Download-Kanal für den IT-Community Sync Agent.<br>Synchronisiert lokale SQL-Server (ERP) mit MySQL-Portalen in der Cloud — ohne einen einzigen eingehenden Port zu öffnen.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <strong>🇩🇪 Deutsch</strong> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Dieses Repository veröffentlicht ausschließlich offizielle Binär-Releases** — der Quellcode ist privat. Signierte Downloads, Prüfsummen und Auto-Update-Feeds.

## Download

| | |
|---|---|
| 📥 **Installer (empfohlen)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — installiert Agent, Dienst und Watchdog |
| 🗜️ **Portables Zip** | `SyncAgent-<Version>.zip` in jedem Release — auch für Remote-Updates verwendet |
| 🌍 **Produktseite** | [it-community.online](https://it-community.online) · Panel: mapeo.it-systems.es |

## Was ist das

Ein **Windows-Server**-Agent, der lokale **SQL-Server**-Datenbanken (ERP IESA / Gesfincas u. ä.) mit **MySQL**-Portalen in der Cloud synchronisiert — sicher und **ohne einen einzigen eingehenden Port** auf dem Kundenserver.

```
Lokaler SQL Server
      │  (nur lesen · optional kontrolliertes Schreiben)
      ▼
IT-Community Sync Agent   ← headless Windows-Dienst (SYSTEM)
      │  Sicheres WebSocket (WSS · verifiziertes TLS · Token)
      ▼
Relay sync-point.es       ← authentifiziert (X-Relay-Key)
      │
      ▼
Webportal / Mapeo         → MySQL-Ziel · Kontrollpanel
```

<p align="center"><img src="./screenshots/website.png" width="640" alt="screenshot"></p>

## Funktionen

- **Null eingehende Ports** — der Agent öffnet nur ausgehende Verbindungen; die Firewall bleibt unberührt.
- **Echt inkrementell** — Change Tracking / rowversion, Delta-Checkpoints pro Tabelle; Unverändertes wird nicht erneut kopiert.
- **Wirklich headless** — läuft als Scheduled Task unter SYSTEM, ohne Benutzersitzung oder offenes RDP; selbstneustartender Watchdog inklusive.
- **Cloud-verwaltet** — Panel auf mapeo.it-systems.es mit Live-Status, Remote-Konfiguration, Log-Viewer und Schreiben an/aus.
- **Signiertes Auto-Update** — SHA-256-verifizierter Download mit automatischem Rollback, falls die neue Version nicht startet.
- **Monitoring** — Online/Offline-Badges und E-Mail-Alerts vor geplanten Synchronisationen.

## So wird es verwendet

1. `IT-Community-Sync-Agent-Setup-<Version>.exe` aus dem neuesten Release laden.
2. **Als Administrator** ausführen — installiert Agent, Scheduled Task (SYSTEM) und Watchdog automatisch.
3. Danach `agent.exe` einmal öffnen, um die Zugangsdaten zu registrieren.
4. Manuelle Alternative: Zip nach `C:\Sincronizador\agent` entpacken, `agent.exe` für die Zugangsdaten ausführen, dann `instalar_servicio.bat` als Administrator.
5. Im Mapeo-Panel Status überwachen, Konfiguration bearbeiten und Remote-Schreiben ein-/ausschalten.

## Voraussetzungen

Windows Server (oder Windows 10/11) · Zugriff auf die SQL-Server-Quellinstanz · Nur ausgehende HTTPS/WSS-Verbindungen — keine eingehenden Ports.

## Was dieses Repository enthält

- `IT-Community-Sync-Agent-Setup-<Version>.exe` — Komplett-Installer (Agent + Dienst + Watchdog)
- `SyncAgent-<Version>.zip` — portables Paket, auch für Remote-Updates vom Panel
- `SyncAgent-<Version>.sha256` — Prüfsumme zur Verifizierung

[Neueste Version](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## Häufige Fragen

**Müssen Ports oder NAT in der Kunden-Firewall geöffnet werden?**  
Nein. Der Agent baut nur ausgehende WSS/TLS-Verbindungen zum Relay auf — funktioniert hinter jeder üblichen Firmenfirewall.

**Was passiert bei Neustart oder Absturz des Agents?**  
Die Scheduled Task startet ihn mit dem System und der Watchdog startet ihn bei Absturz neu; das Panel meldet den Agent offline, wenn er nicht mehr antwortet.

**Kann er ins ERP zurückschreiben?**  
Schreiben ist optional und kontrolliert — umschaltbar im Mapeo-Panel.

## Support

- Produkt: [it-community.online](https://it-community.online)
- Verwaltungspanel: mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
