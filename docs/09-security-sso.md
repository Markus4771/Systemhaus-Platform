# Security, SSO und Berechtigungen

## Keycloak

Keycloak ist als zentrale Identitäts- und SSO-Schicht vorgesehen. Ziel ist ein einheitlicher Login mit MFA für Homarr, Control Center und möglichst viele Fachsysteme.

## Grundsätze

- Authentifizierung zentral, fachliche Berechtigungen weiterhin im jeweiligen Zielsystem
- Least Privilege
- getrennte Service-Accounts für Integrationen
- MFA für administrative und kritische Rollen
- keine gemeinsamen Administrator-Konten
- Secrets ausschließlich im Secret-Manager bzw. sicheren Credential Stores
- keine API-Schlüssel in Git oder n8n-Exports einchecken
- Test und Produktion strikt trennen
- Audit-Logs für kritische Aktionen
- Berechtigungsprüfung auch serverseitig im Control Center

## Rollenmodell

Vorgesehene Rollenklassen:
- Administration
- Servicetechniker
- Vertrieb
- Geschäftsleitung
- Automations-/Service-Account
- später Kunde/Portalbenutzer

## Mandantenfähigkeit

Kundendaten müssen über zentrale Kunden-ID und fachliche Mandanten-/Entity-Strukturen getrennt bleiben. Ein Benutzer darf nur die Daten sehen, für die er berechtigt ist.

## Wazuh / SIEM

Wazuh ist als spätere Ausbaustufe vorgesehen. Erst nach Stabilisierung der Kernintegration sollen Logs und Security Events zentral korreliert werden.

## Backup und Wiederherstellung

- Proxmox Backup Server möglichst getrennt vom Produktivhost
- regelmäßige Restore-Tests
- Backup-Fehler automatisch melden
- Konfigurations- und Datenbank-Backups je Anwendung
- Offsite-Kopie für kritische Daten
- Wiederanlaufverfahren dokumentieren

## KI-Sicherheit

KI erhält niemals pauschalen Vollzugriff. Aktionen werden über definierte Tools/APIs begrenzt und bei kritischen Änderungen durch Freigaben abgesichert.