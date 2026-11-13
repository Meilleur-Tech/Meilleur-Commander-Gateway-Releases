# Gateway 2.2.0 release information

## Changes

Gateway 2.2.0 includes an update progress display and a compact client version selection in the Update Center. Gateway and Project Worker are distributed together in platform-specific packages. Native desktop clients have separate release channels.

## Installation and update

Choose the Linux VM or Unraid kit for the target host. Existing compatible installations can check the signed update catalog in the Gateway Update Center and explicitly confirm the update. Ensure adequate free space and retain the verified pre-update backup. Verify downloaded packages with `SHA256SUMS` and use only the matching platform kit.

## Rollback

Keep the previous known-good image and backup until the new Gateway and Project Worker are healthy. If activation fails, follow the update status and existing recovery or rollback procedure. Confirm the previous version and health before retrying.

## Compatibility and security

The supported kits target x86_64 Debian/Ubuntu Linux VMs or Unraid hosts. Gateway catalog verification uses RSA-SHA256, and package identity includes SHA-256 hashes and sizes. Do not disable signature verification. Client releases remain independent of Gateway publication.

The immutable source identifier for this release is `97464797a3a1e45dd1991854967747f49c8b544c`.
