# Fabric Commander Gateway 2.2.10

**Quellversion:** 2.2.10
**Freigegebener Source-Commit:** `fe102ba6e61eaf6eebb5cc6c4449726e7bcf6be8`
**Plattformen:** x86_64 Linux VM (Debian/Ubuntu) und Unraid
**QA:** 6 von 6 bestanden, `local_process` von Hand belegt.

## Änderungen

- **MCP-Konsole (neu, Vorschau):** Die WebUI hat einen Bereich „MCP-Konsole“: welcher Client mit welchem MCP-Server spricht, was abgelehnt wurde und warum. Das Regelwerk aus 2.2.9 lässt sich dort bearbeiten (Reihenfolge, Standardaktion, Speichern mit Diff, Konflikterkennung). Der Tab „Server“ ist ein Neubau der MCP-Seite (Server registrieren, OAuth, Werkzeuge und Hosts freigeben) und läuft bei 320 px nicht mehr seitlich über. Neu dort der **Werkzeug-Abgleich**: „Parität prüfen“ zeigt je Server, welche Werkzeuge des Anbieters das Gateway nicht anbietet, jeweils mit Grund; gekürzte Listen heißen „Unvollständig (Grund)“, die Zahlen sind dann eine Untergrenze; nur lesend. Neu ist auch der Owner-Endpunkt `POST /api/mcp/policy/dry-run`: er wertet einen Regel-Entwurf aus, ohne etwas zu speichern (noch ohne Oberfläche). Die bisherige MCP-Seite bleibt bestehen.
- **Vertrauenswürdige Proxys:** `MC_WEB_TRUSTED_PROXIES` nimmt auch CIDR-Netze (z. B. `172.17.0.0/16`); zu weite Netze werden ignoriert und einmal geloggt.
- **Pairing und Anmeldung:** keine Zugangsdatenfelder auf der Fehlerseite von `/client/pair` bei aktiver Sitzung, sauberer Start der Pairing-Datenbank bei parallelem Start, Warnung bei einem `MC_WEB_PASSWORD` über 1024 Zeichen.
- **Setup:** `bin/mc targets` liest die Gateway-`.env` nur noch ein (nie ausführen); das stillgelegte `scripts/configure.py` schreibt nicht mehr in den Checkout.
- **Prozess-Worker:** Der Supervisor behält die Bibliotheksumgebung seines Interpreters, ein Startfehler nennt eine maskierte Diagnose; ein beim Start gestorbener Supervisor gilt sofort als fehlgeschlagen, eine FIFO an einem Zustandspfad wird abgelehnt.
- **Images:** Python- und Node-Basisimages sind per Digest gepinnt, Node ist 22.23.5.
- **Release-Werkzeug:** Härtungen der Prüf- und Veröffentlichungswerkzeuge (u. a. brechen Notes über 4000 Zeichen vor der Signatur ab); ohne Wirkung auf den Betrieb.

## Hinweise für Betreiber

1. **MCP-Konsole:** Ist das Regelwerk im Image schreibgeschützt, zeigt die Konsole es nur an. Eine Ablehnen-Regel für einen einzelnen Client lässt sich durch erneute Registrierung umgehen; belastbar ist nur „Standard ablehnen“ plus Erlauben-Regeln.
2. **Proxys:** Private IPv4-Netze ab `/8`, andere IPv4-Netze ab `/24`, IPv6 ab `/48`; ein ungültiger Eintrag wird übersprungen.
3. **Setup-Skripte:** das stillgelegte `scripts/configure.py` endet mit Exit 2; `mc setup configure` verwenden.
4. **Rollback auf 2.2.9:** vorher CIDR-Einträge in `MC_WEB_TRUSTED_PROXIES` durch Einzeladressen ersetzen, sonst 426 auf der Pairing-Seite hinter dem TLS-Proxy bzw. wird der Proxy nicht als TLS-Terminator erkannt.
5. **Relay-State (Sicherheit):** Der Rückroll eines Restores braucht kein gemeinsames Dateisystem mehr. Als root senken `restore`, `key-restore` und `resolve-interrupted` auf den Besitzer eines Dienstnutzer-States ab; restaurierte Secrets gehören danach dem Dienstnutzer (0600/0644). Bei einem root-eigenen State (Standard-Gateway) ändert sich nichts.

## Installation und Update

Die Installation erfolgt über den bestehenden Gateway Update Center. Vorher RSA-Signatur, Paket-SHA256, Plattform, Image-Identitäten, Speicher und Backup prüfen. Ein Update bleibt eine bewusste Entscheidung des Betreibers.

## Rollback und Sicherheit

Das Update kann auf die vorherige Version zurückgesetzt werden; das Backup vorher prüfen. Die Signatur bleibt RSA-SHA256 mit der bisherigen Identität. OAuth-Rechte, Kunden-ACLs und Werkzeugfreigaben werden nicht automatisch erweitert.

## Kompatibilität

Die Gateway-Kits sind für Unraid und unterstützte Debian-/Ubuntu-Linux-VMs auf x86_64 bestimmt. Native Clients behalten eigene Releases; ein Gateway-Update ersetzt keinen Client-Build.
