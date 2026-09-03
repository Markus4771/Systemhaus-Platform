# ADR-003: n8n als zentrale Workflow-Orchestrierung

## Status
Akzeptiert

## Kontext
Die Plattform benötigt viele systemübergreifende Abläufe, Freigaben, Benachrichtigungen und API-Aufrufe.

## Entscheidung
n8n wird als zentrale Workflow-Orchestrierung eingesetzt. Für robuste Integrationen wird zusätzlich ein kleiner Integration Core/API Gateway vorgesehen.

## Abgrenzung
n8n ist nicht:
- führende Datenbank
- Ersatz für Fachsysteme
- alleinige Echtzeit-/High-Volume-Middleware

## Konsequenzen
PoC-Workflows dürfen direkt mit APIs arbeiten. Produktive kritische Flows benötigen Idempotenz, Retry, Logging, Correlation-ID, Deduplizierung und ggf. Queueing.