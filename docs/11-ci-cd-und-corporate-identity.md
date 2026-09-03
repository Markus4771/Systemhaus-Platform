# CI/CD und Corporate Identity

Der Begriff `CI` wurde im Projekt in zwei sinnvollen Bedeutungen aufgenommen: Continuous Integration/Delivery und Corporate Identity.

## Continuous Integration / Delivery

Für Eigenentwicklungen wie Control Center, Asset & Onboarding Gateway, Stempeluhr, ContactSync und Integrationsdienste ist eine durchgängige Pipeline vorgesehen.

Zielprozess:

```text
Issue / Feature
  -> Branch
  -> automatisierte Tests
  -> Build
  -> Security-/Lint-Prüfung
  -> Testumgebung
  -> Pull Request / Review
  -> Freigabe
  -> Produktion
```

### Grundregeln
- `main` bleibt stabil.
- Änderungen bevorzugt über Pull Requests.
- Tests müssen vor Merge erfolgreich sein.
- Secrets nur über GitHub/Forgejo Secrets oder Deployment-Secret-Store.
- Test- und Produktiv-Konfiguration trennen.
- Builds versionieren und nachvollziehbar ausliefern.
- Datenbankmigrationen mit Rollback-/Backup-Plan.
- Deployment-Status und Fehler protokollieren.
- später OpenHands in den Issue->PR-Prozess integrieren, aber menschliches Review beibehalten.

## Corporate Identity / Design System

Eine gemeinsame visuelle Linie soll die vielen Oberflächen als zusammengehörige Plattform erkennbar machen.

### Zentrale Designwerte
- Logo und App-Icon
- Primär- und Sekundärfarbe
- Statusfarben für Erfolg, Warnung und Fehler
- Typografie
- Icon-Satz
- Formulare, Buttons und Navigation
- Hell-/Dunkelmodus
- gemeinsame Begriffe wie Kunde, Standort, Gerät, Ticket, Aufgabe, Projekt, Ansprechpartner

### Anwendungen
Eigene Anwendungen sollen das Design vollständig übernehmen. Homarr, Keycloak-Login und soweit praktikabel Odoo, Zammad, GLPI, Nextcloud und weitere Fremdsysteme sollen zumindest Logo, Farben und Einstiegseiten angleichen.

## Gemeinsame UX

Das Control Center soll eine einheitliche Kopfzeile und Navigation bieten. Homarr bleibt die Portal-/Startseite; das Control Center ist die fachliche Arbeitsoberfläche.