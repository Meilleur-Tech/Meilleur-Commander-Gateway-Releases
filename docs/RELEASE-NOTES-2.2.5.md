# Fabric Commander Gateway 2.2.5 release notes

## Changes and improvements

Gateway 2.2.5 extends the optional, provider-neutral upstream MCP integration. Compatible MCP servers can be registered without requiring any specific network controller, Lexit installation or Unraid host. The administrator configures OAuth authorization and consent separately; the feature remains OFF until explicitly enabled.

The Gateway update-status response now reports the running runtime version and its verified source identity separately from any older cached update-check result. This avoids presenting an outdated cached version as the active installation.

## Installation and update

Use the immutable binary-only x86_64 Debian/Ubuntu Linux VM or Unraid kit that matches your host. Both kits include the Gateway and matching Project Worker generated from the frozen source. Existing installations use the authenticated signed beta channel in the Gateway Update Center and explicitly confirm the update.

## Rollback and recovery

Keep the previous known-good Gateway image and a pre-update backup until Gateway health, MCP endpoint and Project Worker identity have been checked. The existing host recovery plane checks the new candidate and automatically restores the last known-good image if an activation fails. The public release itself never installs or updates PROD automatically.

## Compatibility and security

The release uses the existing pinned RSA-SHA256 update catalog signature and per-platform SHA-256 hashes. Optional upstream MCP connections keep HTTPS hostname verification and OAuth PKCE S256; private-name or DNS-changing targets require the authorized IP bound to operator consent. An administrator may provide an optional additional local public CA root, but no signing private keys, account passwords or provider-specific certificates are included in the kits.

An installation does not by itself grant any access to a third-party server; a personal consent and authorized tool-call acceptance must be tested separately for each enabled provider. Native Windows, macOS and Linux clients have their own independent release channels.

Frozen Gateway source SHA: ad7b313c5d4a9a3021fa6de51c13d15f3fd510a2.
