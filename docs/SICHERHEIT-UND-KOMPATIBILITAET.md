# Gateway security and compatibility

Fabric Commander Gateway 2.2.6 is a Linux-hosted Gateway and Project Worker release for x86_64 Debian/Ubuntu VMs and Unraid. This repository distributes binary-only platform kits, not the Commander source tree or native desktop clients.

## Release verification

The Gateway Update Center accepts a release only through the RSA-SHA256 signed catalog and its pinned public key. The catalog binds version, source commit/tree, Gateway and Project Worker OCI digests, and each platform kit's immutable URL, byte size, and SHA-256. The installer verifies the kit and embedded release identity before staging. Keep these checks enabled. A valid checksum alone does not replace catalog-signature or source-identity verification.

The 2.1.19 release was built from source commit `d6ba42010be0cf511db9c16070cb18a9cc302ed5` and tree `895da6d0f3dc72906fba78ede367818c3941c446`. Its two platform kits passed package verification and recursive binary/secret audit. Isolated clone update, Gateway/WebUI health, and automatic rollback passed. The published beta catalog is signed with the pinned release key.

## Platform and client boundaries

The supported Gateway kits are Linux VM and Unraid. Windows, macOS, ARM64 hosts, and Linux desktop client installation are not included in this Gateway release. The Gateway source supports separate signed Linux client release channels, but no native client binaries are distributed here. Linux client migration and updates follow their own release process. Do not infer client compatibility from Gateway health alone.

The Gateway updater creates a pre-update backup and retains the previous known-good image for recovery. Updates require owner confirmation through the Update Center; there is no automatic public-channel installation. Never place secrets or customer data in this public repository or its release assets.


## Gateway 2.2.1

These instructions also apply to Gateway 2.2.1 on supported Linux VM and Unraid hosts. The optional MCP client remains disabled by default; leave the existing signature and backup checks enabled.

## Gateway 2.2.2 security and compatibility

Gateway 2.2.2 is an x86_64 Linux VM and Unraid Gateway + Project Worker
package. The optional NOC & Control upstream OAuth integration requires
separate owner activation, explicit consent, PKCE S256 and suitable scope.
It remains OFF by default and does not grant Control access by installation.
Frozen binary-only Gateway kits retain explicit original SHA-256 and OCI
identities, while the update manifest requires the existing RSA-SHA256
signed catalog with its pinned public key. Installed QA recovery and PROD
acceptance must be proven separately from successful source/audit tests.


## Gateway 2.2.4

Gateway 2.2.4 is for x86_64 Unraid and supported Linux VM hosts. The signed catalog is RSA-SHA256 verified with the existing pinned Gateway key. New MCP providers, OAuth scopes and approved tool schemas remain opt-in, with provider permissions and identity checks enforced separately.

## Gateway 2.2.5 security and compatibility

Gateway 2.2.5 supports x86_64 Debian/Ubuntu Linux VM and Unraid installation kits, with the Gateway and Project Worker tied to one source SHA. Pinned RSA-SHA256 catalog signatures and source/package SHA-256 integrity remain mandatory. The optional universal MCP client uses explicit owner consent, TLS hostname checks and authorized IP pinning against DNS rebinding. Native desktop clients are not part of this public Gateway release.

## Gateway 2.2.6 authorization and binary identity

The optional provider-neutral MCP integration uses explicit human consent and OAuth PKCE S256. Permissions derive from verified provider/resource discovery, but activation requires an actual token grant, current provider tool list and the site's own access control. `inventory:read` alone must not authorize monitoring; monitoring tools are read-only and existing safeguards reject mutating scopes and untrusted schemas. The release preserves the registered RSA-SHA256 public update signature and SHA-256 digests, without introducing a new signing identity or any dependency on native client upgrades. Publishing a release never installs it on PROD automatically.

## Gateway 2.2.8 RSA bridge and compatibility

Gateway **2.2.8** keeps the existing pinned RSA-SHA256 v2 catalog verification compatible with installations on supported x86_64 Linux VMs and Unraid. The reviewed source commit is `851e57674a68201f5aa507522cb15f1e3907d6df`. The signing candidate binds the original trusted OCI digests, immutable platform-manifest checksum, two package SHA-256 values and a separately signed six-check isolated QA receipt. This prevents mixing older QA evidence with a newer build.

Future Sigstore/Cosign OIDC verification remains preparatory and is not an active trust fallback in this release. Gateway MCP OAuth rights for NOC and Lexit Apps still require individual user consent, explicit scopes, verified provider metadata and site ACL. Native Windows/macOS/Linux desktop client releases are separately signed and not contained in the Gateway packages. Always preserve rollback data and confirm live health; publishing is not a PROD update.

## Gateway 2.2.9 authorization, update and compatibility

Gateway **2.2.9** keeps the existing pinned RSA-SHA256 v2 catalog verification compatible with installations on supported x86_64 Linux VMs and Unraid. The reviewed source commit is `5fdbdb2f3148d4bfee326b4f64f1e228ddd3ed55`. The signing candidate binds the original trusted OCI digests, the immutable platform-manifest checksum, two package SHA-256 values and a separately signed six-check isolated QA receipt, so older QA evidence cannot be mixed with a newer build.

Outbound MCP OAuth connections keep their access-token expiry in the encrypted store and use the previously approved refresh token instead of reusing an expired token; scope, issuer and resource checks and token revocation are unchanged. The refresh is covered by tests, without a live provider session. The new MCP policy lets operators allow or deny tools per client; tool schema changes are held until approved again. No new signing identity is introduced, and OAuth rights, customer ACLs and tool approvals are not widened automatically. Native Windows/macOS/Linux desktop client releases are separately signed and not contained in the Gateway packages. Always preserve rollback data and confirm live health; publishing is not a production update.

## Gateway 2.2.10 authorization, update and compatibility

Gateway **2.2.10** keeps the existing pinned RSA-SHA256 v2 catalog verification compatible with installations on supported x86_64 Linux VMs and Unraid. The reviewed source commit is `fe102ba6e61eaf6eebb5cc6c4449726e7bcf6be8`. The signing candidate binds the original trusted OCI digests, the immutable platform-manifest checksum, two package SHA-256 values and a separately signed six-check isolated QA receipt, so older QA evidence cannot be mixed with a newer build; the process start of the Project Worker was verified by hand on the QA host.

The MCP console and the Server tab are a preview and do not widen access: OAuth rights, customer ACLs and tool approvals are not extended automatically. `MC_WEB_TRUSTED_PROXIES` accepts CIDR networks (too wide networks are ignored and logged once). The rollback of a relay-state restore no longer needs a shared file system, and copies are removed only after `fsync`. No new signing identity is introduced. Native Windows/macOS/Linux desktop client releases are separately signed and not contained in the Gateway packages. Always preserve rollback data and confirm live health; publishing is not a production update.
