# Gateway beta update channel

This **public** repository distributes the Meilleur Commander Gateway's explicitly released, **public-distribution-approved** binaries and a credential-free beta update manifest. This channel is intended for the transition to a Control Plane managed update service.

## Stable manifest URL
`https://raw.githubusercontent.com/Meilleur-Tech/Meilleur-Commander-Gateway-Releases/main/latest.json`

This URL is **not** GitHub's `/releases/latest`: GitHub generally excludes prereleases from that endpoint, and the `2.1.0-beta.*` lane consists of prereleases.

## Safety and release contract
- `latest.json` starts as `unpublished`: **do not update** when no release exists.
- Before updating, validate schema, channel, semver, HTTPS destination, exact GitHub release/tag, SHA256, and provenance. Never run arbitrary shell instructions from a remote manifest.
- Choose only explicitly supported artifacts for the current deployment flavor and architecture.
- Download to a temporary location; verify the entire downloaded file against its SHA256 checksum and the signed/verified release provenance, then use the existing preflight, backup, health, and rollback flows.
- Owner/internal assets, credentials, tokens, entitlement secrets, signing private keys, and unrestricted admin builds must **never** be published.
- Releasing beta19.1 requires a separate approved distributable build and successful isolated QA; this repository alone does **not** enable production auto-updates.
- Longer term, move manifest discovery, entitlements and trust policy to the Control Plane.

Maintainers must update the manifest **only after** the release is actually published and the checksum and source identity are checked. The manifest should reference immutable versioned release assets rather than mutable `latest` asset names.
