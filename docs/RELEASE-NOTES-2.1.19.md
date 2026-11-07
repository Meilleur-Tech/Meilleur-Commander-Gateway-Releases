# Meilleur Commander Gateway 2.1.19

**Availability:** 2.1.19 is the latest public Gateway release and is listed in the signed `beta` update catalog.

## Included changes

Gateway 2.1.19 adds server-side support for four separately signed Linux client release channels: x86_64 GUI (`linux`), x86_64 headless (`linux-headless`), ARM64 GUI (`linux-arm64`), and ARM64 headless (`linux-arm64-headless`). New enrollment assigns an explicit matching channel; malformed variants are rejected before a pairing code is consumed. Release activation and public discovery bind the RSA-signed manifest and ZIP asset identity to the assigned channel. Headless and ARM64 variants do not fall back to a GUI or different architecture.

This Gateway release contains no native client installer or source code. Publication of a Linux client and activation of its Gateway channel remain separate approvals. Existing paired Linux 2.2.2 clients without an update source do not migrate automatically. The 2.2.3 client packages mentioned in the engineering work are QA prereleases, not part of these Gateway assets. No client OTA or existing-device migration acceptance is claimed here; that work remains in its separate lane.

The Update Center also now preserves the five canonical client update states and bounded check timestamps through redaction, persistence and reload, and exposes all four Linux source channels. A typed client check is treated as positive only when the HTTP response and completed `check` operation agree; invalid or incomplete evidence does not mark a client current. Existing offline, compatibility, pending-operation and recovery priorities remain in force.

The Gateway and Project Worker images are built as a pair from the same reviewed source commit. No additional Gateway runtime feature or compatibility guarantee is claimed beyond the changes listed above.

## Package identity

- Source commit: `d6ba42010be0cf511db9c16070cb18a9cc302ed5`
- Source tree: `895da6d0f3dc72906fba78ede367818c3941c446`
- Gateway OCI: `sha256:6fe2f7b3850e992b77dbc91bd84dc35375599f09494fbdedd2337be83831826f`
- Project Worker OCI: `sha256:7af2a2267cb221f34836df4532b77f70680c5176a55c49934ddc620246726284`
- Private R2 manifest SHA-256: `1633285ea1afbec2632e5f45b0ec86c626b129df3a5677f5900981e817c220ab`
- Exact-head release CI: [42278640163](https://github.com/Meilleur-Tech/Meilleur-Commander/actions/runs/42278640163); Connector checks: [42278640149](https://github.com/Meilleur-Tech/Meilleur-Commander/actions/runs/42278640149); provenance: [42281965836](https://github.com/Meilleur-Tech/Meilleur-Commander/actions/runs/42281965836).
- Independent exact-head approval: [ChristopherZender review 5806054195](https://github.com/Meilleur-Tech/Meilleur-Commander/pull/1760#pullrequestreview-5806054195).
- Trusted artifact build run: [42283755540](https://github.com/Meilleur-Tech/Meilleur-Commander/actions/runs/42283755540).
- Release PR: [#1760, exact head `d6ba42010be0cf511db9c16070cb18a9cc302ed5`](https://github.com/Meilleur-Tech/Meilleur-Commander/pull/1760)

The read-only R2 readback independently verified all eight original objects and their provenance. The Unraid and Linux VM kits were created from those verified OCI objects; both passed `release-kits.py verify` and the recursive public binary/secret audit. These package checks do not substitute for live QA.

## Installation and recovery

Supported installations use **Updates → Gateway-Updates** and explicitly confirm **Install**. The host recovery plane verifies the signature and package identity, makes a pre-update backup, stages the kit, checks health and release identity, and automatically rolls back on activation failure. Keep the prior image and backup until the new Gateway and Worker are verified.

## Verification status

- Trusted build, original R2 objects, both package identities, and both recursive binary/secret audits: **PASS**.
- Isolated Unraid clone update to 2.1.19, Gateway and WebUI health, immutable Gateway/Worker image identity, and automatic rollback to the 2.1.1 known-good image after an injected QA-only health failure: **PASS**.
- Public binary-only release and anonymous GET/SHA-256 verification of all seven release assets: **PASS**.
- Signed `beta` catalog: **PASS**; signature verified with the pinned public key after publication.
- Production rollout is separate from this public release and is not claimed here.

