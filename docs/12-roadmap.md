# Roadmap

## Phase 1 – Bestehende Testumgebung erfassen
- vorhandene Proxmox-VMs/LXCs dokumentieren
- IPs, DNS-Namen und Ports erfassen
- Versionen von Odoo, Zammad, GLPI, n8n, Paperless, Homarr und Home Assistant dokumentieren
- Backup-Status prüfen
- keine unnötigen Neuinstallationen

## Phase 2 – Kernsysteme per API verbinden
- Odoo API
- Zammad API
- GLPI API
- n8n Credentials und Testflows

## Phase 3 – Zentrale Kunden-ID
- Format festlegen
- Erzeugung definieren
- Felder in Odoo, Zammad und GLPI vorbereiten
- Mapping externer IDs dokumentieren

## Phase 4 – Erster End-to-End-PoC
`Odoo -> n8n -> Zammad + GLPI`

Erfolgskriterien:
- neuer Kunde wird korrekt repliziert
- Updates sind idempotent
- keine Duplikate
- Fehler werden sichtbar
- Logs enthalten keine Secrets

## Phase 5 – Dokumente und Zusammenarbeit
- Paperless
- Nextcloud
- Kundenordner
- Kalender/Kontakte
- ContactSync

## Phase 6 – Technikbetrieb
- NetLock RMM
- Checkmk
- Alert-to-Ticket
- Backup-Monitoring
- Domain/SSL-Monitoring

## Phase 7 – Eigene Fachanwendungen
- Asset & Onboarding Gateway
- Stempeluhr
- Systemhaus Control Center
- Plugin-Schnittstellen

## Phase 8 – Vertrieb und Controlling
- Sales Intelligence
- Lead Intelligence
- Vertrags-/Lizenzabweichungen
- Budget/Controlling
- Personal-/Kapazitätsplanung

## Phase 9 – Identity und UX-Ausbau
- Keycloak SSO/MFA vollständig integrieren
- Homarr als Startportal
- Corporate Identity / Design System
- rollenabhängige Navigation

## Phase 10 – KI und Wissen
- Unternehmenshandbuch/Wiki
- RAG
- AI Gateway
- OpenClaw
- OpenHands-Integration

## Phase 11 – weitere Integration
- DATEV
- VoIP/CTI
- Bestellsynchronisation
- Kundenportal
- Wazuh/SIEM
- Reporting/BI

## Grundsatz

Jede Phase soll erst erweitert werden, wenn der vorherige Kernfluss stabil, dokumentiert und testbar ist.