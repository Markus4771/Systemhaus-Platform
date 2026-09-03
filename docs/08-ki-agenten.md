# KI-, RAG- und Agenten-Konzept

## Ziel

KI soll Mitarbeiter bei Recherche, Zusammenfassung, Dokumentation, Priorisierung und Entwicklung unterstützen. Zahlen und Statusinformationen müssen aus verlässlichen Fachsystemen stammen; die KI darf sie nicht erfinden.

## Komponenten

### OpenHands
Interner Entwicklungsagent für Codeanalyse, Änderungsvorschläge, Tests, Dokumentation und Pull Requests. Zielprozess: Issue -> Analyse -> Patch -> Tests -> PR -> menschliches Review.

### OpenClaw
Geplantes Agent-/Mitarbeiter-Gateway mit Tools, Skills, Webhooks und Automationen.

### RAG / Wissens-KI
Freigegebene Quellen:
- internes Wiki / Unternehmenshandbuch
- ausgewählte Nextcloud-Dokumente
- GLPI-Dokumentation und Assets
- gelöste Zammad-Tickets
- ausgewählte Odoo-Daten

Nicht indexieren:
- Passbolt-Secrets
- Passwörter/API-Schlüssel
- unnötige personenbezogene Daten

### AI Gateway
Zentrale Schicht für:
- Modellrouting
- Berechtigungen
- Datenklassifizierung
- Provider-Auswahl
- Logging/Audit
- Kostenkontrolle

## Hosting

OpenHands, OpenClaw und RAG-Dienste dürfen auf dem Business-Proxmox laufen. Die eigentlichen LLM-Modelle sollen auf einem separaten KI-Server oder bei externen Providern laufen.

## Sicherheitsmodell

1. KI darf technische und fachlich freigegebene Daten lesen.
2. KI darf Aktionen vorschlagen.
3. Änderungen laufen über kontrollierte APIs/n8n-Workflows.
4. Kritische Aktionen benötigen explizite Freigabe.
5. DATEV-, Secret- und sensible Personaldaten erhalten besonders restriktive Regeln.
6. RAG-Antworten sollen Quellen anzeigen.

## Sales Intelligence
KI kann vorhandene, deterministisch berechnete Vertriebsindikatoren zusammenfassen und priorisieren. Regeln wie `Serveralter > 5 Jahre` oder `aktive Geräte > Vertragsmenge` werden nicht von der KI geschätzt, sondern aus Fachsystemdaten berechnet.