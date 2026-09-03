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

Jeder Kunde erhält eine unveränderliche technische ID, z. B.:

`K-000001`

Diese ID wird in allen integrierten Systemen gespeichert bzw. referenziert:

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

1. Die Kunden-ID wird nur einmal erzeugt.
2. Nachträgliche Namensänderungen ändern die ID nicht.
3. Synchronisation erfolgt bevorzugt über die ID, nicht über Firmennamen oder E-Mail-Adressen.
4. Fremdschlüssel/IDs der einzelnen Fachsysteme werden im Integration Core gemappt.
5. Bei Konflikten gewinnt das definierte führende System.
6. Löschungen werden nicht blind repliziert; sie benötigen definierte Lifecycle-Regeln.

## Offene Entscheidung

Es ist noch festzulegen, ob die zentrale Kunden-ID direkt in Odoo erzeugt wird oder durch den Integration Core vergeben und danach nach Odoo zurückgeschrieben wird. Für den ersten PoC ist eine Erzeugung in Odoo ausreichend.