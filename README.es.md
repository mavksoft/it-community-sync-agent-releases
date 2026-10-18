<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Canal oficial de descargas del agente de sincronización de IT-Community.<br>Sincroniza SQL Server local (ERP) con portales MySQL en la nube — sin abrir ni un solo puerto entrante.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center"><a href="https://mavksoft.github.io/it-community-sync-agent-releases/"><img src="https://img.shields.io/badge/docs-mavksoft.github.io%2Fit-community-sync-agent-releases-blue" alt="docs"></a></p>

<p align="center">🌍 <strong>🇪🇸 Español</strong> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <a href="README.pt.md">🇵🇹 Português</a></p>

> **Este repositorio publica únicamente releases oficiales** — el código fuente es privado. Descargas firmadas, checksums y feeds de auto-actualización.

## Descarga

| | |
|---|---|
| <img src='https://raw.githubusercontent.com/mavksoft/it-community-sync-agent-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **Instalador (recomendado)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — instala agente, servicio y watchdog |
| <img src='https://raw.githubusercontent.com/mavksoft/it-community-sync-agent-releases/main/icons/windows.svg' width='15' style='vertical-align:-2px' alt='windows'> **Zip portátil** | `SyncAgent-<versión>.zip` en cada release — también usado por las actualizaciones remotas |
| <img src='https://it-community.online/assets/logo.png' width='15' style='vertical-align:-2px'> **Web del producto** | [it-community.online](https://it-community.online) · Panel: mapeo.it-systems.es |

## Qué es

Agente para **Windows Server** que sincroniza bases de datos **SQL Server** locales (ERP IESA / Gesfincas y similares) hacia portales **MySQL** en la nube — de forma segura y **sin abrir ni un solo puerto** en el servidor del cliente.

```
SQL Server local
      │  (solo lectura · escritura opcional controlada)
      ▼
IT-Community Sync Agent   ← servicio Windows headless (SYSTEM)
      │  WebSocket seguro (WSS · TLS verificado · token)
      ▼
Relay sync-point.es       ← autenticado (X-Relay-Key)
      │
      ▼
Portal web / Mapeo        → MySQL destino · panel de control
```

<p align="center"><img src="./screenshots/website.png" width="640" alt="screenshot"></p>

## Funciones

- **Cero puertos entrantes** — el agente solo abre conexiones salientes; el firewall del cliente no se toca.
- **Incremental real** — Change Tracking / rowversion, checkpoints delta por tabla; no re-copia lo que no cambió.
- **Headless de verdad** — corre como Scheduled Task en cuenta SYSTEM, sin sesión de usuario ni RDP abierto; watchdog auto-relanzador incluido.
- **Gestionado desde la nube** — panel en mapeo.it-systems.es con estado en vivo, configuración remota, visor de logs y escritura on/off.
- **Auto-actualización firmada** — descarga verificada por SHA-256 con rollback automático si la nueva versión no arranca.
- **Monitorización** — badges online/offline y alertas por email antes de las copias programadas.

## Cómo se usa

1. Descarga `IT-Community-Sync-Agent-Setup-<versión>.exe` de la última release.
2. Ejecútalo **como administrador** — instala el agente, crea la Scheduled Task (SYSTEM) y el watchdog automáticamente.
3. Al terminar, abre `agent.exe` una vez para registrar las credenciales.
4. Alternativa manual: descomprime el zip en `C:\Sincronizador\agent`, ejecuta `agent.exe` para registrar credenciales y luego `instalar_servicio.bat` como administrador.
5. Desde el panel Mapeo supervisa el estado, edita la configuración y activa o desactiva la escritura remota.

## Requisitos

Windows Server (o Windows 10/11) · Acceso a la instancia SQL Server origen · Solo conectividad saliente HTTPS/WSS — ningún puerto entrante.

## Qué contiene este repositorio

- `IT-Community-Sync-Agent-Setup-<versión>.exe` — instalador completo (agente + servicio + watchdog)
- `SyncAgent-<versión>.zip` — paquete portátil, también usado para actualizaciones remotas desde el panel
- `SyncAgent-<versión>.sha256` — checksum para verificación

[Última release](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## Preguntas frecuentes

**¿Hay que abrir puertos o hacer NAT en el firewall del cliente?**  
No. El agente solo establece conexiones salientes WSS/TLS hacia el relay — funciona tras cualquier firewall corporativo estándar.

**¿Qué pasa si el servidor se reinicia o el agente muere?**  
La Scheduled Task lo arranca con el sistema y el watchdog lo relanza si cae; el panel marca el agente offline si deja de responder.

**¿Puede escribir de vuelta en el ERP?**  
La escritura es opcional y controlada — se activa/desactiva desde el panel Mapeo.

## Soporte

- Producto: [it-community.online](https://it-community.online)
- Panel de gestión: mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
