# Gateway beta update channel

This **public** repository distributes audited, distributable Meilleur Commander Gateway beta releases and the signed beta update catalog used by the Gateway Update Center (Owner decision 2026-10-17, Meilleur-Commander #1222).

## Catalog

- `latest.json` — schema `meilleur-commander-gateway-update/v2`, channel `beta`: version, tag, source SHA/tree, Gateway and Project Worker OCI digests, release notes and per-platform kit URL, SHA-256 and size.
- `latest.json.sig` — base64 RSA-SHA256 signature over the exact bytes of `latest.json`.

Gateways fetch both anonymously from `https://raw.githubusercontent.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/main/latest.json` (+ `.sig`), verify the signature with the public key shipped in their installed kit, accept only kit URLs on this repository's immutable release tag, download the kit, verify size, SHA-256 and the kit's embedded release identity, take a backup and install through their host recovery plane with automatic rollback. A catalog without a valid signature is ignored. Only versions newer than the installed one are offered.

## Release process

1. A release is built from an exact source commit of `Meilleur-Tech/Meilleur-Commander` and QA-tested.
2. Every kit is audited for secrets, private keys and installation-specific data before it is published here.
3. The versioned GitHub release (prerelease only for beta-version identifiers) with kits, manifest, `SHA256SUMS`, `INSTALL.md`, and the signed catalog pair is published first and verified by an anonymous download.
4. Only then are `latest.json` and `latest.json.sig` updated together in one commit.

Platform kits that fail the distribution audit are withheld (2.1.0-beta.21: Unraid kit withheld; from 2.1.0-beta.21.1 both kits are published). From 2.1.0-beta.23, installed gateways accept stable releases (2.1.0, 2.1.1, …) on this same signed `beta` channel; a stable sorts after its Betas and a Beta is never offered over an installed stable. Licensing/entitlement enforcement is a later, separate extension.


## OWNER Release-Fast-Path v1.2 · 14.11.2026 · gilt ab Gateway 2.2.2

**Die zusätzliche menschliche Public-Release-Freigabe zwischen bestandenem
exakten CI-/MCG- und Chris-Review und unveränderlicher Veröffentlichung
entfällt dauerhaft.** Ein bereits beauftragter Gateway-Release wird vom
einzigen vorhandenen autorisierten Release-Operator ohne neue Owner-GO-Runde
nach Main integriert, im Trusted-Workflow aus einem eingefrorenen
Release-Branch gebaut, mit dem bestehenden isolierten autorisierten
RSA-Schlüssel signiert, QA-/Backup-/Rollback-geprüft und mit den sieben
unveränderlichen binär-only-Assets sowie atomarem signierten
`latest.json`/`latest.json.sig` öffentlich veröffentlicht.

**Technische Gates entfallen nicht:** exact-head unabhängiger Review,
PR-/Main-CI, MCG-/Provenance-/R2-/Paket-Hash-/Signaturprüfung,
wahre QA-Install-/Recovery-/Rollback-Belege und anonymer HTTP-Readback
bleiben Pflicht. Der private Signierschlüssel gelangt nicht nach CI
oder GitHub. Es wird kein neues per-Version Pflicht-mTLS-/QA-Receipt-
oder Signierkonto-Ritual eingeführt. Ein späterer Code-Commit erfordert
erneute Exact-HEAD-Prüfung, aber keine neue Owner-Freigabe.

**Public ist ausdrücklich NICHT PROD.** Der Public-Publisher installiert
niemals automatisch einen Gateway, schaltet NOC-MCP nicht frei und
erteilt keinen OAuth-Consent. Jede PROD-Installation bleibt eine
ausdrückliche, getrennte Owner-Aktion über den normalen Update Center.
Für 2.2.2 ist ausdrücklich das direkte Update von bestehendem
2.2.0 auf 2.2.2 vorgesehen, ohne Zwischeninstallation von 2.2.1.

Kanonischer Owner-Beschluss: [Commander #1537](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1537),
[#1812](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1812),
[Clients #536](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/536),
[#1762](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1762).
Diese jüngere Entscheidung ersetzt ältere Sätze über ein zweites
Public-Owner-GO; die separate PROD-GO-Regel bleibt unverändert.

## Verbindlicher Owner-Standardprozess ab Gateway 2.2.1 · #1537

**Owner-Entscheidung 13.–14.11.2026:** Der einfache, bereits für 2.2.0 und 2.2.1 verwendete, signierte Public-Releaseweg ist verbindlich. Zusätzliche QA-Receipt-, mTLS-, Invoker-, Service- oder Schlüssel-Provisionierung pro Gateway-Version ist **keine** Standard-Releasevoraussetzung. Der receipt-gebundene `gateway-release-promote.py`-Finalizer ist ein gesonderter Optionalpfad, **nicht** der Pflichtweg. Die notwendige bestehende Signatur, Integritätskontrolle, Autorisierung, Review/CI, QA und Wiederherstellung bleiben unverändert.

**Wiederholbarer Ablauf für 2.2.2 und Folgeversionen:**

1. **Einen einzigen eingefrorenen Source-Commit** mit exact-head Review/CI und echten QA-Install-/Health-/Recovery-Belegen aus dem bereits beauftragten Release verwenden. Unveränderte, auditierte Unraid- und Linux-VM-Kits plus Plattformmanifest, öffentliche Anleitung, Release Notes und Prüfsummen vorbereiten. Keine nachträglichen Rebuilds oder veränderten Kits. `SHA256SUMS` führt `INSTALL.md`, Plattformmanifest und beide Kits auf.
2. Aus dem vorhandenen Plattformmanifest das kanonische `latest.json` im Schema `meilleur-commander-gateway-update/v2` für Kanal `beta` erzeugen. Source SHA, OCI-Digests, Paketnamen, Byte-Längen, SHA-256, Release-URLs und `MCP default OFF` (solange nicht gesondert abgenommen) auf Übereinstimmung prüfen. Der schon vorhandene `scripts/gateway-release-catalog.py build` ist der Standardgenerator; bei bereits geprüftem und unverändertem Katalog darf exakt dieser Bytebestand signiert werden.
3. **Nur auf einem bereits autorisierten Owner-Signiergerät** den vorhandenen privaten Gateway-RSA-Schlüssel für **RSA-SHA256 über die exakten `latest.json`-Bytes** verwenden. Kein privater Schlüssel in Git, CI, Logs, Übergabedateien oder auf dem Publisher. Bei getrenntem Signier- und Publisher-Gerät nur die nicht geheime Katalogdatei zum Signiergerät und die fertige base64-kodierte Signatur zurück übertragen. Vorher die öffentliche SPKI-Identität des Schlüssels mit `scripts/gateway-release-public-key.spki` (gepinnter DER-SPKI-SHA-256) vergleichen. Danach `gateway-release-catalog.py verify --catalog latest.json --public-key <PINNED-PUBLIC-KEY>` erfolgreich ausführen. **Niemals** einen falschen Receipt erzeugen oder die Verifikation abschalten.
4. Über die vorhandene autorisierte GitHub-Owner-Identität `gh release create vX.Y.Z --draft` mit **allen sieben Assets** ausführen: beide unveränderten Kits, Plattformmanifest, `INSTALL.md`, `SHA256SUMS`, `latest.json`, `latest.json.sig`. Die exakten lokalen SHA-256 und Größen gegen GitHubs Asset-`digest` und `size` vergleichen. Anschließend den Draft veröffentlichen, `immutable: true`, Versions-Tag und anonym erreichbare Downloads unabhängig prüfen. Nur dann gilt der Binary-Release als öffentlich.
5. **Erst danach** `main/latest.json` **und** `main/latest.json.sig` über **einen einzigen Git-Tree-/Commit-/Ref-Update-Vorgang** atomar aktualisieren. Ausgangs-`main`-SHA vor dem Fast-Forward abgleichen; niemals die beiden Dateien in getrennten Contents-API-Commits ersetzen. Wird `main` zwischenzeitlich verändert, auf neuem Head neu ansetzen, ohne den signierten Katalog zu verändern. Nach Promotion beide Raw-Dateien anonym neu abrufen, exakte Bytes vergleichen und die Signatur mit dem Pin verifizieren. `/releases/latest` muss auf das immutable neue Release zeigen.
6. **PROD ist getrennt:** Die Veröffentlichung löst kein PROD-Deployment aus. Erst separates Owner-GO und der reguläre Gateway-Update-Center-Knopf erlauben die Installation mit Backup, Health-/Identitätsprüfung und rollbackfähigem Recovery-Plane-Pfad. Native Clients haben unabhängige Releasekanäle.

**Reale Wiederverwendungsbelege:** 2.2.0 Public `v2.2.0` vom 13.11.2026, atomarer Katalogcommit `9ae88cd372640e5b401d23b0db639ebc18d86c47`; 2.2.1 Public `v2.2.1` vom 14.11.2026, Source `00c1d1a0beb38c6878fa42c85c9f65a6e4de41ff`, atomarer Katalogcommit `ec5be369e6ed4dd908d2cc32eb4e37c259467f1c`. 2.2.1 wurde signiert und mit der vorhandenen öffentlichen Gateway-Schlüsselidentität unabhängig verifiziert; es benötigte keine neue Signatur- oder QA-Receipt-Infrastruktur.
