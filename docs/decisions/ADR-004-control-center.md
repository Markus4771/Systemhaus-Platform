# ADR-004: Control Center als Aggregations- und Aktionsoberfläche

## Status
Akzeptiert

## Kontext
Techniker sollen nicht für jede Tätigkeit zwischen vielen Fachsystemen wechseln müssen.

## Entscheidung
Es wird ein eigenes Systemhaus Control Center entwickelt. Es aggregiert Fachinformationen und löst Aktionen über APIs/Workflows aus, wird aber kein zusätzlicher Master für Kunden, Assets oder Tickets.

## Konsequenzen
- modulare Plugin-Architektur
- fachliche Daten bleiben in Odoo, GLPI, Zammad usw.
- SSO über Keycloak
- Auditierbare Aktionen
- Homarr bleibt Startportal und wird nicht zum Ersatz des Control Centers