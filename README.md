# IT-Community Sync Agent

**Canal oficial de descargas del agente de sincronización de IT-Community.**

Este repositorio público publica únicamente los binarios empaquetados
(GitHub Releases) y la documentación del producto. El código fuente se
desarrolla en un repositorio privado.

## Qué hace

Agente para **Windows Server** que sincroniza bases de datos
**SQL Server** locales (ERP IESA / Gesfincas y similares) hacia portales
**MySQL** en la nube — de forma segura y **sin abrir ni un solo puerto**
en el servidor del cliente:

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

## Características

- **Cero puertos entrantes**: el agente solo abre conexiones salientes.
- **Incremental real**: Change Tracking / rowversion, checkpoints delta
  por tabla — no re-copia lo que no cambió.
- **Headless de verdad**: corre como Scheduled Task en cuenta SYSTEM,
  sin sesión de usuario ni RDP abierto. Watchdog auto-relanzador incluido.
- **Gestionado desde la nube**: panel en mapeo.it-systems.es con estado
  en vivo, configuración remota, visor de logs, escritura on/off y
  **auto-actualización** (descarga firmada por SHA-256 con rollback
  automático si la nueva versión no arranca).
- **Monitorización**: badges online/offline, alertas por email antes de
  las copias programadas.

## Instalación

1. Descarga `SyncAgent-X.Y.Z.zip` de la última
   [release](../../releases).
2. Descomprime y ejecuta `agent.exe` una vez para registrar credenciales.
3. Ejecuta `instalar_servicio.bat` **como administrador** — queda como
   servicio con watchdog.

## Licencia

Software comercial de **IT-Community** — uso sujeto a licencia.
Consultas: [it-community.online](https://it-community.online)
