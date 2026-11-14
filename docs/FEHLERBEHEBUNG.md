# Gateway troubleshooting

This guide covers the Linux VM and Unraid Gateway kits, including versions 2.1.19 and 2.2.0. Use only steps that match the platform and release actually installed.

## Release is not offered

Keep the Update Center open for up to five minutes while its signed catalog refreshes. Confirm that the installed Gateway has the Update Center and that its configured channel is the intended signed channel. A version is not installable if the catalog signature, channel, package size, SHA-256, release identity, platform, or version check fails. Do not edit the catalog cache or disable signature verification. If 2.2.0 is not listed after its public release is announced, retain the displayed error and operation ID for the administrator.

## Download or checksum failure

Re-download the matching platform kit and run `sha256sum -c SHA256SUMS` from the directory containing the official release checksum file. A mismatch, missing asset, or wrong platform means the file must not be installed. Network downloads that continue to make progress may take time; do not launch a second installation while the first operation is active.

## Gateway does not become healthy

Read the Update Center operation status and host recovery-plane status. The updater checks health and release identity and attempts automatic rollback if the candidate cannot activate. After rollback, confirm the previous version and health before retrying. Do not remove the previous image or pre-update backup while the operation is unresolved.

## Still blocked

Record the Gateway version, platform, operation ID, and sanitized error text. Exclude credentials, `.env` contents, access tokens, private keys, and full logs from public reports. Contact the administrator with that limited evidence.


## Gateway 2.2.1

These instructions also apply to Gateway 2.2.1 on supported Linux VM and Unraid hosts. The optional MCP client remains disabled by default; leave the existing signature and backup checks enabled.
