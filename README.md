# Meilleur Commander Gateway Releases

This repository distributes binary-only Gateway and Project Worker releases for Linux hosts and Unraid. The packages include the self-hosted Gateway WebUI and its host recovery-plane helpers. They contain no source repository, credentials, customer data, or native desktop client installers.

## Current release

Gateway **2.2.12** is the current RSA-SHA256 signed Public Latest for supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts. It introduces compact upstream discovery, scoped catalog caching and timing. Installation on PROD remains an explicit owner action.

- [Gateway 2.2.12 official public release](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.12)
- [Gateway 2.2.12 release notes](docs/RELEASE-NOTES-2.2.12.md)
- [Gateway 2.2.12 SHA-256 asset inventory](docs/SHA256SUMS-2.2.12.txt)
- [Installation and upgrade](docs/INSTALLATION.md)
- [Troubleshooting](docs/FEHLERBEHEBUNG.md)
- [Security and compatibility](docs/SICHERHEIT-UND-KOMPATIBILITAET.md)

## Prepared Gateway 2.2.13

The reviewed Gateway 2.2.13 adds explicit HTTPS OAuth callbacks, improved upstream tool guidance and per-instance cache invalidation. It is not installable until its signed catalog and immutable release are published. [Release notes](docs/RELEASE-NOTES-2.2.13.md) and [SHA-256 inventory](docs/SHA256SUMS-2.2.13.txt).

## Previous release

Gateway **2.2.11** remains available at its immutable [release tag](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.11), with [release notes](docs/RELEASE-NOTES-2.2.11.md) and [SHA-256 inventory](docs/SHA256SUMS-2.2.11.txt).

## Supported Gateway packages

The Gateway release provides two separate platform kits: Linux VM (`linux-vm`, x86_64 Debian/Ubuntu hosts with Docker) and Unraid (`unraid`). The kits contain Gateway and Project Worker OCI images built from the same reviewed source. There are no Windows, macOS, or Linux desktop client packages in these Gateway releases. Native client installers and their own release channels are separate products and approvals.

When a release is public, download its immutable assets from the matching GitHub release tag and verify `SHA256SUMS` before use. Gateways with the Update Center fetch the signed catalog from this repository; installation requires an explicit owner action and uses the host recovery plane, a pre-update backup, health and identity checks, and automatic rollback on activation failure.

## Gateway 2.2.1

[Gateway 2.2.1 is publicly published, immutable, and signed](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.1). The optional MCP client remains disabled by default. The beta update catalog is at [latest.json](latest.json), with signature [latest.json.sig](latest.json.sig).

- [Binding owner release contract](CHANNEL.md)
