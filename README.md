# Meilleur Commander Gateway Releases

This repository distributes binary-only Gateway and Project Worker releases for Linux hosts and Unraid. The packages include the self-hosted Gateway WebUI and its host recovery-plane helpers. They contain no source repository, credentials, customer data, or native desktop client installers.

## Current release

The latest public Gateway release remains **2.1.18** until a later version has passed isolated QA and its signed update catalog has been promoted. The audited **2.1.19** release candidate is being prepared; it is not available to install yet. Its release notes, package hashes, and installation guidance are published for review, but no 2.1.19 public download or update-catalog entry exists until release approval.

- [2.1.19 release notes and gate status](docs/RELEASE-NOTES-2.1.19.md)
- [Installation and upgrade instructions](docs/INSTALLATION.md)
- [Troubleshooting](docs/FEHLERBEHEBUNG.md)
- [Security and compatibility](docs/SICHERHEIT-UND-KOMPATIBILITAET.md)
- [2.1.19 SHA-256 inventory](docs/SHA256SUMS-2.1.19.txt)

## Supported Gateway packages

The Gateway release provides two separate platform kits: Linux VM (`linux-vm`, x86_64 Debian/Ubuntu hosts with Docker) and Unraid (`unraid`). The kits contain Gateway and Project Worker OCI images built from the same reviewed source. There are no Windows, macOS, or Linux desktop client packages in these Gateway releases. Native client installers and their own release channels are separate products and approvals.

When a release is public, download its immutable assets from the matching GitHub release tag and verify `SHA256SUMS` before use. Gateways with the Update Center fetch the signed catalog from this repository; installation requires an explicit owner action and uses the host recovery plane, a pre-update backup, health and identity checks, and automatic rollback on activation failure.
