# Systeme und Zuständigkeiten

## Aktueller IST-Stand

Die folgende Übersicht trennt bewusst zwischen bereits eingesetzten Systemen, Systemen im frühen Ausbau und zukünftigen/geplanten Bausteinen.

| System | Status | Aktuelle Rolle |
|---|---|---|
| Odoo | produktiv | ERP/CRM, Kunden, Waren und kaufmännische Prozesse |
| Bestellautomation | produktiv, Eigenentwicklung/Integration | trägt Bestellungen automatisiert als Waren in Odoo ein |
| Zammad | produktiv | Tickets, Support, Kundenkommunikation |
| Passbolt | produktiv | Passwörter und Secrets |
| Nextcloud | produktiv | Dateien/Cloud; derzeit noch ohne systematischen Kundenbezug |
| Wiki | produktiv | interne Wissensbasis und Dokumentation |
| 3CX | produktiv | Telefonanlage / VoIP |
| Stempeluhr | produktiv, Eigenentwicklung | Arbeitszeiterfassung / Anwesenheitszeit |
| NetLock RMM | produktiv, früher Ausbau | Endpoint Management, Remote Support, Geräte- und Patchinformationen |
| Keycloak | produktiv | zentrale Identität / SSO; bereits an die Domäne gekoppelt |
| Homarr | produktiv | zentrale Startseite / Portal für interne Dienste |
| Home Assistant | produktiv | Gebäude-, Energie- und IoT-Automation; bereits mit Homarr im Einsatz |
| Frigate | produktiv | Video-/Kameraüberwachung und Ereigniserkennung; mit Home Assistant verbunden |
| n8n | Test-/Integrationsplattform | zentrale Workflow-Orchestrierung für zukünftige Systemverknüpfungen |
| GLPI | Test-/Ausbauphase | zukünftige CMDB-/Asset-Hoheit |
| Paperless-ngx | Test-/Ausbauphase | zukünftiges Dokumentenmanagement |

## Zielrollen der bestehenden Systeme

| System | Zielrolle |
|---|---|
| Odoo | führendes kaufmännisches System für Kunden, Angebote, Aufträge, Verträge und Abrechnung |
| Zammad | führendes Ticketsystem für Support, SLA und Kundenkommunikation |
| Passbolt | alleiniger Tresor für Passwörter und technische Secrets |
| Nextcloud | Dateien, Zusammenarbeit, Kalender/Kontakte und ausgewählte kundenbezogene Strukturen |
| Wiki | freigegebene Wissensbasis; später mögliche Quelle für RAG/KI |
| 3CX | zentrale Telefonie mit späterer CTI-/Kunden-/Ticketintegration |
| Stempeluhr | führendes System für Anwesenheits-/Arbeitszeit; getrennt von abrechenbarer Servicezeit |
| NetLock RMM | Endpoint Management, Remote Support, Patchmanagement und technische Gerätedaten |
| Keycloak | zentrale Anmeldung, SSO und MFA; Fachrechte verbleiben in den Zielsystemen |
| Homarr | Mitarbeiter-Startseite / Application Launcher, nicht Ersatz für das spätere Control Center |
| Home Assistant | interne Gebäude-/IoT-Schicht; technische Ereignisse können später über Node-RED/n8n weiterverarbeitet werden |
| Frigate | Kamera- und Ereignisschicht für Home Assistant; relevante Ereignisse können später über Home Assistant/Node-RED/n8n in Benachrichtigungen oder definierte Workflows einfließen |
| Bestellautomation | bestehender Integrationsbaustein; nicht neu bauen, sondern sauber in die Gesamtarchitektur einbinden |

## Geplante/ergänzende Systeme

| System | Rolle |
|---|---|
| GLPI | CMDB, Assets, Geräte, Standorte, Software, Lizenzen und Verträge |
| n8n | zentrale Workflow-Orchestrierung und Geschäftsprozess-Automatisierung |
| Node-RED | technische Event-/IoT-Automatisierung, besonders Home Assistant, MQTT, Sensorik und Geräteintegration |
| Paperless-ngx | Dokumentenmanagement, Rechnungen, Lieferscheine und Verträge |
| Checkmk | Server-, Netzwerk- und Service-Monitoring |
| Proxmox Backup Server | zentrale Backups und Restore-Tests |
| Wazuh | spätere SIEM-/Security-Schicht |
| ContactSync | spezialisierte Kontakt-Synchronisation zwischen Odoo, Nextcloud, Zammad, 3CX u. a. |
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

3CX ist bereits produktiv im Einsatz und wird als Telefonieplattform beibehalten. Ziel der Integration sind Anruferkennung, Kundenkontext, Click-to-Call, Rückrufaufgaben, Verknüpfung zu Zammad/Odoo und optional Voicemail-Transkription.

## Gebäude-, IoT- und Kameraebene

Home Assistant, Homarr und Frigate sind bereits produktiv miteinander im Einsatz. Diese Ebene bleibt fachlich von Kunden-, Ticket- und ERP-Daten getrennt. Technische Ereignisse wie definierte Alarme, Statuswechsel oder Sensorwerte können später über Node-RED bzw. n8n kontrolliert an Benachrichtigungs- oder Supportprozesse übergeben werden.