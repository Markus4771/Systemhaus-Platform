# Proxmox-Testumgebung

## Ziel

Die ersten Integrationsschritte werden auf dem vorhandenen Proxmox-Testserver durchgeführt. Bestehende Installationen bleiben zunächst unverändert.

## Bereits vorhanden

- Odoo
- Zammad
- GLPI
- n8n
- Paperless-ngx
- Homarr
- Home Assistant

Einige Dienste laufen als LXC-Container. Das ist für den PoC kein Problem, solange die Dienste sauber über Netzwerk/APIs erreichbar sind.

## LXC vs. VM

Geeignet für LXC:
- GLPI
- n8n bei nativer Installation
- kleinere eigene Dienste
- Control Center
- ContactSync
- Stempeluhr
- viele klassische Webanwendungen

Eher VM bevorzugen:
- Docker-Hosts mit mehreren komplexen Stacks
- OpenHands
- OpenClaw
- Wazuh
- besonders kritische oder stark isolierte Komponenten

Docker in LXC ist technisch möglich, kann aber bei AppArmor, Mounts, Nested Features und Berechtigungen zusätzliche Komplexität verursachen. Für produktive Docker-Stacks ist eine kleine Debian-VM oft einfacher.

## PoC-Reihenfolge

1. Netzwerk- und API-Erreichbarkeit prüfen.
2. Odoo API testen.
3. Zammad API testen.
4. GLPI API testen.
5. n8n Credentials getrennt einrichten.
6. zentrale Kunden-ID definieren.
7. PoC `Odoo -> n8n -> Zammad + GLPI` bauen.
8. Update-Synchronisation testen.
9. Fehlerfälle, Retry und Duplikate testen.
10. Paperless anbinden.
11. danach Nextcloud, NetLock und Checkmk ergänzen.

## Produktivplanung

Vor Hardwarekauf soll der vorhandene Fujitsu PRIMERGY TX2550 inventarisiert werden: Generation, CPU-Modelle, RAM, RAID/HBA, Datenträger, NICs und freier Storage. Danach wird ein finaler VM/LXC-/Storage-Plan erstellt.

Die späteren LLM-Modelle laufen nicht auf dem Business-Proxmox, sondern auf separater KI-Hardware oder extern.