# Meilleur Commander Gateway Releases

This repository distributes binary-only Gateway and Project Worker releases for Linux hosts and Unraid. The packages include the self-hosted Gateway WebUI and its host recovery-plane helpers. They contain no source repository, credentials, customer data, or native desktop client installers.

## Current release

Gateway **2.2.7** is the current RSA-SHA256 signed Public Latest for supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts. The immutable Gateway and matching Project Worker passed source/review checks, trusted build and independent R2 readback, isolated QA install, Gateway/WebUI/HTTPS and worker identity checks, and recursive binary-only package audits. Monitoring through an optional MCP provider still requires explicit provider OAuth consent and site/building permissions; no new access is granted by updating.

The signed Gateway Update Center offers the binary kits on the beta channel; **installation on PROD is a separate, explicit owner action**, never performed automatically by publishing this release.

- [Gateway 2.2.7 official public release](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.7)
- Gateway 2.2.7 immutable release contains its own SHA-256 asset inventory.
- [Installation and upgrade](docs/INSTALLATION.md)
- [Troubleshooting](docs/FEHLERBEHEBUNG.md)
- [Security and compatibility](docs/SICHERHEIT-UND-KOMPATIBILITAET.md)

## Previous release

Gateway **2.2.6** remains available at its immutable [release tag](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.6), with [release notes](docs/RELEASE-NOTES-2.2.6.md) and [SHA-256 inventory](docs/SHA256SUMS-2.2.6.txt). The update catalog now selects 2.2.7 for a consenting owner, without modifying existing PROD installations.

## Supported Gateway packages

The Gateway release provides two separate platform kits: Linux VM (`linux-vm`, x86_64 Debian/Ubuntu hosts with Docker) and Unraid (`unraid`). The kits contain Gateway and Project Worker OCI images built from the same reviewed source. There are no Windows, macOS, or Linux desktop client packages in these Gateway releases. Native client installers and their own release channels are separate products and approvals.

When a release is public, download its immutable assets from the matching GitHub release tag and verify `SHA256SUMS` before use. Gateways with the Update Center fetch the signed catalog from this repository; installation requires an explicit owner action and uses the host recovery plane, a pre-update backup, health and identity checks, and automatic rollback on activation failure.

## Gateway 2.2.1

[Gateway 2.2.1 is publicly published, immutable, and signed](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.1). The optional MCP client remains disabled by default. The beta update catalog is at [latest.json](latest.json), with signature [latest.json.sig](latest.json.sig).

- [Binding owner release contract](CHANNEL.md)

## Prepared Gateway 2.2.8

Gateway **2.2.8** is prepared from the reviewed source commit `851e57674a68201f5aa507522cb15f1e3907d6df`. Its original Trusted Build, isolated six-check QA, automatic image rollback, live in-flight restart/resume, signed QA receipt and two audited binary-only kits have been independently verified.

- [Gateway 2.2.8 release notes](docs/RELEASE-NOTES-2.2.8.md)
- [Gateway 2.2.8 asset SHA-256 inventory](docs/SHA256SUMS-2.2.8.txt)

Documentation preparation is not public-update authorization. Customers may install this version only **after** the immutable v2.2.8 release has been published and the pinned RSA-SHA256 signature on the distribution `latest.json` has been verified. Publishing never installs on owner PROD.

## Prepared Gateway 2.2.9

Gateway **2.2.9** is prepared from the reviewed source commit `5fdbdb2f3148d4bfee326b4f64f1e228ddd3ed55`. Its original Trusted Build, isolated six-check QA, automatic rollback, resume after a restart, signed QA receipt and two audited binary-only kits have been independently verified.

- [Gateway 2.2.9 release notes](docs/RELEASE-NOTES-2.2.9.md)
- [Gateway 2.2.9 asset SHA-256 inventory](docs/SHA256SUMS-2.2.9.txt)

Documentation preparation is not public-update authorization. Customers may install this version only **after** the immutable v2.2.9 release has been published and the pinned RSA-SHA256 signature on the distribution `latest.json` has been verified. Publishing never installs on a production system.
