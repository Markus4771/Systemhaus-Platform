# Systemhaus Control Center

## Zweck

Das Control Center ist das zentrale Techniker-Cockpit. Es ersetzt die Fachsysteme nicht, sondern zeigt kundenbezogene Informationen gebündelt an und stößt kontrollierte Aktionen über APIs und n8n an.

## Kundenansicht

Für einen Kunden sollen mindestens sichtbar sein:

- Stammdaten und Ansprechpartner
- offene und letzte Tickets
- Geräte und Server
- Monitoringstatus
- RMM-Status
- Verträge und Lizenzen
- Dokumente
- letzte Tätigkeiten
- offene Aufgaben/Projekte
- Service- und Vertragsinformationen

## Schnellaktionen

- Ticket anlegen
- Remotezugriff starten
- Gerät erfassen
- Passwort/Secret über sicheren Link öffnen
- Dokumentation öffnen
- Kunde anrufen / Click-to-Call
- Arbeitszeit starten/stoppen
- Vor-Ort-Termin planen
- Vertriebschance anlegen

## Plugin-Architektur

Geplante Module:

- plugin-odoo
- plugin-zammad
- plugin-glpi
- plugin-netlock
- plugin-checkmk
- plugin-paperless
- plugin-nextcloud
- plugin-passbolt
- plugin-keycloak
- plugin-stempeluhr
- plugin-datev
- plugin-voip
- plugin-sales-intelligence
- plugin-lead-intelligence

## Architekturregeln

- keine unnötige lokale Kopie der Fachsystemdaten
- Caching nur mit klarer Ablaufzeit
- Aktionen immer mit Benutzeridentität und Audit-Trail
- Berechtigungen aus Keycloak plus fachliche Rechte im Zielsystem
- Fehlende Zielsysteme dürfen andere Plugins nicht blockieren
- jeder Connector braucht Health-Status, Timeout, Retry und klare Fehlermeldungen

## Homarr-Abgrenzung

Homarr ist die zentrale Startseite mit Links/Kacheln und Statusinformationen. Das Control Center ist die fachliche Arbeitsoberfläche für den Service. Beide können optisch dieselbe Corporate Identity erhalten.