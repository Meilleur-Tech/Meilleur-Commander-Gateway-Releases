# Meilleur Commander Gateway Releases

This repository distributes binary-only Gateway and Project Worker releases for Linux hosts and Unraid. The packages include the self-hosted Gateway WebUI and its host recovery-plane helpers. They contain no source repository, credentials, customer data, or native desktop client installers.

## Current release

Gateway **2.2.1** is the current signed public release for Linux VM and Unraid. Its optional upstream MCP client is disabled by default. Use the signed update catalog and verify downloads before installation.

- [2.2.1 release notes](docs/RELEASE-NOTES-2.2.1.md)
- [2.2.0 release notes](docs/RELEASE-NOTES-2.2.0.md)
- [2.1.19 release notes](docs/RELEASE-NOTES-2.1.19.md)
- [Installation and upgrade instructions](docs/INSTALLATION.md)
- [Troubleshooting](docs/FEHLERBEHEBUNG.md)
- [Security and compatibility](docs/SICHERHEIT-UND-KOMPATIBILITAET.md)
- [2.2.1 SHA-256 inventory](docs/SHA256SUMS-2.2.1.txt)
- [2.2.0 SHA-256 inventory](docs/SHA256SUMS-2.2.0.txt)
- [2.1.19 SHA-256 inventory](docs/SHA256SUMS-2.1.19.txt)

## Supported Gateway packages

The Gateway release provides two separate platform kits: Linux VM (`linux-vm`, x86_64 Debian/Ubuntu hosts with Docker) and Unraid (`unraid`). The kits contain Gateway and Project Worker OCI images built from the same reviewed source. There are no Windows, macOS, or Linux desktop client packages in these Gateway releases. Native client installers and their own release channels are separate products and approvals.

When a release is public, download its immutable assets from the matching GitHub release tag and verify `SHA256SUMS` before use. Gateways with the Update Center fetch the signed catalog from this repository; installation requires an explicit owner action and uses the host recovery plane, a pre-update backup, health and identity checks, and automatic rollback on activation failure.

## Gateway 2.2.1

[Gateway 2.2.1 is publicly published, immutable, and signed](https://github.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/releases/tag/v2.2.1). The optional MCP client remains disabled by default. The beta update catalog is at [latest.json](latest.json), with signature [latest.json.sig](latest.json.sig).

- [Binding owner release contract](CHANNEL.md)
