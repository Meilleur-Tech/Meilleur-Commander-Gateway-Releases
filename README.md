# Meilleur Commander Gateway Releases

This repository distributes binary-only Gateway and Project Worker releases for Linux hosts and Unraid. The packages include the self-hosted Gateway WebUI and its host recovery-plane helpers. They contain no source repository, credentials, customer data, or native desktop client installers.

## Gateway 2.2.6 release candidate documentation

The frozen and successfully tested Gateway **2.2.6** candidate is prepared for the signed beta channel. This documentation is published ahead of the immutable release and does not indicate that 2.2.6 is already installed on any customer's PROD host. For live update availability rely on the RSA-SHA256 signed `latest.json` catalog.

- [Gateway 2.2.6 release notes](docs/RELEASE-NOTES-2.2.6.md)
- [Gateway 2.2.6 SHA-256 kit inventory](docs/SHA256SUMS-2.2.6.txt)

## Current release

Gateway **2.2.5** is the current signed Public Latest for supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts. The immutable Gateway and Project Worker images passed package verification, isolated QA install, health, recovery to the previous version and re-installation. The public update is offered through the signed Gateway Update Center; installation on PROD remains a separate, explicit owner action.

- [Gateway 2.2.5 release notes](docs/RELEASE-NOTES-2.2.5.md)
- [Gateway 2.2.5 SHA-256 kit inventory](docs/SHA256SUMS-2.2.5.txt)
- [Installation and upgrade](docs/INSTALLATION.md)
- [Troubleshooting](docs/FEHLERBEHEBUNG.md)
- [Security and compatibility](docs/SICHERHEIT-UND-KOMPATIBILITAET.md)

## Supported Gateway packages

The Gateway release provides two separate platform kits: Linux VM (`linux-vm`, x86_64 Debian/Ubuntu hosts with Docker) and Unraid (`unraid`). The kits contain Gateway and Project Worker OCI images built from the same reviewed source. There are no Windows, macOS, or Linux desktop client packages in these Gateway releases. Native client installers and their own release channels are separate products and approvals.

When a release is public, download its immutable assets from the matching GitHub release tag and verify `SHA256SUMS` before use. Gateways with the Update Center fetch the signed catalog from this repository; installation requires an explicit owner action and uses the host recovery plane, a pre-update backup, health and identity checks, and automatic rollback on activation failure.

## Gateway 2.2.1

[Gateway 2.2.1 is publicly published, immutable, and signed](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.1). The optional MCP client remains disabled by default. The beta update catalog is at [latest.json](latest.json), with signature [latest.json.sig](latest.json.sig).

- [Binding owner release contract](CHANNEL.md)
