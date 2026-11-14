# Gateway security and compatibility

Meilleur Commander Gateway 2.2.0 is a Linux-hosted Gateway and Project Worker release for x86_64 Debian/Ubuntu VMs and Unraid. This repository distributes binary-only platform kits, not the Commander source tree or native desktop clients.

## Release verification

The Gateway Update Center accepts a release only through the RSA-SHA256 signed catalog and its pinned public key. The catalog binds version, source commit/tree, Gateway and Project Worker OCI digests, and each platform kit's immutable URL, byte size, and SHA-256. The installer verifies the kit and embedded release identity before staging. Keep these checks enabled. A valid checksum alone does not replace catalog-signature or source-identity verification.

The 2.1.19 release was built from source commit `d6ba42010be0cf511db9c16070cb18a9cc302ed5` and tree `895da6d0f3dc72906fba78ede367818c3941c446`. Its two platform kits passed package verification and recursive binary/secret audit. Isolated clone update, Gateway/WebUI health, and automatic rollback passed. The published beta catalog is signed with the pinned release key.

## Platform and client boundaries

The supported Gateway kits are Linux VM and Unraid. Windows, macOS, ARM64 hosts, and Linux desktop client installation are not included in this Gateway release. The Gateway source supports separate signed Linux client release channels, but no native client binaries are distributed here. Linux client migration and updates follow their own release process. Do not infer client compatibility from Gateway health alone.

The Gateway updater creates a pre-update backup and retains the previous known-good image for recovery. Updates require owner confirmation through the Update Center; there is no automatic public-channel installation. Never place secrets or customer data in this public repository or its release assets.


## Gateway 2.2.1

These instructions also apply to Gateway 2.2.1 on supported Linux VM and Unraid hosts. The optional MCP client remains disabled by default; leave the existing signature and backup checks enabled.
