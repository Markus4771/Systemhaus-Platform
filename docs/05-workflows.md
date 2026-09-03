# Kern-Workflows

## 1. Neukunde

```text
Odoo
  -> Kunden-ID erzeugen/übernehmen
  -> n8n / Integration Core
      -> Zammad Organisation
      -> GLPI Entity
      -> Nextcloud Kundenordner
      -> später NetLock Gruppe
      -> später Checkmk Struktur
      -> später Passbolt Ordner/Referenz
```

## 2. Monitoring-Alarm

```text
Checkmk oder NetLock
  -> Integration Core
  -> n8n
  -> Kunde/Gerät über zentrale IDs ermitteln
  -> bestehendes Ticket auf Duplikat prüfen
  -> Zammad Ticket erzeugen/aktualisieren
  -> Techniker benachrichtigen
  -> bei Recovery Ticket automatisch ergänzen/auflösen
```

## 3. Neues Gerät

```text
Asset & Onboarding Gateway
  -> GLPI Asset anlegen
  -> NetLock Agent / RMM Zuordnung
  -> Hardware-, Software- und Patchdaten zurück nach GLPI
  -> Dokumentation vervollständigen
```

## 4. Ticket und Abrechnung

```text
Zammad Ticket
  -> Techniker erfasst Arbeitszeit
  -> Odoo Vertragsprüfung
  -> inklusive oder abrechenbar
  -> Rechnung
  -> DATEV
```

## 5. Vertragsabweichung

```text
GLPI aktive Geräte
  > Odoo vertraglich vereinbarte Geräte
  -> Sales Intelligence
  -> Aufgabe/Opportunity in Odoo
```

## 6. Bestellprozess

```text
Odoo Auftrag
  -> Lieferant/Distributor
  -> Bestellstatus
  -> Wareneingang
  -> Seriennummern
  -> GLPI Onboarding
  -> NetLock
  -> Liefer-/Installationstermin
  -> Rechnung
  -> DATEV
```

## 7. Kontakt-Synchronisation

Odoo ist der Geschäftskontakt-Master. ContactSync verteilt passende Daten an Nextcloud/CardDAV, Zammad, GLPI und VoIP. Für jedes Feld werden Richtung und Writeback-Regeln definiert.

## 8. Kalender

Ein Vor-Ort-Termin oder eine Aufgabe kann aus Zammad/Odoo entstehen und über Nextcloud Calendar per CalDAV in Thunderbird und auf Mobilgeräte verteilt werden.

## 9. Wissenssuche

```text
Ticket / Problem
  -> RAG sucht nur freigegebene Quellen
     - Wiki
     - Nextcloud Dokumentation
     - GLPI
     - gelöste Zammad Tickets
  -> Antwort mit Quellenhinweisen
  -> Techniker entscheidet
```

Passbolt-Inhalte und Secrets werden nicht indexiert.

## 10. Entwicklung

```text
GitHub Issue
  -> OpenHands
  -> Analyse / Patch / Tests
  -> Pull Request
  -> menschliches Review
  -> Merge / Deployment
```

## 11. Personal und Zeiten

Anwesenheitszeit aus der eigenen Stempeluhr wird getrennt von abrechenbarer Ticket-/Projektzeit behandelt. Kapazitätsplanung kombiniert Anwesenheit, Urlaub, Aufgaben und Projektplanung.

## 12. Home Assistant

Interne Gebäude-/IoT-Ereignisse können bei Bedarf über n8n weiterverarbeitet werden, z. B. hohe Serverraumtemperatur -> Benachrichtigung oder Zammad-Ticket. Kritische Automationen werden getrennt von Kunden-IT und klar berechtigt betrieben.