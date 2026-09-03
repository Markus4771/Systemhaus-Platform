# Systeme und Zuständigkeiten

## Kernsysteme

| System | Rolle |
|---|---|
| Odoo | ERP/CRM, Kunden, Angebote, Aufträge, Verträge, Projekte, Abrechnung |
| Zammad | Tickets, SLA, Kundenkommunikation, Supporthistorie |
| GLPI | CMDB, Assets, Geräte, Standorte, Software, Lizenzen, Verträge |
| n8n | Workflow-Orchestrierung und Automatisierung |
| Paperless-ngx | Dokumentenmanagement, Rechnungen, Lieferscheine, Verträge |
| Homarr | zentrale Mitarbeiter-Startseite / Portal |
| Home Assistant | interne Gebäude-, Energie- und IoT-Automation |

## Geplante/ergänzende Systeme

| System | Rolle |
|---|---|
| Keycloak | SSO, MFA, zentrale Identität |
| Nextcloud | Dateien, Kundenordner, Kalender, Kontakte, Zusammenarbeit |
| Passbolt | Passwörter und Secrets |
| NetLock RMM | Endpoint Management, Remote Support, Patching, Alarme |
| Checkmk | Server-, Netzwerk- und Service-Monitoring |
| Proxmox Backup Server | zentrale Backups und Restore-Tests |
| Wazuh | spätere SIEM-/Security-Schicht |
| ContactSync | spezialisierte Kontakt-Synchronisation zwischen Odoo, Nextcloud, Zammad, 3CX u. a. |
| Stempeluhr | Anwesenheitszeit, Urlaub, Teilzeit-/Wochenarbeitstage |
| OpenHands | interner Entwicklungsagent |
| OpenClaw | Agent-/Mitarbeiter-Gateway |

## Eigene Anwendungen

### Systemhaus Control Center
Zentrales Techniker-Cockpit für Kundenkontext, Tickets, Geräte, Monitoring, RMM, Dokumente, Verträge, Zeiten und Schnellaktionen. Modularer Plugin-Ansatz.

### Asset & Onboarding Gateway
Eigene GLPI-nahe Anwendung zur Erfassung und Inbetriebnahme von Geräten. Geplante Felder/Funktionen umfassen Kunde/Tenant, Standort, MAC-Adresse, Wake-on-LAN, TeamViewer/RustDesk, NetLock RMM, Virenschutz, Techniker, Offline-Erfassung und spätere Synchronisierung.

### Sales Intelligence
Analyse bestehender Kunden auf technische und kaufmännische Potenziale.

### Lead Intelligence
Unterstützung bei rechtmäßiger Neukundengewinnung und Lead-Qualifizierung; Odoo bleibt CRM-Master.

### Personal-/Kapazitätsplanung
Verknüpft Anwesenheit, Urlaub, Aufgaben, Projekte und abrechenbare Servicezeiten.

## Externe Systeme

- DATEV / DATEV Online
- Banken
- Lieferanten und Distributoren
- Microsoft 365
- öffentliche DNS-/Domain-Dienste
- externe KI-Provider bzw. separater KI-Server

## Telefonie

VoIP/CTI ist vorgesehen. 3CX ist ein naheliegender Kandidat, da bereits Integrationsarbeit vorhanden ist. Alternativen bleiben möglich. Ziel sind Anruferkennung, Kundenkontext, Click-to-Call, Rückrufaufgaben und optional Voicemail-Transkription.