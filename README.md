# Systemhaus-Platform

Zentrale Architektur-, Integrations- und Planungsdokumentation für eine weitgehend selbst gehostete, modular aufgebaute Systemhaus-Plattform.

## Ziel

Die Plattform soll vorhandene Fachsysteme über APIs, n8n und einen kleinen Integration Core verbinden, ohne unnötig Daten doppelt zu pflegen. Für jede Datenart wird ein führendes System definiert. Mitarbeiter arbeiten perspektivisch über ein zentrales Control Center und Homarr als Startportal.

## Bereits vorhandene Systeme in der Testumgebung

- Odoo
- Zammad
- GLPI
- n8n
- Paperless-ngx
- Homarr
- Home Assistant

Weitere geplante bzw. bereits an anderer Stelle vorhandene Komponenten: Keycloak, Nextcloud, NetLock RMM, Checkmk, Passbolt, ContactSync, Stempeluhr, OpenHands, OpenClaw, Proxmox Backup Server und weitere Module.

## Leitprinzipien

- Open Source und Self-Hosting bevorzugen
- Proxmox als Virtualisierungsbasis
- LXC und VMs je nach Anforderung mischen
- n8n als zentrale Workflow-Orchestrierung, aber nicht als alleinige Integrationsschicht oder Datenbank
- APIs/Webhooks statt direkter Datenbankzugriffe
- eindeutige zentrale Kunden-ID über alle Systeme
- Keycloak für SSO/MFA
- keine Secrets in KI/RAG oder im Control Center duplizieren
- produktive Änderungen und KI-Aktionen nur kontrolliert und nachvollziehbar
- modulare Plugin-Architektur für Eigenentwicklungen

## Dokumentation

Siehe `docs/` für Architektur, Systeme, Datenhoheit, Workflows, Proxmox-Testplan, Control Center, KI, Security, CI/CD, Corporate Identity, Roadmap und Backlog.

## Erster Proof of Concept

1. Bestehende Installationen unverändert lassen.
2. Odoo, Zammad und GLPI per API mit n8n verbinden.
3. Zentrale Kunden-ID definieren, z. B. `K-000001`.
4. Testkunde in Odoo anlegen.
5. Automatisch Zammad-Organisation und GLPI-Entity erzeugen.
6. Änderungen aus Odoo in die Zielsysteme synchronisieren.
7. Danach Paperless, Nextcloud, NetLock und Checkmk ergänzen.

## Status

Projektstart / Architektur- und PoC-Phase.