# Business-, Vertriebs- und Planungsmodule

## Sales Intelligence / Kundenanalyse

Ziel ist, Bestandskunden datenbasiert auf technische und kaufmännische Potenziale zu analysieren. Die Analyse soll Informationen aus Odoo, DATEV, GLPI, NetLock RMM, Checkmk, Zammad, Bestellhistorie und Lizenzdaten zusammenführen.

Beispiele für Kennzahlen:
- Umsatz Vorjahr / aktuelles Jahr
- offene Angebote und Rechnungen
- wiederkehrender Managed-Service-Umsatz
- Anzahl Endgeräte und Server
- Serveralter / ältester Server
- Firewall-Alter
- Garantieabläufe
- M365-/Software-Lizenzen
- Ticketanzahl und Supportstunden
- vertragliche Gerätezahl vs. tatsächlich aktive Geräte
- Verlängerungs- und Kündigungstermine

Deterministische Regeln sollen Chancen erkennen, z. B. Server älter als fünf Jahre, mehr Geräte als vertraglich vereinbart, auslaufende Garantie, ungewöhnlich hoher Supportaufwand, alte Firewall, fehlendes Offsite-Backup oder fehlendes Monitoring. Erst danach darf KI die Ergebnisse zusammenfassen oder priorisieren. Opportunities/Tasks landen in Odoo.

## Lead Intelligence / Neukundengewinnung

Eigenes Modul zur rechtmäßigen Suche und Qualifizierung neuer Firmenkunden anhand öffentlicher Unternehmensinformationen. Filter können Region/Radius, Branche, Mitarbeiterzahl und Unternehmensgröße umfassen. Ergebnisse werden bewertet und als Leads in Odoo angelegt. Aggressives Scraping oder unnötige Sammlung personenbezogener Daten ist nicht Ziel.

## Budget und Controlling

Bevorzugt Odoo plus eigenes Control-Center-Modul statt eines weiteren ERP. Geplant:
- Jahresbudgets
- Kostenstellen
- Ist/Plan
- Investitionen
- Rolling Forecast
- Pipeline- und Auftragsdaten aus Odoo
- Ist-Finanzdaten aus DATEV soweit verfügbar
- offene Bestellverpflichtungen
- Personalkosten und Kapazitäten

## Personal- und Kapazitätsplanung

Vier Datenarten werden bewusst getrennt:
1. Anwesenheitszeit aus der Stempeluhr
2. geplante Arbeitszeit, Urlaub und Teilzeit
3. Aufgaben-/Projektlast
4. abrechenbare Ticket-/Servicezeit

Zielanzeige: verfügbare Technikerstunden vs. bereits verplante Stunden sowie eine realistische Ressourcenplanung.

## Aufgaben- und Projektplanung

Ticket, Aufgabe und Projekt bleiben unterschiedliche Objekte. Service- und Projektaufgaben sollen im Control Center unabhängig vom jeweiligen Backend sichtbar sein und mit Kalendern verknüpft werden.

## Reporting / BI

Für übergreifende Auswertungen soll eine separate BI-Schicht geprüft werden. Metabase ist die bevorzugte erste Option; Apache Superset bleibt Alternative.