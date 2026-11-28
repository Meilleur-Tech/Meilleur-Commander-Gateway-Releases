# Fabric Commander Gateway 2.2.13

**Version:** 2.2.13
**Freigegebener Source-Commit:** `753ef2c54d4e64677d648e9c9deb18debbacb425`
**Plattformen:** x86_64 Debian/Ubuntu Linux-VM und Unraid.

## Änderungen gegenüber 2.2.12

- #2131: Explizite, standardmäßig leere HTTPS-Callback-Allowlist für OAuth. Der Betreiber muss die exakte Control-Rücksprungadresse über `MC_OAUTH_HTTPS_REDIRECT_URIS` konfigurieren. Bestehende OAuth-Regeln und PKCE S256 bleiben aktiv.
- #2135: Klarere Tool-Beschreibungen und MCP-Fehlerhinweise. Namespace aus dem Katalog übernehmen, registrierten Scope verwenden und nicht raten. Interne Fehlergründe für Audit und Paritätsbericht bleiben unverändert.
- #2138: Fehler invalidieren nur den Katalog-Cache der betroffenen Upstream-Instanz.

## Installation und Update

Beide binary-only-Kits werden über den RSA-SHA256-signierten Gateway-Katalog und die gebundenen SHA-256-Prüfsummen angeboten. Über das Gateway Update Center bewusst installieren, vorher Backup und freien Speicher prüfen. Für Control nach Installation die exakte HTTPS-Rücksprungadresse im Betreiber-Environment konfigurieren und den normalen Neustart verwenden. Keine automatische PROD-Konfigurationsänderung.

## Rollback und Wiederherstellung

Die Recovery Plane stellt bei fehlgeschlagenem Update den bekannten gesunden Vorgänger wieder her. Vorgänge mit unbekanntem Ergebnis vor einem erneuten Versuch abgleichen. Backup und vorherige Images bis erfolgreichem Postcheck behalten.

## Kompatibilität und Sicherheit

Native Desktop-Clients haben separate Releasekanäle. Keine automatische Rechteerweiterung. Katalogsignatur, Quellidentität, Paketprüfsummen und Recovery-Checks bleiben verbindlich. Der vollständige Control-OAuth-Rundlauf und die Hermes-Latenz-Nachmessung bleiben Laufzeitabnahme; Verbindungspooling ist nicht enthalten.
