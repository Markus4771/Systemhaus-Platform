# Datenhoheit und zentrale IDs

## Grundsatz

Für jede Datenart gibt es genau ein führendes System. Andere Systeme erhalten Kopien oder Referenzen nur soweit fachlich nötig.

## Vorgesehene führende Systeme

| Datentyp | Führendes System | Bemerkung |
|---|---|---|
| Kunde / kaufmännischer Kundenstamm | Odoo | zentraler Ursprung für Kundenanlage |
| Geschäftskontakte | Odoo | Verteilung über ContactSync/n8n |
| Assets / Geräte / CMDB | GLPI | technische Asset-Hoheit |
| Tickets / SLA / Supportkommunikation | Zammad | Service-Hoheit |
| Dokumente | Paperless bzw. Nextcloud je Dokumenttyp | klare Zuordnung pro Klasse nötig |
| Benutzeridentität / SSO | Keycloak | Authentifizierung; Fachrechte bleiben im Zielsystem |
| Secrets | Passbolt | niemals in andere Systeme oder RAG kopieren |
| Monitoring-Zustand | Checkmk | technische Überwachung |
| Endpoint-/RMM-Zustand | NetLock RMM | Endpunktdaten und Remote Management |
| Anwesenheitszeit | Stempeluhr | von abrechenbarer Servicezeit trennen |
| Projekte, Angebote, Verträge, Abrechnung | Odoo | kaufmännische Hoheit |
| Ticketspezifische Arbeitszeit | Zammad | Übergabe an Odoo zur Abrechnung möglich |

## Zentrale Kunden-ID

Als zentrale Customer-ID wird **die bereits im Unternehmen verwendete Kundennummer** übernommen. Es wird keine zusätzliche technische Nummer wie `K-000001` eingeführt.

Beispiel einer bestehenden Kundennummer:

`10028`

Die Kundennummer muss eindeutig, dauerhaft und unveränderlich einem Kunden zugeordnet sein. Sie wird als gemeinsamer Schlüssel in allen integrierten Systemen gespeichert bzw. referenziert:

- Odoo
- Zammad
- GLPI
- Nextcloud
- Paperless
- NetLock RMM
- Checkmk
- Passbolt-Struktur
- Control Center
- Integrations- und Reporting-Schicht

## Regeln

1. Bestehende betriebliche Kundennummern werden übernommen.
2. Neue Kunden erhalten ihre Kundennummer im führenden kaufmännischen System Odoo bzw. nach dem dort festgelegten Nummernkreis.
3. Eine Kundennummer darf niemals einem anderen Kunden erneut zugeordnet werden.
4. Nachträgliche Namens-, Adress- oder Ansprechpartneränderungen ändern die Kundennummer nicht.
5. Synchronisation erfolgt bevorzugt über die Kundennummer, nicht über Firmennamen oder E-Mail-Adressen.
6. Fremdschlüssel/IDs der einzelnen Fachsysteme werden im Integration Core auf die zentrale Kundennummer gemappt.
7. Bei Konflikten gewinnt das definierte führende System.
8. Löschungen werden nicht blind repliziert; sie benötigen definierte Lifecycle-Regeln.

## Entscheidung

Die bisher geplante zusätzliche technische Kunden-ID im Format `K-000001` wird verworfen. Die vorhandene betriebliche Kundennummer ist die zentrale Customer-ID der Systemhaus-Plattform.

Für den ersten PoC wird geprüft, in welchem Odoo-Feld die vorhandene Kundennummer gespeichert ist und wie sie über n8n zuverlässig an Zammad und GLPI übertragen wird.