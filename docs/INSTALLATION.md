# Gateway installation and upgrades

These instructions cover Meilleur Commander Gateway 2.1.19 for an x86_64 Debian/Ubuntu Linux VM or an Unraid host. The Gateway release does not include desktop client packages. The 2.1.19 candidate is not publicly installable yet: isolated update/rollback QA and signed-catalog promotion are still pending. Until the catalog and release page advertise 2.1.19, continue using the latest published release, currently 2.1.18.

## Before installation

Use the kit for the actual host: `meilleur-commander-linux-vm-2.1.19.tar.gz` for the supported Linux VM platform or `meilleur-commander-unraid-2.1.19.tar.gz` for Unraid. Require x86_64, a supported Debian/Ubuntu or Unraid host, Docker access, and sufficient free space for the new images plus the pre-update backup. Do not use a kit for another platform. Do not install a candidate until its tagged GitHub release and signed catalog entry are public.

After publication, download the release assets and verify them from the same directory before installation:

```sh
sha256sum -c SHA256SUMS
```

The platform release manifest binds each kit's version, source commit, size and SHA-256, and the Gateway and Project Worker OCI digests. Keep the manifest and checksum file with the downloaded kit.

## Upgrade through the Gateway Update Center

On a supported Gateway that already has **Updates → Gateway-Updates**, open that page and wait for the signed catalog to refresh. Select the offered release and explicitly confirm **Install**. The existing host recovery plane verifies the catalog and package identity, creates a pre-update backup, stages the kit, restarts the Gateway, and checks health and release identity. If activation fails, the plane restores the previous known-good container automatically. Keep the backup and previous image until the new Gateway and Project Worker have been checked.

A new public release can take up to five minutes to appear in an already-open Update view. Do not disable signature verification, bypass the host recovery plane, or replace the running image manually to work around a missing catalog entry.

## Older installations

Installations without the Gateway Update Center need the platform-specific one-time bootstrap documented by the release that introduced the recovery plane. Follow that release's `INSTALL.md` and use only the matching, checksum-verified platform kit. The 2.1.19 candidate has not yet been approved for this path. Do not bootstrap it until its public release and signed catalog are available.

## Rollback

Use the Gateway Backup Center or the recovery plane's documented rollback procedure. Verify the previous release's health and identity after rollback. Preserve the pre-update backup and previous image until recovery is confirmed. If the Update Center reports an unknown operation outcome, inspect its recorded operation status before retrying; do not start a second update operation blindly.

