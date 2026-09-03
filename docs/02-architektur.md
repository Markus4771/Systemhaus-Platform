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
                n8n
                 |
   +-------------+--------------+
   |             |              |
Paperless    Nextcloud       Passbolt
   |             |              |
   +-------------+--------------+
                 |
         weitere Fachsysteme
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
- Odoo: ERP/CRM/Vertrieb/Projekte/Abrechnung
- Zammad: Helpdesk/Tickets/SLA
- GLPI: CMDB/Assets
- Paperless-ngx: DMS/Dokumente
- Nextcloud: Dateien/Kalender/Kontakte/Zusammenarbeit
- Passbolt: Secrets
- NetLock RMM: Endpoint Management
- Checkmk: Monitoring
- Home Assistant: Gebäude-/IoT-Automation

### 4. Integration
- n8n als Workflow-Orchestrierung
- kleiner Integration Core/API Gateway für IDs, Mapping, Queueing, Retry, Logging, Fehlerbehandlung und Normalisierung
- APIs, Webhooks und Events statt direkter Datenbankkopplung

### 5. Benutzeroberflächen
- Homarr als Startportal
- eigenes Systemhaus Control Center als Techniker-Cockpit
- eigenes GLPI Asset & Onboarding Gateway
- eigene Stempeluhr
- später Kundenportal

### 6. KI
- OpenHands für Entwicklung
- OpenClaw als Agent-/Mitarbeiter-Gateway
- RAG/Wissens-KI
- AI Gateway für Modellrouting, Policies und Datenklassen
- eigentliche LLMs auf separatem KI-Server oder externem Provider

## Architekturregel

Das Control Center ist keine zusätzliche Master-Datenbank. Es aggregiert Informationen aus den führenden Fachsystemen und löst Aktionen über kontrollierte APIs/Workflows aus.