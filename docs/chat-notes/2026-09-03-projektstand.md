# Projektstand aus der Planung – 2026-09-03

Diese Datei ist eine strukturierte Zusammenfassung der bisherigen Planung und ersetzt keinen wortwörtlichen Chat-Export.

## Ausgangslage

Für ein Systemhaus mit ungefähr 15 Mitarbeitern soll eine weitgehend selbst gehostete, modular aufgebaute Plattform auf Proxmox entstehen. Vorhandene Open-Source-Systeme sollen nicht ersetzt, sondern über APIs, n8n und eine Integrationsschicht verbunden werden.

## Bereits vorhandene Testsysteme

Auf einem Proxmox-Testserver sind bereits Odoo, Zammad, GLPI, n8n, Paperless-ngx, Homarr und Home Assistant vorhanden. Einige Installationen laufen in LXC-Containern; das wird für den PoC bewusst beibehalten.

## Beschlossene Kernidee

Erster technischer End-to-End-Test:

`Odoo -> n8n -> Zammad + GLPI`

Ein Testkunde wird in Odoo angelegt und erhält eine zentrale Kunden-ID wie `K-000001`. n8n erzeugt bzw. aktualisiert daraus eine Zammad-Organisation und eine GLPI-Entity. Danach folgen Paperless, Nextcloud, NetLock RMM und Checkmk.

## Wesentliche Architekturentscheidungen

- Odoo ist kaufmännischer Kunden-/CRM-Master.
- GLPI ist Asset-/CMDB-Master.
- Zammad ist Ticket-/Support-Master.
- Keycloak ist für Identität, SSO und MFA vorgesehen.
- Passbolt bleibt alleinige Secret-Quelle.
- n8n orchestriert die Mehrzahl der systemübergreifenden Workflows.
- Ein kleiner Integration Core/API Gateway wird für IDs, Mapping, Retry, Logging, Queueing und Fehlerbehandlung vorgesehen.
- Das Systemhaus Control Center ist eine Aggregations- und Aktionsoberfläche, kein zusätzlicher Datenmaster.
- Homarr bleibt die zentrale Mitarbeiter-Startseite.
- Home Assistant wird für interne Gebäude-/IoT-Automation genutzt und kann Betriebsalarme an n8n/Zammad liefern.
- ContactSync bleibt spezialisierte Kontakt-Synchronisation.
- Die eigene Stempeluhr bleibt Master für Anwesenheitszeit.
- OpenHands und OpenClaw können auf dem Business-Proxmox laufen; LLM-Modelle selbst laufen getrennt auf KI-Hardware oder extern.

## Infrastrukturgedanke

Zunächst wird die vorhandene Testumgebung genutzt. Vor Beschaffung eines neuen Produktivservers soll vorhandene Fujitsu-PRIMERGY-Hardware vollständig inventarisiert werden. Proxmox Backup Server soll getrennt betrieben und Restore-Tests sollen automatisiert dokumentiert werden.

## Noch geplante Ausbaustufen

- Nextcloud / CalDAV / CardDAV
- NetLock RMM
- Checkmk
- Passbolt
- VoIP/CTI, wahrscheinlich mit 3CX als naheliegendem Kandidaten
- DATEV-Anbindung
- Bestell-/Lieferanten-Synchronisation
- Asset & Onboarding Gateway
- Systemhaus Control Center
- Sales Intelligence
- Lead Intelligence
- Budget/Controlling
- Personal-/Kapazitätsplanung
- Kundenportal
- Wiki/QM/Unternehmenshandbuch
- RAG/Wissens-KI
- OpenHands/OpenClaw/AI Gateway
- Wazuh/SIEM
- zentrale Backup-/Domain-/SSL-/Lizenzüberwachung

## Entwicklungsprinzip

Eigenentwicklungen sollen durchgängig über Git, automatisierte Tests, Build, Testumgebung, Review und kontrolliertes Deployment entwickelt werden. Zusätzlich soll eine gemeinsame Corporate Identity für Homarr, Keycloak und Eigenentwicklungen entstehen.

## Nächster Schritt

Nicht weitere Systeme installieren, sondern die vorhandenen APIs testen und den ersten Kunden-Synchronisationsworkflow in n8n umsetzen.