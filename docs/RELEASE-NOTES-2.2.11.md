# Fabric Commander Gateway 2.2.11

**Version:** 2.2.11  
**Freigegebener Source-Commit:** `1749e9b1ef4b08c7aaea8f67b9f46dfb3dcd6dbb`  
**Plattformen:** x86_64 Debian/Ubuntu Linux-VM und Unraid  
**QA:** 7 von 7 echten Checks bestanden, einschließlich Rollback, Fortschritt, Neustart-Wiederaufnahme, Health, Binary-Only-Audit und lokalem Prozessstart.

## Änderungen gegenüber 2.2.10

- **Hermes OAuth (Owner-Demo):** Der Gateway unterstützt einen ausdrücklich per SHA-256-Client-Fingerprint freigegebenen OAuth-Client ohne Chat-Sitzungsscope an `/mcp`, indem er einen serverseitigen internen Owner-Scope ableitet. Die Einstellung `MC_ROOT_SCOPELESS_OWNER_CLIENT_FINGERPRINTS` ist **standardmäßig deaktiviert**, nur für `owner_internal` vorgesehen und erteilt Kunden oder anderen Clients keinerlei zusätzliche Rechte. Ein Update aktiviert Hermes nicht automatisch.
- **Worker und SSH:** Prozessstarts, die bereits gestorben sind, geben Quoten und Journal zuverlässig frei; begrenzte getrennte Pools, kontrollierte Probes und sauber aufgeräumte Handles verbessern Stabilität und Fehlermeldungen.
- **MCP-Konsole:** Ungespeicherte Regeln und Alias-Eingaben werden geschützt. Kleinere Bedienflächen und ein angepasstes Raster verbessern die Anzeige auf schmalen Bildschirmen.
- **Sicherheit und Betrieb:** Erweiterte Prüfungen für persistente Schema-Kompatibilität, verbesserte macOS-QA und gehärtete Runner-/Release-CI. Alle seit Source 2.2.10 gemergten freigegebenen Änderungen sind enthalten, nicht nur der Hermes-Hotfix.

## Installation und Update

Die beiden unveränderlichen binary-only-Kits für `linux-vm` und `unraid` werden ausschließlich über den RSA-SHA256-signierten Gateway-Katalog und die dort gebundenen SHA-256-Prüfsummen angeboten. Über das **Gateway Update Center** die passende Version auswählen und die Installation bewusst bestätigen. Vorher ausreichend freien Speicher, verifiziertes Backup und bekannte gesunde Vorversion sicherstellen. Die Veröffentlichung allein installiert nichts auf PROD.

## Rollback und Wiederherstellung

Der Recovery-Plane-Pfad bewahrt einen bekannten gesunden Vorgänger und stellt ihn bei fehlgeschlagenem Update/Healthcheck automatisch wieder her. Ein bestehender Vorgang mit unbekanntem Ergebnis muss erst abgeglichen werden. Bei einem Rollback auf Gateway 2.2.9 die seit 2.2.10 geltenden Betreiberhinweise zu CIDR-Einträgen in `MC_WEB_TRUSTED_PROXIES` beachten: Vor dem Rückgang auf 2.2.9 durch einzelne Adressen ersetzen.

## Kompatibilität und Sicherheit

Die Kits unterstützen x86_64 Linux-VMs (Debian/Ubuntu) und Unraid. Native macOS-, Windows- und Linux-Clients haben eigene Releasekanäle. Für den Hermes-OAuth-Sonderfall sind eine ausdrücklich geprüfte private Client-Registrierung, gültiges OAuth für die kanonische MCP-Ressource und eine separate Owner-Freigabe erforderlich. Legacy-Endpunkte sowie bestehende Policy-/Upstream-Regeln bleiben unverändert. RSA-SHA256-Katalogsignatur, Quellidentität, Paketprüfsummen und Recovery-Checks dürfen nicht deaktiviert werden.

Weitere technische Änderungen und Prüfgrundlagen: [Gateway-Release-Auftrag #2129](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/2129).
