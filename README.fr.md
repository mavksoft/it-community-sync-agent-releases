<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Canal officiel de téléchargement de l'agent de synchronisation IT-Community.<br>Synchronise SQL Server local (ERP) vers les portails MySQL cloud — sans ouvrir un seul port entrant.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <strong>🇫🇷 Français</strong> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Ce dépôt publie uniquement les releases officielles** — le code source est privé. Téléchargements signés, sommes de contrôle et flux de mise à jour automatique.

## Téléchargement

| | |
|---|---|
| 📥 **Installateur (recommandé)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — installe agent, service et watchdog |
| 🗜️ **Zip portable** | `SyncAgent-<version>.zip` dans chaque release — aussi utilisé par les mises à jour à distance |
| 🌍 **Site produit** | [it-community.online](https://it-community.online) · Panneau : mapeo.it-systems.es |

## Qu'est-ce que c'est

Un agent **Windows Server** qui synchronise les bases **SQL Server** locales (ERP IESA / Gesfincas et similaires) vers des portails **MySQL** dans le cloud — en toute sécurité et **sans ouvrir un seul port entrant** sur le serveur du client.

```
SQL Server local
      │  (lecture seule · écriture optionnelle contrôlée)
      ▼
IT-Community Sync Agent   ← service Windows headless (SYSTEM)
      │  WebSocket sécurisé (WSS · TLS vérifié · jeton)
      ▼
Relais sync-point.es      ← authentifié (X-Relay-Key)
      │
      ▼
Portail web / Mapeo       → destination MySQL · panneau de contrôle
```

## Fonctionnalités

- **Zéro port entrant** — l'agent n'ouvre que des connexions sortantes ; le pare-feu du client n'est pas touché.
- **Incrémental réel** — Change Tracking / rowversion, checkpoints delta par table ; rien d'inchangé n'est recopié.
- **Vraiment headless** — tourne en Scheduled Task sous SYSTEM, sans session utilisateur ni RDP ouvert ; watchdog auto-relanceur inclus.
- **Géré depuis le cloud** — panneau sur mapeo.it-systems.es avec état en direct, configuration à distance, visionneuse de logs et écriture on/off.
- **Auto-mise à jour signée** — téléchargement vérifié SHA-256 avec rollback automatique si la nouvelle version ne démarre pas.
- **Supervision** — badges online/offline et alertes email avant les synchronisations programmées.

## Mode d'emploi

1. Téléchargez `IT-Community-Sync-Agent-Setup-<version>.exe` depuis la dernière release.
2. Exécutez-le **en administrateur** — il installe l'agent, crée la Scheduled Task (SYSTEM) et le watchdog automatiquement.
3. Puis ouvrez `agent.exe` une fois pour enregistrer les identifiants.
4. Alternative manuelle : décompressez le zip dans `C:\Sincronizador\agent`, lancez `agent.exe` pour les identifiants, puis `instalar_servicio.bat` en administrateur.
5. Depuis le panneau Mapeo, supervisez l'état, modifiez la configuration et activez/désactivez l'écriture distante.

## Configuration requise

Windows Server (ou Windows 10/11) · Accès à l'instance SQL Server source · Connectivité sortante HTTPS/WSS uniquement — aucun port entrant.

## Contenu de ce dépôt

- `IT-Community-Sync-Agent-Setup-<version>.exe` — installateur complet (agent + service + watchdog)
- `SyncAgent-<version>.zip` — paquet portable, aussi utilisé pour les mises à jour à distance
- `SyncAgent-<version>.sha256` — somme de contrôle pour vérification

[Dernière version](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## Questions fréquentes

**Faut-il ouvrir des ports ou du NAT sur le pare-feu du client ?**  
Non. L'agent n'établit que des connexions sortantes WSS/TLS vers le relais — il fonctionne derrière tout pare-feu d'entreprise standard.

**Que se passe-t-il si le serveur redémarre ou l'agent plante ?**  
La Scheduled Task le démarre au boot et le watchdog le relance en cas de crash ; le panneau marque l'agent offline s'il ne répond plus.

**Peut-il écrire en retour dans l'ERP ?**  
L'écriture est optionnelle et contrôlée — activable depuis le panneau Mapeo.

## Assistance

- Produit : [it-community.online](https://it-community.online)
- Panneau de gestion : mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
