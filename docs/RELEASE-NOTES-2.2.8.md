# Fabric Commander Gateway 2.2.8

**Quellversion:** 2.2.8
**Freigegebener Source-Commit:** `851e57674a68201f5aa507522cb15f1e3907d6df`
**Plattformen:** x86_64 Linux VM (Debian/Ubuntu) und Unraid

## Änderungen

- Der universelle MCP-Wizard zeigt dynamisch die vom Anbieter tatsächlich angebotenen und durch HTTPS-Metadaten verifizierten OAuth-Berechtigungen. Neue NOC-Rechte bleiben ungegrantet, bis der Benutzer sie ausdrücklich freigibt; erhöhte Rechte benötigen eine zusätzliche Bestätigung.
- Die OAuth-Neuanmeldung für Lexit Apps kann bewusst gestartet werden. Ein alter Token bleibt erhalten, bis der neue PKCE-Callback vollständig erfolgreich ist. Fehlender persönlicher Consent wird als erneute Autorisierung und nicht als allgemeiner Verbindungsfehler gemeldet.
- Die native Bridge vermeidet beschädigte oder unnötig große Textkopien von Binärdateien und liefert bei zu großen Resultaten einen eindeutigen Fehler statt wiederholter Reconnects.
- Die Linux-VM-Recovery stellt beim fehlgeschlagenen Docker-Cutover unmittelbar die vorherige bekannte gute Version wieder her. Publisher-Korrekturen vereinheitlichen den GitHub-Ref-Updatepfad und die Prüfung aller sieben Release-Assets.

## Installation und Update

Nach der öffentlichen Freigabe erfolgt die Installation über den bestehenden Gateway Update Center. Vorher die RSA-Signatur, Paket-SHA256, passende Plattform, die Gateway-/Worker-Imageidentitäten, verfügbaren Speicher sowie das Backup prüfen. Ein veröffentlichter Build installiert niemals automatisch das Gateway auf PROD.

## Rollback und Sicherheit

Die isolierte QA hat für exakt diesen Commit den automatischen Image-Rollback auf Gateway 2.2.7 bei verweigertem Kandidatenstart sowie einen echten Docker-Neustart während einer aktiven 2.2.8-Updateoperation mit erfolgreicher Fortsetzung nachgewiesen. Die sechs QA-Nachweise wurden separat signiert und an die Originalartefakte gebunden. Ungeklärte Operationszustände bleiben ein Stoppsignal.

Das Update bleibt kompatibel mit der bisherigen RSA-SHA256-Verifikation. Eine zukünftige Sigstore-/Cosign-Signierung ist vorbereitet, aber für Gateway 2.2.8 nicht als produktiver Signaturpfad aktiviert. OAuth-Rechte, Kunden-ACLs und Werkzeugfreigaben werden durch das Update nicht automatisch erweitert.

## Kompatibilität

Die offiziellen Gateway-Kits sind für Unraid und unterstützte Debian-/Ubuntu-Linux-VMs auf x86_64 bestimmt. Native macOS-, Windows- und Linux-Desktopclients behalten eigenständige Releases und Signaturen. Ein Gateway-Update ersetzt keinen Client-Build.
