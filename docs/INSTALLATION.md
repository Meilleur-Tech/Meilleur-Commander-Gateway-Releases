# Gateway installation and upgrades

These instructions cover Fabric Commander Gateway 2.2.6 for an x86_64 Debian/Ubuntu Linux VM or an Unraid host (with earlier 2.2.x behaviour retained where compatible). The Gateway release does not include desktop client packages.

## Before installation

Use the kit for the actual host: `meilleur-commander-linux-vm-2.2.6.tar.gz` for the supported Linux VM platform or `meilleur-commander-unraid-2.2.6.tar.gz` for Unraid. Require x86_64, a supported Debian/Ubuntu or Unraid host, Docker access, and sufficient free space for the new images plus the pre-update backup. Do not use a kit for another platform.

After publication, download the release assets and verify them from the same directory before installation:

```sh
sha256sum -c SHA256SUMS
```

The platform release manifest binds each kit's version, source commit, size and SHA-256, and the Gateway and Project Worker OCI digests. Keep the manifest and checksum file with the downloaded kit.

## Upgrade through the Gateway Update Center

On a supported Gateway that already has **Updates → Gateway-Updates**, open that page and wait for the signed catalog to refresh. Select the offered release and explicitly confirm **Install**. The existing host recovery plane verifies the catalog and package identity, creates a pre-update backup, stages the kit, restarts the Gateway, and checks health and release identity. If activation fails, the plane restores the previous known-good container automatically. Keep the backup and previous image until the new Gateway and Project Worker have been checked.

A new public release can take up to five minutes to appear in an already-open Update view. Do not disable signature verification, bypass the host recovery plane, or replace the running image manually to work around a missing catalog entry.

## Older installations

Installations without the Gateway Update Center need the platform-specific one-time bootstrap documented by the release that introduced the recovery plane. Follow that release's `INSTALL.md` and use only the matching, checksum-verified platform kit.

## Rollback

Use the Gateway Backup Center or the recovery plane's documented rollback procedure. Verify the previous release's health and identity after rollback. Preserve the pre-update backup and previous image until recovery is confirmed. If the Update Center reports an unknown operation outcome, inspect its recorded operation status before retrying; do not start a second update operation blindly.


## Gateway 2.2.1

These instructions also apply to Gateway 2.2.1 on supported Linux VM and Unraid hosts. The optional MCP client remains disabled by default; leave the existing signature and backup checks enabled.

## Gateway 2.2.2 publication preparation

Gateway 2.2.2 supports the matching x86_64 Unraid or Debian/Ubuntu Linux VM
kit. Only use the official signed beta channel after it actually offers
version 2.2.2, not merely after this documentation appears. A direct update
from Gateway 2.2.0 to 2.2.2 is intended without installing 2.2.1 first.
Verify signature, package SHA-256 and OCI identity, free disk space, pre-update
backup, installed health, and the recovery plane rollback state. The owner
must explicitly press the Update Center Install button for PROD.


## Gateway 2.2.4

Gateway 2.2.4 for x86_64 Unraid and Linux VM must be installed from the verified signed Public Beta Update Center only. Confirm the previous healthy release, current pre-update backup, exact package SHA-256, and recovery-plane rollback before updating.

## Gateway 2.2.5 installation and update

For Gateway 2.2.5, use the supported x86_64 Debian/Ubuntu Linux VM or Unraid kit. Verify the RSA-SHA256 signature of the beta channel and matching SHA-256 kit, keep a working backup and confirm installation using the normal Gateway Update Center. The optional universal MCP connection is OFF by default and needs explicit administrator consent. PROD is never installed merely because the public release has appeared.

## Gateway 2.2.6 OAuth consent

After installing Gateway 2.2.6, the optional upstream MCP Wizard discovers the permissions genuinely advertised by the provider. Select `monitor:read` only when needed and complete the new provider OAuth consent. Existing `inventory:read` tokens do not silently gain monitoring access. The normal signed Update Center is the recommended installation path, and customer PROD activation is always explicit.

## Gateway 2.2.8 signed update and installation

For the supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts, version **2.2.8** is installed only after the public beta catalog contains its valid pinned RSA-SHA256 signature, matching immutable kit SHA-256 and Gateway/Project Worker identities. The Linux-VM kit is `meilleur-commander-linux-vm-2.2.8.tar.gz`; the Unraid kit is `meilleur-commander-unraid-2.2.8.tar.gz`.

Keep the original pre-update backup and the known-good 2.2.7 or 2.2.6 container until successful postcheck. The 2.2.8 recovery plane has passed isolated fault-injection automatic rollback and in-flight Docker restart/resume. A status of `outcome_unknown` still means stop, investigate and reconcile before retrying. Use the existing Update Center, never an unsigned OCI image. A public release does not trigger PROD activation automatically.

## Gateway 2.2.9 signed update and installation

For the supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts, version **2.2.9** is installed only after the public beta catalog contains its valid pinned RSA-SHA256 signature, matching immutable kit SHA-256 and Gateway/Project Worker identities. The Linux-VM kit is `meilleur-commander-linux-vm-2.2.9.tar.gz`; the Unraid kit is `meilleur-commander-unraid-2.2.9.tar.gz`.

Keep the original pre-update backup and the known-good previous container until successful postcheck. Before updating, read the operator notes in the [2.2.9 release notes](RELEASE-NOTES-2.2.9.md): the first start creates the MCP policy store with the default `allow`, new or changed WebUI passwords are limited to 256 characters, and a redirecting `gateway_url` must be replaced by its final HTTPS address. The update plan refuses downgrades. Use the existing Update Center, never an unsigned OCI image; a public release does not trigger production activation automatically.

## Gateway 2.2.10 signed update and installation

For the supported x86_64 Debian/Ubuntu Linux VM and Unraid hosts, version **2.2.10** is installed only after the public beta catalog contains its valid pinned RSA-SHA256 signature, matching immutable kit SHA-256 and Gateway/Project Worker identities. The Linux-VM kit is `meilleur-commander-linux-vm-2.2.10.tar.gz`; the Unraid kit is `meilleur-commander-unraid-2.2.10.tar.gz`. The [SHA-256 inventory](SHA256SUMS-2.2.10.txt) lists both kits, the platform manifest and `INSTALL.md`.

Keep the original pre-update backup and the known-good previous container until successful postcheck. Before updating, read the operator notes in the [2.2.10 release notes](RELEASE-NOTES-2.2.10.md): the MCP console is a preview, a read-only policy in the image is shown but not editable, and before a rollback to 2.2.9 any CIDR entry in `MC_WEB_TRUSTED_PROXIES` must be replaced by single addresses. The update plan refuses downgrades. Use the existing Update Center, never an unsigned OCI image; a public release does not trigger production activation automatically.

## Gateway 2.2.11 signed update and installation

For supported x86_64 Debian/Ubuntu Linux VMs and Unraid, **2.2.11** is installable only when the official signed `latest.json` has been published, its RSA-SHA256 signature verifies against the pinned key, and the platform kit/Project Worker identities match. The [2.2.11 SHA-256 inventory](SHA256SUMS-2.2.11.txt) includes `INSTALL.md`, the platform-release manifest and the unchanged original `meilleur-commander-linux-vm-2.2.11.tar.gz` and `meilleur-commander-unraid-2.2.11.tar.gz` kits.

Use **Updates → Gateway-Updates**, retain the pre-update backup and previous known-good container, and confirm the update explicitly. Do not copy Docker images over a running Gateway or bypass catalog checks. Hermes owner-internal scope remains disabled until its fingerprint is activated separately; the publication itself cannot change PROD.
