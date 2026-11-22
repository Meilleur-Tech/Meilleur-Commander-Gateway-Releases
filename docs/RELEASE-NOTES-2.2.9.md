# Fabric Commander Gateway 2.2.9

**Quellversion:** 2.2.9
**Freigegebener Source-Commit:** `5fdbdb2f3148d4bfee326b4f64f1e228ddd3ed55`
**Plattformen:** x86_64 Linux VM (Debian/Ubuntu) und Unraid

## Änderungen

- **OAuth-Verbindungen zu MCP-Anbietern:** Die Ablaufzeit eines Access-Tokens wird dauerhaft im verschlüsselten Speicher geführt. Ein abgelaufenes Token wird nicht mehr irrtümlich weiterverwendet; stattdessen nutzt das Gateway den zuvor ausdrücklich genehmigten Refresh-Token, ohne dass ein neuer Browser-Consent nötig ist. Erst bei fehlendem oder widerrufenem Refresh-Token ist eine neue Anmeldung erforderlich. Liefert ein Anbieter keine Ablaufzeit, bleibt das Token nutzbar. Eine fehlende OAuth-Freigabe in der Werkzeugvorschau erscheint als ausdrückliche Neuautorisierung. Der Refresh ist durch Tests belegt, ohne Live-Provider-Session.
- **Regelwerk für MCP-Verbindungen:** Betreiber legen fest, welcher Client welche Werkzeuge eines angebundenen MCP-Servers nutzen darf (Regeln, die erste passende gilt, Standard `allow`). Die Entscheidungen werden ohne Argumente protokolliert; verbotene Werkzeuge verschwinden aus Katalog und Vorschau. In 2.2.9 wird das Regelwerk über die WebUI-API verwaltet, die Bedienoberfläche folgt in einem späteren Release. Grenze: Ein Verbot für einen Client lässt sich durch eine Neuregistrierung (neuer Fingerprint) umgehen.
- **Werkzeug-Freigaben:** Ein Werkzeug mit verändertem Schema wird angehalten und nicht mehr still neu freigegeben. NOC-Token werden nur bei einer echten Ablehnung gelöscht, der Rücksprung des Anbieters ist geordnet.
- **Zugangsdaten und Pairing:** Die WebUI-Zugangsdatei entsteht sofort mit Modus `0600` und wird atomar geschrieben. Neue oder geänderte Passwörter dürfen höchstens 256 Zeichen haben. Das Pairing hat ein Limit je Quelle und räumt Altlasten auf, Fehlversuche beim Login werden verzögert, und das Bestätigen eines Pairings verlangt ein CSRF-Token.
- **Bridge:** Es wird kein Bearer-Token an Weiterleitungsziele gesendet. Der Heartbeat ist robuster, Telemetriefehler verlieren kein Job-Ergebnis, und eine monotone Instanzprüfung verhindert veraltete Instanzen.
- **Update und Betrieb:** Der Update-Plan blockiert Downgrades, das Image enthält einen HEALTHCHECK, der Federation-Edge läuft ohne root, und die Zielbindung beim Gateway-Update ist Pflicht. Die Betriebsskripte laufen auch unter macOS-bash 3.2.
- **Abhängigkeiten:** opentelemetry-api 1.45.2, PyJWT 2.15.1 und dnspython 2.9.2 schließen 20 der 21 gemeldeten Schwachstellen, darunter eine nach Anmeldung erreichbare ReDoS. Eine weitere Meldung betrifft ein Paket, für das kein Anbieter-Fix verfügbar ist.
- **Enrollment:** `enroll` nimmt den Einmal-Code per `--code-stdin` oder `--code-file` (private Datei) entgegen und nicht mehr nur als Prozessargument; das Positionsargument warnt.
- **WebUI:** In allen Aktionsdialogen mit Projekt- oder Agent-Auswahl ist das Auswahlfeld wieder bedienbar (u. a. „Aufgabe zuweisen“, das sich vorher nicht absenden ließ); der Fokus bleibt nach der Auswahl auf dem Auslöser. Der Einklapp-Knopf der Seitenleiste wird nicht mehr verdeckt, die Einstellungen haben ein eigenes Symbol, die Live-Anzeige ist nur bei bestätigtem Gateway-Status grün, und die MCP-Einstellungen scrollen bei 320 und 375 px nicht seitlich. MCP-Fehler erscheinen als verständlicher Text. Pro angebundenem MCP-Server ist die Werkzeugliste standardmäßig eingeklappt. Bekannt: Escape bei geöffneter Auswahl schließt den ganzen Dialog.
- **Claude.ai:** Der Rücksprung-Callback von Claude.ai wird zusätzlich zu den bestehenden ChatGPT-Callbacks akzeptiert (PKCE und Ressourcenrechte bleiben). Weitere Claude-Funktionen wie Claude-Code-Sitzungen und „Verbundene KI-Clients“ sind nicht Teil dieses Release.

## Hinweise für Betreiber

1. **Regelwerk:** Beim ersten Start nach dem Update wird `policy.sqlite3` mit dem Marker `policy-initialized` (Modus `0600`) unter `$MC_STATE_DIR/upstream-mcp/` mit dem Standard `allow` angelegt; bestehende Verbindungen laufen weiter. Ist der Marker vorhanden, das Regelwerk aber nicht, scheitern die `upstream_*`-Werkzeuge geschlossen (`upstream_policy_unavailable`): aus dem Backup wiederherstellen oder einmalig `MC_UPSTREAM_POLICY_RECREATE=1` setzen (leeres Regelwerk mit Standard `deny`, Warnung bei jedem Start, solange die Variable gesetzt ist). Unbekannte oder annotationslose Werkzeuge gelten als `destructive`. Endpunkte: `GET /api/mcp/connections`, `GET|PUT /api/mcp/policy`, `GET /api/mcp/log`; Änderungen nur mit Owner-Rechten.
2. **Werkzeug-Freigaben:** Nach einem Control-/NOC-Update müssen veränderte Werkzeuge in der WebUI erneut freigegeben werden.
3. **Pairing:** neue Variable `MC_CLIENT_PAIRING_MAX_PER_SOURCE` (Standard 25, 1 bis 1000); die Pairing-Datenbank wird an Ort und Stelle migriert. Hinter einem Tunnel greift das Limit je Quelle nur, wenn der Tunnel in `MC_WEB_TRUSTED_PROXIES` steht.
4. **Passwörter:** Neue oder geänderte WebUI-Passwörter sind auf 256 Zeichen begrenzt. Ein Passwort aus `MC_WEB_PASSWORD` mit mehr als 1024 Zeichen gilt als nicht konfiguriert; vor dem Update prüfen.
5. **Weiterleitungen:** Eine `gateway_url`, die weiterleitet, funktioniert nicht mehr (`redirect_not_followed`); die endgültige HTTPS-Adresse direkt eintragen.
6. **Abhängigkeiten:** Die neuen Versionen wirken erst mit dem neu gebauten Image dieses Release; ein bestehender Container bleibt unverändert, bis das Update installiert ist.
7. **Downgrades und Federation:** Der Update-Plan blockiert Downgrades (`downgrade_not_allowed`). Nur bei genutzter Federation: ein von root angelegtes, per Bind-Mount eingebundenes `/state` einmalig mit `chown -R 10001:10001` übergeben.

## Installation und Update

Nach der öffentlichen Freigabe erfolgt die Installation über den bestehenden Gateway Update Center. Vorher die RSA-Signatur, die Paket-SHA256, die passende Plattform, die Gateway-/Worker-Imageidentitäten, den verfügbaren Speicher und das Backup prüfen. Ein veröffentlichter Build installiert das Gateway niemals automatisch auf einem Produktivsystem.

## Rollback und Sicherheit

Die isolierte QA hat für exakt diesen Commit sechs Prüfungen bestanden: reines Binär-Paket, Gateway-Update, Operationsfortschritt, Postcheck, Fortsetzung nach einem Neustart und automatischer Rollback. Das QA-Ergebnis ist separat signiert und an die Originalartefakte gebunden. Ungeklärte Operationszustände bleiben ein Stoppsignal: erst untersuchen, dann erneut versuchen.

Das Update bleibt kompatibel mit der bisherigen RSA-SHA256-Verifikation; es gibt keine neue Signaturidentität. OAuth-Rechte, Kunden-ACLs und Werkzeugfreigaben werden durch das Update nicht automatisch erweitert.

## Kompatibilität

Die offiziellen Gateway-Kits sind für Unraid und unterstützte Debian-/Ubuntu-Linux-VMs auf x86_64 bestimmt. Native macOS-, Windows- und Linux-Desktopclients behalten eigenständige Releases und Signaturen. Ein Gateway-Update ersetzt keinen Client-Build.
