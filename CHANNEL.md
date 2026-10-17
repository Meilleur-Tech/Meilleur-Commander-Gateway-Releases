# Gateway beta update channel

This **public** repository distributes audited, distributable Meilleur Commander Gateway beta releases and the signed beta update catalog used by the Gateway Update Center (Owner decision 2026-10-17, Meilleur-Commander #1222).

## Catalog

- `latest.json` — schema `meilleur-commander-gateway-update/v2`, channel `beta`: version, tag, source SHA/tree, Gateway and Project Worker OCI digests, release notes and per-platform kit URL, SHA-256 and size.
- `latest.json.sig` — base64 RSA-SHA256 signature over the exact bytes of `latest.json`.

Gateways fetch both anonymously from `https://raw.githubusercontent.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/main/latest.json` (+ `.sig`), verify the signature with the public key shipped in their installed kit, accept only kit URLs on this repository's immutable release tag, download the kit, verify size, SHA-256 and the kit's embedded release identity, take a backup and install through their host recovery plane with automatic rollback. A catalog without a valid signature is ignored. Only versions newer than the installed one are offered.

## Release process

1. A release is built from an exact source commit of `Meilleur-Tech/Meilleur-Commander` and QA-tested.
2. Every kit is audited for secrets, private keys and installation-specific data before it is published here.
3. The GitHub pre-release with kits, manifest, `SHA256SUMS` and `INSTALL.md` is published first and verified by an anonymous download.
4. Only then are `latest.json` and `latest.json.sig` updated together in one commit.

Platform kits that fail the distribution audit are withheld (2.1.0-beta.21: Unraid kit withheld; Linux-VM kit published). Licensing/entitlement enforcement is a later, separate extension.
