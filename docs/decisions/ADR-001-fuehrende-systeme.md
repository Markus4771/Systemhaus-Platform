# ADR-001: Führende Systeme statt Mehrfach-Master

## Status
Akzeptiert

## Kontext
Mehrere Systeme enthalten ähnliche Daten. Ohne klare Datenhoheit entstehen Konflikte und Doppelpflege.

## Entscheidung
Für jede Datenart wird genau ein führendes System definiert. Zielsysteme erhalten nur benötigte Kopien/Referenzen.

Aktuelle Zuordnung:
- Odoo: kaufmännischer Kundenstamm, CRM, Verträge, Projekte, Abrechnung
- GLPI: Assets/CMDB
- Zammad: Tickets/SLA/Supportkommunikation
- Keycloak: Identität/SSO
- Passbolt: Secrets
- Checkmk: Monitoringzustand
- NetLock RMM: Endpoint-/RMM-Zustand
- Stempeluhr: Anwesenheitszeit

## Konsequenzen
Synchronisationsregeln müssen Richtung, Feldhoheit, Fehlerfälle und Löschverhalten explizit definieren. Das Control Center wird kein neuer Master.