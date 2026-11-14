# Gateway 2.2.1 release information

## Changes

Gateway 2.2.1 adds an optional client for registered MCP servers. It remains disabled by default; enabling and operating that feature has not been accepted for this release. Existing Gateway and Project Worker functions remain available with the feature disabled. Desktop clients retain their own independent release channels.

## Installation and update

Use the Linux VM or Unraid package matching your host. Existing installations can check the signed catalog in Update Center and explicitly confirm an update. Check free space, retain a verified backup, and verify the official SHA-256 checksums.

## Rollback

Keep the previous known-good Gateway image and backup until Gateway and Project Worker health are confirmed. If activation fails, follow the reported recovery status and verify the restored version before retrying.

## Compatibility and security

The packages support x86_64 Debian/Ubuntu Linux VMs and Unraid hosts. Catalog signatures use RSA-SHA256 and bind package hashes and image identities; signature verification must remain enabled. The source identity for this release is `00c1d1a0beb38c6878fa42c85c9f65a6e4de41ff`.
