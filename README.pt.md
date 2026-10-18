<p align="center">
  <img src="https://it-community.online/assets/logo.png" alt="IT-Community" width="96">
</p>

<h1 align="center">IT-Community Sync Agent</h1>

<p align="center">Canal oficial de downloads do agente de sincronização IT-Community.<br>Sincroniza SQL Server local (ERP) com portais MySQL na cloud — sem abrir uma única porta de entrada.</p>

<p align="center">
  <a href="https://it-community.online"><img src="https://img.shields.io/badge/website-it--community.online-0A84FF" alt="website"></a>
  <a href="https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest"><img src="https://img.shields.io/github/v/release/mavksoft/it-community-sync-agent-releases?label=latest" alt="latest release"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20Server-black" alt="Windows Server">
  <img src="https://img.shields.io/badge/license-commercial-orange" alt="commercial license">
</p>

<p align="center">🌍 <a href="README.es.md">🇪🇸 Español</a> · <a href="README.md">🇬🇧 English</a> · <a href="README.de.md">🇩🇪 Deutsch</a> · <a href="README.fr.md">🇫🇷 Français</a> · <a href="README.it.md">🇮🇹 Italiano</a> · <strong>🇵🇹 Português</strong></p>

> **Este repositório publica apenas releases binários oficiais** — o código-fonte é privado. Downloads assinados, checksums e feeds de atualização automática.

## Transferir

| | |
|---|---|
| 📥 **Instalador (recomendado)** | [IT-Community-Sync-Agent-Setup.exe](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest) — instala agente, serviço e watchdog |
| 🗜️ **Zip portátil** | `SyncAgent-<versão>.zip` em cada release — também usado pelas atualizações remotas |
| 🌍 **Site do produto** | [it-community.online](https://it-community.online) · Painel: mapeo.it-systems.es |

## O que é

Um agente para **Windows Server** que sincroniza bases **SQL Server** locais (ERP IESA / Gesfincas e semelhantes) com portais **MySQL** na cloud — de forma segura e **sem abrir uma única porta de entrada** no servidor do cliente.

```
SQL Server local
      │  (só leitura · escrita opcional controlada)
      ▼
IT-Community Sync Agent   ← serviço Windows headless (SYSTEM)
      │  WebSocket seguro (WSS · TLS verificado · token)
      ▼
Relay sync-point.es       ← autenticado (X-Relay-Key)
      │
      ▼
Portal web / Mapeo        → destino MySQL · painel de controlo
```

## Funcionalidades

- **Zero portas de entrada** — o agente só abre ligações de saída; a firewall do cliente não é tocada.
- **Incremental real** — Change Tracking / rowversion, checkpoints delta por tabela; o que não mudou não é recopiado.
- **Verdadeiramente headless** — corre como Scheduled Task sob SYSTEM, sem sessão de utilizador nem RDP aberto; watchdog auto-reiniciador incluído.
- **Gerido a partir da cloud** — painel em mapeo.it-systems.es com estado em direto, configuração remota, visualizador de logs e escrita on/off.
- **Auto-atualização assinada** — download verificado por SHA-256 com rollback automático se a nova versão não arrancar.
- **Monitorização** — badges online/offline e alertas por email antes das sincronizações programadas.

## Como usar

1. Descarregue `IT-Community-Sync-Agent-Setup-<versão>.exe` da última release.
2. Execute-o **como administrador** — instala o agente, cria a Scheduled Task (SYSTEM) e o watchdog automaticamente.
3. Depois abra `agent.exe` uma vez para registar as credenciais.
4. Alternativa manual: descomprima o zip em `C:\Sincronizador\agent`, execute `agent.exe` para as credenciais e depois `instalar_servicio.bat` como administrador.
5. No painel Mapeo supervisione o estado, edite a configuração e ligue/desligue a escrita remota.

## Requisitos

Windows Server (ou Windows 10/11) · Acesso à instância SQL Server de origem · Apenas conectividade de saída HTTPS/WSS — nenhuma porta de entrada.

## O que contém este repositório

- `IT-Community-Sync-Agent-Setup-<versão>.exe` — instalador completo (agente + serviço + watchdog)
- `SyncAgent-<versão>.zip` — pacote portátil, também usado para atualizações remotas do painel
- `SyncAgent-<versão>.sha256` — checksum para verificação

[Versão mais recente](https://github.com/mavksoft/it-community-sync-agent-releases/releases/latest)

## Perguntas frequentes

**É preciso abrir portas ou fazer NAT na firewall do cliente?**  
Não. O agente só estabelece ligações de saída WSS/TLS para o relay — funciona atrás de qualquer firewall empresarial padrão.

**O que acontece se o servidor reiniciar ou o agente morrer?**  
A Scheduled Task arranca-o com o sistema e o watchdog relança-o se cair; o painel marca o agente offline se deixar de responder.

**Pode escrever de volta no ERP?**  
A escrita é opcional e controlada — liga-se/desliga-se no painel Mapeo.

## Suporte

- Produto: [it-community.online](https://it-community.online)
- Painel de gestão: mapeo.it-systems.es

---
<p align="center"><sub>IT-Community Sync Agent · © MavkSoft / IT-Systems</sub></p>
