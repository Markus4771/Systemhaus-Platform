# Zielarchitektur

## Überblick

```text
Benutzer / Kunden / Partner
          |
       Keycloak
     SSO / MFA
          |
        Homarr
   Mitarbeiter-Startseite
          |
          v
+-------------------------------+
| Systemhaus Control Center     |
+-------------------------------+
  |      |      |      |      |
 Odoo  Zammad  GLPI  Checkmk  NetLock
  |      |      |      |      |
  +------+------+-+----+------+
                 |
          Integration Core
                 |
       +---------+---------+
       |         |         |
      n8n    ContactSync  Node-RED
       |         |         |
       |    Kontakte       | technische Events
       |         |         |
       +---------+---------+
                 |
   +-------------+--------------+
   |             |              |
Paperless    Nextcloud       Passbolt
                 |
           CardDAV/Kontakte
                 |
          Smartphone/Thunderbird

ContactSync zusätzlich zu:
Odoo <-> ContactSync <-> Zammad / Nextcloud / 3CX
                         später GLPI / Control Center /
                         Techniker-Außendienst-App
```

## Schichten

### 1. Infrastruktur
- Proxmox VE
- Reverse Proxy
- DNS/Netzwerk
- Backup/PBS
- Monitoring
- Security/SIEM

### 2. Identität und Zugriff
- Keycloak für SSO/MFA
- Rollen und Rechte weiterhin fachlich in den Zielsystemen

### 3. Fachsysteme
- Odoo: ERP/CRM/Vertrieb/Projekte/Abrechnung und führendes System für geschäftliche Kunden-/Ansprechpartnerdaten
- Zammad: Helpdesk/Tickets/SLA
- GLPI: CMDB/Assets
- Paperless-ngx: DMS/Dokumente
- Nextcloud: Dateien/Kalender/Kontakte/Zusammenarbeit
- Passbolt: Secrets
- NetLock RMM: Endpoint Management
- Checkmk: Monitoring
- Home Assistant: Gebäude-/IoT-Automation
- 3CX: Telefonie/VoIP

### 4. Integration und Automatisierung

Die Integrationsschicht wird bewusst in mehrere spezialisierte Bausteine aufgeteilt. Es soll nicht versucht werden, sämtliche Aufgaben in n8n abzubilden.

#### Integration Core / API Gateway
Zentrale technische Integrationsschicht für IDs, Mapping, Queueing, Retry, Logging, Fehlerbehandlung und Normalisierung. APIs, Webhooks und Events werden gegenüber direkten Datenbankkopplungen bevorzugt.

#### n8n
n8n übernimmt Geschäftsprozesse und systemübergreifende Orchestrierung, beispielsweise Kundenanlage, Ticket-/Auftragsprozesse, Freigaben, Dokumentenprozesse und Benachrichtigungen.

#### ContactSync
ContactSync ist ein eigener, dauerhafter Architekturbaustein für die Kontakt-Synchronisation. Der aktuelle Entwicklungsstand ist **3.2.09**. Die bestehende Eigenentwicklung wird weiterverwendet und nicht durch n8n neu gebaut.

Aktuelle Kernanbindungen:
- Odoo
- Nextcloud / CardDAV
- Zammad
- 3CX

ContactSync übernimmt insbesondere:
- Kontaktabgleich und Feldmapping
- definierte Synchronisationsrichtungen
- Konflikt- und Dublettenbehandlung
- Änderungsweitergabe
- Audit-/Synchronisationsprotokollierung
- zentrale Zuordnung über Kundennummer und eindeutige Kontaktkennungen
- Verteilung von E-Mail-Adressen und weiteren freigegebenen Kontaktfeldern
- CSV-Export sowie vorhandene Backup-/Administrationsfunktionen

Für geschäftliche Kunden und Ansprechpartner ist Odoo die führende Quelle. Die bestehende Odoo-Kundennummer wird als zentrale Customer-ID verwendet; eine zusätzliche künstliche `K-...`-ID wird nicht eingeführt.

```text
                         Odoo
                  Kunden / Kontakte
                         |
                 zentrale Kundennummer
                         |
                         v
                    ContactSync
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
    Nextcloud          Zammad            3CX
     CardDAV          Kontakte         Telefonbuch
        |
        v
Thunderbird / Smartphone

spätere Connectoren:
GLPI / Control Center / Techniker-Außendienst-App
```

ContactSync darf von n8n über definierte APIs oder Webhooks angestoßen bzw. in größere Workflows eingebunden werden. Die eigentliche Kontaktlogik verbleibt jedoch in ContactSync. Damit gibt es eine klare Trennung: **ContactSync synchronisiert Kontakte; n8n orchestriert Geschäftsprozesse.**

#### Node-RED
Node-RED übernimmt zukünftig technische und ereignisorientierte Automatisierungen, insbesondere Home Assistant, MQTT, Sensorik, Geräte- und Infrastrukturereignisse. Node-RED ersetzt weder n8n noch ContactSync.

### 5. Benutzeroberflächen
- Homarr als Startportal
- eigenes Systemhaus Control Center als Techniker-Cockpit
- eigenes GLPI Asset & Onboarding Gateway
- eigene Stempeluhr
- ContactSync mit eigener Administrations-/Synchronisationsoberfläche
- später Kundenportal

### 6. KI
- OpenHands für Entwicklung
- OpenClaw als Agent-/Mitarbeiter-Gateway
- RAG/Wissens-KI
- AI Gateway für Modellrouting, Policies und Datenklassen
- eigentliche LLMs auf separatem KI-Server oder externem Provider

## Zuständigkeiten der Integrationsbausteine

| Baustein | Hauptaufgabe |
|---|---|
| Integration Core | APIs, IDs, Mapping, Normalisierung, Logging, Retry, technische Entkopplung |
| n8n | Geschäftsprozesse und systemübergreifende Workflow-Orchestrierung |
| ContactSync | Kontakte, Feldmapping, Synchronisationsrichtungen, Konflikte und Dubletten |
| Node-RED | technische Events, IoT, MQTT, Home Assistant und schnelle Event-Flows |
| Keycloak | Identität, SSO und MFA |

Diese Trennung verhindert parallele Synchronisationslogik. Ein Kontakt soll beispielsweise nicht gleichzeitig durch einen n8n-Kontaktflow und ContactSync verändert werden.

## Architekturregel

Das Control Center ist keine zusätzliche Master-Datenbank. Es aggregiert Informationen aus den führenden Fachsystemen und löst Aktionen über kontrollierte APIs/Workflows aus.

Ebenso ist ContactSync kein neuer Kunden-Master. ContactSync verteilt und synchronisiert Kontaktinformationen gemäß festgelegter Datenhoheit. Odoo bleibt für geschäftliche Kunden- und Ansprechpartnerdaten führend, GLPI bleibt für Assets führend und Zammad für Tickets.