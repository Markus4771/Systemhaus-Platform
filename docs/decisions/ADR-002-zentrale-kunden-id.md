# ADR-002: Zentrale unveränderliche Kunden-ID

## Status
Akzeptiert

## Kontext
Firmennamen, E-Mail-Adressen und Ansprechpartner sind keine stabilen systemübergreifenden Schlüssel.

## Entscheidung
Jeder Kunde erhält eine unveränderliche zentrale ID im Format `K-000001` oder kompatibel. Diese ID wird in allen relevanten Fachsystemen gespeichert oder referenziert.

## Konsequenzen
- Synchronisation und Zuordnung erfolgen primär über diese ID.
- Namensänderungen erzeugen keinen neuen Kunden.
- Systeminterne IDs werden zusätzlich im Integration Core gemappt.
- Die genaue zentrale Erzeugungsstelle wird noch festgelegt; im ersten PoC darf Odoo die ID führen.