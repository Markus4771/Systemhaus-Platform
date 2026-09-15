# Systeme und Zuständigkeiten

## Aktueller IST-Stand

Die folgende Übersicht trennt bewusst zwischen bereits eingesetzten Systemen, Testumgebungen, Systemen im frühen Ausbau und zukünftigen/geplanten Bausteinen.

| System | Status | Aktuelle Rolle |
|---|---|---|
| Odoo | produktiv + separate Testumgebung | ERP/CRM, Kunden, Waren und kaufmännische Prozesse |
| Bestellautomation | produktiv, Eigenentwicklung/Integration | trägt Bestellungen automatisiert als Waren in Odoo ein |
| Zammad | produktiv + separate Testumgebung | Tickets, Support, Kundenkommunikation |
| Passbolt | produktiv | Passwörter und Secrets |
| Nextcloud | produktiv | Dateien/Cloud; derzeit noch ohne systematischen Kundenbezug |
| Wiki | produktiv | interne Wissensbasis und Dokumentation |
| 3CX | produktiv | Telefonanlage / VoIP |
| Stempeluhr | produktiv, Eigenentwicklung | Arbeitszeiterfassung / Anwesenheitszeit |
| ContactSync | Eigenentwicklung, Entwicklungsstand 3.2.09 | spezialisierter zentraler Dienst zur Kontaktsynchronisation; Anbindungen für Nextcloud/CardDAV, Zammad, Odoo und 3CX |
| NetLock RMM | produktiv, früher Ausbau | Endpoint Management, Remote Support, Geräte- und Patchinformationen |
| Keycloak | produktiv | zentrale Identität / SSO; bereits an die Domäne gekoppelt |
| Homarr | produktiv | zentrale Startseite / Portal für interne Dienste |
| Home Assistant | produktiv | Gebäude-, Energie- und IoT-Automation; mit Homarr im Einsatz |
| Frigate | produktiv | Video-/Kameraüberwachung und Ereigniserkennung; mit Home Assistant verbunden |
| Rocket.Chat | produktiv | interne Kommunikation und später möglicher Benachrichtigungskanal für Automatisierungen |
| n8n | in Gebrauch | Workflow-Orchestrierung und Integrationen |
| GLPI | Testinstallation | zukünftige CMDB-/Asset-Hoheit |
| Paperless-ngx | Testinstallation | zukünftiges Dokumentenmanagement |
| Gitea | vorhanden | interne Git-/Entwicklungsplattform |
| Techniker-Außendienst-App | Eigenentwicklung, in Entwicklung | Unterstützung von Technikereinsätzen beim Kunden |
| Checkmk | noch nicht installiert | zukünftiges Server-, Netzwerk- und Service-Monitoring |
| Node-RED | noch nicht installiert | zukünftige technische Event-/IoT-Automatisierung |

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
| ContactSync | verbindlicher zentraler Dienst für die Kontaktsynchronisation zwischen Odoo, Nextcloud, Zammad, 3CX und später weiteren Systemen |
| NetLock RMM | Endpoint Management, Remote Support, Patchmanagement und technische Gerätedaten |
| Keycloak | zentrale Anmeldung, SSO und MFA; Fachrechte verbleiben in den Zielsystemen |
| Homarr | Mitarbeiter-Startseite / Application Launcher, nicht Ersatz für das spätere Control Center |
| Home Assistant | interne Gebäude-/IoT-Schicht; technische Ereignisse können später über Node-RED/n8n weiterverarbeitet werden |
| Frigate | Kamera- und Ereignisschicht für Home Assistant |
| Rocket.Chat | interner Kommunikationskanal; später Ziel für Benachrichtigungen, Freigaben und Systemmeldungen |
| Bestellautomation | bestehender Integrationsbaustein; nicht neu bauen, sondern sauber in die Gesamtarchitektur einbinden |
| Gitea | interne Quellcode- und Entwicklungsplattform; GitHub bleibt für ausgewählte öffentliche Projekte, Releases und übergreifende Dokumentation nutzbar |

## Kontaktsynchronisation mit ContactSync

ContactSync ist die spezialisierte Synchronisationsschicht für Kontakte. Kontaktabgleich, Feldzuordnung, Dublettenbehandlung, Synchronisationsrichtung und Änderungsweitergabe werden dort gebündelt und nicht als verstreute n8n-Einzelflows neu aufgebaut.

### Aktueller Entwicklungsstand ContactSync

Der zuletzt erreichte Entwicklungsstand ist **3.2.09**. ContactSync ist als eigenständige Anwendung aufgebaut und soll im Systemhaus-Konzept dauerhaft die spezialisierte Kontakt-Synchronisation übernehmen.

Aktuell bzw. im bisherigen Projektstand vorgesehen sind:

- Nextcloud über CardDAV
- Zammad
- Odoo
- 3CX
- konfigurierbare Synchronisationsrichtungen im Menü „Synchronisation“
- Konflikt- und Dublettenbehandlung
- Audit-/Protokollierung der Synchronisationsvorgänge
- Backup-/Update-Bereich
- SMB-Backup
- CSV-Export der Kontakte
- Benutzerverwaltung
- Hilfe-Funktion
- zentrale Kontaktfelder einschließlich E-Mail-Adresse
- Kundennummer als wichtiges Zuordnungsfeld

Die Kundennummer ist für die Systemhaus-Plattform besonders wichtig: Es wird keine zusätzliche künstliche `K-...`-Kennung eingeführt. Die vorhandene geschäftliche Odoo-Kundennummer dient als zentrale Customer-ID und soll von ContactSync zur systemübergreifenden Zuordnung mitgeführt werden.

### Geplante Weiterentwicklung im Systemhaus-Konzept

ContactSync soll modular weitergeführt werden. Die bestehenden Odoo-, Zammad-, 3CX- und Nextcloud-Anbindungen werden als spezialisierte Connectoren betrachtet. Weitere Connectoren können später ergänzt werden, insbesondere:

- GLPI
- Systemhaus Control Center
- Techniker-Außendienst-App
- weitere freigegebene Kommunikations- oder CRM-/Service-Systeme

Damit bleibt ContactSync ein eigener Integrationsbaustein und wird nicht durch n8n ersetzt. n8n kann ContactSync jedoch über definierte API-/Webhook-Schnittstellen in übergeordnete Geschäftsprozesse einbinden.

### Führende Quelle

Für geschäftliche Kunden- und Ansprechpartnerdaten bleibt **Odoo das führende System**. Die bestehende Odoo-Kundennummer wird als zentrale Customer-ID verwendet.

```text
                   Odoo
      führende Kunden und Ansprechpartner
                    |
                    v
               ContactSync
                    |
       +------------+------------+
       |            |            |
       v            v            v
   Nextcloud      Zammad        3CX
    Kontakte      Kontakte    Telefonbuch
       |
       v
Smartphone / Thunderbird

später zusätzlich:
GLPI / Außendienst-App / Control Center / weitere freigegebene Systeme
```

### Grundregeln

- Odoo ist für geschäftliche Kundenstammdaten und zentrale Ansprechpartner führend.
- ContactSync verteilt freigegebene Kontaktfelder an die Zielsysteme.
- Kundennummer und E-Mail-Adresse gehören zu den zentralen Zuordnungs-/Kontaktfeldern.
- Lokale System-IDs werden auf die zentrale Odoo-Kundennummer bzw. eindeutige Kontaktkennungen abgebildet.
- Änderungen dürfen nur gemäß definierter Feldhoheit zurückgeschrieben werden.
- Firmenname, Kundennummer und zentrale Geschäftsdaten dürfen nicht unkontrolliert aus Zielsystemen nach Odoo überschrieben werden.
- Dubletten und Konflikte werden in ContactSync behandelt.
- Synchronisation soll protokolliert und nachvollziehbar sein.
- n8n bleibt für Geschäftsprozesse zuständig und ersetzt ContactSync nicht.

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
| OpenHands | zukünftiger interner Entwicklungsagent für Codeanalyse, Änderungen, Tests, Dokumentation und Git-Workflows |
| OpenClaw | zukünftiges Agent-/Mitarbeiter-Gateway für kontrollierten Zugriff auf Werkzeuge und Prozesse |
| MCP-Server | zukünftige standardisierte Werkzeug- und Kontextschicht für KI-Agenten |

## Zukünftige KI- und MCP-Architektur

OpenHands, OpenClaw und ein eigener MCP-Server sind Zukunftsbausteine und werden nicht für den ersten Integrations-PoC benötigt.

Der MCP-Server soll eine kontrollierte, standardisierte Werkzeugschicht zwischen KI-Agenten und den Fachsystemen bilden. Er ersetzt weder n8n noch Node-RED.

```text
OpenHands / OpenClaw / weitere KI-Agenten
                  |
                  v
              MCP-Server
                  |
      +-----------+-----------+
      |           |           |
     Odoo       Zammad       GLPI
      |           |           |
  Nextcloud      Wiki      NetLock/Checkmk
      |
   weitere freigegebene Systeme

                  |
                  v
                 n8n
       Workflows / Freigaben / Aktionen
```

### Klare Aufgabenteilung

- **MCP-Server:** Werkzeuge und kontrollierter Kontext für KI-Agenten.
- **n8n:** Geschäftsprozesse, systemübergreifende Orchestrierung, Freigaben und Aktionen.
- **ContactSync:** spezialisierte Kontakt-Synchronisation und Konfliktbehandlung.
- **Node-RED:** technische Ereignisse, IoT, Home Assistant, MQTT, Sensorik und schnelle Event-Flows.
- **Keycloak:** Identität, Anmeldung, SSO und MFA.
- **Passbolt:** Secrets und Passwörter; keine allgemeine KI-/RAG-Datenquelle.
- **OpenHands:** Entwicklungsagent für eigene Software und Git-Workflows.
- **OpenClaw:** Agenten-/Mitarbeiterzugang zu freigegebenen Werkzeugen und Prozessen.

### Sicherheitsprinzip

KI-Agenten erhalten keinen pauschalen Vollzugriff auf Produktivsysteme. Lesende Werkzeuge werden nach Rolle und Zweck begrenzt. Kritische oder schreibende Aktionen sollen über definierte APIs, n8n-Workflows und bei Bedarf menschliche Freigaben laufen. Passbolt-Inhalte werden nicht in allgemeine RAG-Indizes oder KI-Kontexte übernommen.

### Mögliche MCP-Werkzeuge

Beispiele für spätere, klar begrenzte Werkzeuge:

- `get_customer(customer_number)`
- `get_open_tickets(customer_number)`
- `get_customer_devices(customer_number)`
- `get_monitoring_status(customer_number)`
- `search_wiki(query)`
- `get_order_status(order_number)`
- `get_service_history(customer_number)`
- `create_service_report(...)` über einen kontrollierten Workflow

Die bestehende Odoo-Kundennummer wird auch in dieser Schicht als zentrale Customer-ID verwendet. Der MCP-Server soll vorhandene APIs und Integrationsdienste wiederverwenden, damit keine parallele zweite Integrationslandschaft entsteht.

## Eigene Anwendungen

### Systemhaus Control Center
Zentrales Techniker-Cockpit für Kundenkontext, Tickets, Geräte, Monitoring, RMM, Dokumente, Verträge, Zeiten und Schnellaktionen. Modularer Plugin-Ansatz.

### Asset & Onboarding Gateway
Eigene GLPI-nahe Anwendung zur Erfassung und Inbetriebnahme von Geräten. Geplante Felder/Funktionen umfassen Kunde/Tenant, Standort, MAC-Adresse, Wake-on-LAN, TeamViewer/RustDesk, NetLock RMM, Virenschutz, Techniker, Offline-Erfassung und spätere Synchronisierung.

### Techniker-Außendienst-App
Bereits begonnene Eigenentwicklung für Außeneinsätze von Technikern. Die bestehende Codebasis soll vor einer Neuplanung analysiert werden. Langfristig sind Integrationen mit Zammad, Odoo, GLPI, Stempeluhr sowie Dokumenten-/Dateisystemen sinnvoll.

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

3CX ist bereits produktiv im Einsatz und wird als Telefonieplattform beibehalten. Ziel der Integration sind Anruferkennung, Kundenkontext, Click-to-Call, Rückrufaufgaben, Verknüpfung zu Zammad/Odoo und optional Voicemail-Transkription. Die Bereitstellung konsistenter Kontaktdaten für 3CX erfolgt über ContactSync.

## Gebäude-, IoT- und Kameraebene

Home Assistant, Homarr und Frigate sind bereits produktiv miteinander im Einsatz. Diese Ebene bleibt fachlich von Kunden-, Ticket- und ERP-Daten getrennt. Technische Ereignisse wie definierte Alarme, Statuswechsel oder Sensorwerte können später über Node-RED bzw. n8n kontrolliert an Benachrichtigungs- oder Supportprozesse übergeben werden.

## Nächster praktischer Schritt

Die Zukunftsbausteine MCP, OpenHands, OpenClaw, Checkmk und Node-RED werden zunächst nicht installiert. Für den ersten Integrations-PoC werden die vorhandenen Testsysteme genutzt:

**Odoo Test -> n8n -> Zammad Test + GLPI Test**

Die Kontakt-Synchronisation wird dabei nicht neu in n8n gebaut. Für Kontakte wird ContactSync verwendet. n8n bleibt für organisatorische und fachliche Workflows zuständig.

Dabei wird mit künstlichen Testdaten und einer Test-Kundennummer gearbeitet. Erst wenn dieser Datenfluss stabil funktioniert, werden weitere Systeme schrittweise angebunden.