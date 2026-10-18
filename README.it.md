<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Canale ufficiale di download dell'agente di sincronizzazione IT-Community.<br>Sincronizza SQL Server locale (ERP) con i portali MySQL in cloud — senza aprire nemmeno una porta in ingresso.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <strong>🇮🇹 Italiano</strong> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Questo repository pubblica solo release binarie ufficiali** — il codice sorgente è privato. Download firmati, checksum e feed di aggiornamento automatico.

## Download

| | |
|---|---|
| 📥 **Installer (consigliato)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — installa agente, servizio e watchdog |
| 🗜️ **Zip portable** | `SyncAgent-<versione>.zip` in ogni release — usato anche dagli aggiornamenti remoti |
| 🌍 **Sito prodotto** | [it-community.online](https://it-community.online) · Pannello: mapeo.it-systems.es |

## Che cos'è

Un agente per **Windows Server** che sincronizza database **SQL Server** locali (ERP IESA / Gesfincas e simili) verso portali **MySQL** in cloud — in modo sicuro e **senza aprire nemmeno una porta in ingresso** sul server del cliente.

```
SQL Server locale
      │  (sola lettura · scrittura opzionale controllata)
      ▼
IT-Community Sync Agent   ← servizio Windows headless (SYSTEM)
      │  WebSocket sicuro (WSS · TLS verificato · token)
      ▼
Relay sync-point.es       ← autenticato (X-Relay-Key)
      │
      ▼
Portale web / Mapeo       → destinazione MySQL · pannello di controllo
```

<p align="center"><img src="./screenshots/website.png" width="640" alt="screenshot"></p>

## Funzionalità

- **Zero porte in ingresso** — l'agente apre solo connessioni in uscita; il firewall del cliente non viene toccato.
- **Incrementale reale** — Change Tracking / rowversion, checkpoint delta per tabella; ciò che non cambia non viene ricopiato.
- **Davvero headless** — gira come Scheduled Task sotto SYSTEM, senza sessione utente né RDP aperto; watchdog auto-rilanciante incluso.
- **Gestito dal cloud** — pannello su mapeo.it-systems.es con stato in tempo reale, configurazione remota, visualizzatore log e scrittura on/off.
- **Auto-aggiornamento firmato** — download verificato SHA-256 con rollback automatico se la nuova versione non si avvia.
- **Monitoraggio** — badge online/offline e avvisi email prima delle sincronizzazioni programmate.

## Come si usa

1. Scarica `IT-Community-Sync-Agent-Setup-<versione>.exe` dall'ultima release.
2. Eseguilo **come amministratore** — installa l'agente, crea la Scheduled Task (SYSTEM) e il watchdog automaticamente.
3. Poi apri `agent.exe` una volta per registrare le credenziali.
4. Alternativa manuale: scomprimi lo zip in `C:\Sincronizador\agent`, esegui `agent.exe` per le credenziali, poi `instalar_servicio.bat` come amministratore.
5. Dal pannello Mapeo supervisiona lo stato, modifica la configurazione e attiva/disattiva la scrittura remota.

## Requisiti

Windows Server (o Windows 10/11) · Accesso all'istanza SQL Server di origine · Solo connettività in uscita HTTPS/WSS — nessuna porta in ingresso.

## Cosa contiene questo repository

- `IT-Community-Sync-Agent-Setup-<versione>.exe` — installer completo (agente + servizio + watchdog)
- `SyncAgent-<versione>.zip` — pacchetto portable, usato anche per aggiornamenti remoti dal pannello
- `SyncAgent-<versione>.sha256` — checksum per la verifica

[Ultima release](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## Domande frequenti

**Bisogna aprire porte o fare NAT sul firewall del cliente?**  
No. L'agente stabilisce solo connessioni in uscita WSS/TLS verso il relay — funziona dietro qualsiasi firewall aziendale standard.

**Cosa succede se il server si riavvia o l'agente muore?**  
La Scheduled Task lo avvia col sistema e il watchdog lo rilancia se cade; il pannello segna l'agente offline se smette di rispondere.

**Può scrivere di ritorno nell'ERP?**  
La scrittura è opzionale e controllata — si attiva/disattiva dal pannello Mapeo.

## Assistenza

- Prodotto: [it-community.online](https://it-community.online)
- Pannello di gestione: mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
