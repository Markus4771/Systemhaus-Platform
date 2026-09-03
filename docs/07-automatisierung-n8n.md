# Automatisierung mit n8n

## Rolle von n8n

n8n ist die zentrale Workflow-Orchestrierung der Plattform. Es verbindet APIs, Webhooks, Benachrichtigungen und Freigaben. Es soll jedoch weder führende Fachsysteme ersetzen noch zum dauerhaften Integrations-Datenspeicher werden.

## Zielbild

```text
Fachsystem
  -> API/Webhook/Event
  -> Integration Core
  -> n8n Workflow
  -> Zielsystem(e)
```

Für einfache PoC-Flows darf n8n zunächst direkt mit Odoo, Zammad und GLPI kommunizieren. Der Integration Core wird ergänzt, sobald gemeinsame IDs, Mapping, Retry, Queueing und Audit systemübergreifend gebraucht werden.

## Anforderungen an produktive Workflows

- idempotente Verarbeitung
- eindeutige Correlation-ID
- Logging pro Lauf
- Retry mit Backoff
- Dead-Letter-/Fehlerpfad
- Duplikaterkennung
- keine Secrets in Workflow-Logs
- getrennte Credentials je Zielsystem
- Test- und Produktiv-Credentials trennen
- manuelle Freigaben für kritische Änderungen
- Versionierung der Workflows

## Erste Workflows

### PoC-001: Kunde synchronisieren
Trigger: neuer/aktualisierter Kunde in Odoo.

Aktionen:
1. zentrale Kunden-ID prüfen
2. Organisation in Zammad suchen/erzeugen
3. Entity in GLPI suchen/erzeugen
4. Mapping der externen IDs speichern
5. Ergebnis protokollieren

### PoC-002: Paperless-Zuordnung
Dokument erhält eine Kundenreferenz und wird anhand der zentralen Kunden-ID korrekt zugeordnet.

### PoC-003: Monitoring zu Ticket
Checkmk/NetLock-Alarm wird dedupliziert und als Zammad-Ticket erzeugt bzw. aktualisiert.

## Spätere Automationen

- Kunden-Onboarding und Offboarding
- Mitarbeiter-Onboarding und Offboarding
- Bestellung und Wareneingang
- Vertrags-/Lizenzablauf
- Backup-Fehler
- Domain-/SSL-Ablauf
- Rechnungs-/Lieferscheinworkflow
- Kalender-/Vor-Ort-Termine
- Vertriebschancen
- KI-gestützte Vorschläge mit Freigabe