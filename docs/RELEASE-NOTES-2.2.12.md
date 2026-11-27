# Fabric Commander Gateway 2.2.12

**Version:** 2.2.12  
**Freigegebener Source-Commit:** `e9fd908ff2d1e55ff4ab83aa7277f854bc10dc20`  
**Plattformen:** x86_64 Debian/Ubuntu Linux-VM und Unraid.

## Änderungen gegenüber 2.2.11

- Upstream-Policy-Klassifikationen werden gebündelt aus der Datenbank gelesen; die bestehenden Live-Autorisierungs- und Schema-Prüfungen bleiben erhalten.
- Optionaler gefilterter und kompakter Tool-Katalog (`query`, `compact`), optionaler Katalog-Cache bis 300 Sekunden je authentifiziertem Client-/Session-Scope (`max_age_seconds`).
- `compact_result=true` entfernt ausschließlich identische, doppelte JSON-Textrepräsentationen; keine fachlichen Daten werden verworfen. Standardantworten bleiben kompatibel.
- Laufzeitmessungen für Verbindung, Discovery und Ausführung sind im normalen Gateway-Log sichtbar, ohne Argumente oder Ergebnisse zu protokollieren.
- Parallel aktive Chat-Sessions verdrängen bei erfolgreichen Katalogabfragen nicht mehr gegenseitig ihre Cache-Einträge.

## Bekannte Einschränkung

Ein Fehler einer Upstream-Verbindung kann auch gültige Cache-Einträge anderer Verbindungen verwerfen. Die Ausführung bleibt funktionsfähig; die Cache-Invalidierung je Instanz folgt in 2.2.13. Die tatsächliche Ende-zu-Ende-Beschleunigung ist noch nicht gemessen. Verbindungspooling und generische Ergebnis-Pagination sind nicht enthalten.

## Installation und Update

Die beiden binary-only-Kits für Linux-VM und Unraid werden über den RSA-SHA256-signierten Gateway-Katalog und die dort gebundenen SHA-256-Prüfsummen angeboten. Über das Gateway Update Center die Version auswählen und die Installation bewusst bestätigen. Vorher ausreichend freien Speicher, verifiziertes Backup und bekannte gesunde Vorversion sicherstellen. Die Veröffentlichung allein installiert nichts auf PROD.

## Rollback und Wiederherstellung

Die Recovery Plane bewahrt den bekannten gesunden Vorgänger und stellt ihn bei fehlgeschlagenem Update/Healthcheck automatisch wieder her. Ein bestehender Vorgang mit unbekanntem Ergebnis muss erst abgeglichen werden. Bei einem Rollback auf Gateway 2.2.9 gelten die Betreiberhinweise zu CIDR-Einträgen in MC_WEB_TRUSTED_PROXIES aus 2.2.10.

## Kompatibilität und Sicherheit

Native macOS-, Windows- und Linux-Clients haben separate Releasekanäle. Es erfolgt keine State-Migration. Katalogsignatur, Quellidentität, Paketprüfsummen und Recovery-Checks dürfen nicht deaktiviert werden. Die neuen kompakten und Cache-Optionen sind opt-in; Clients müssen sie aktiv nutzen.
