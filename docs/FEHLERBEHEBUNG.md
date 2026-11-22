# Gateway troubleshooting

This guide covers the Linux VM and Unraid Gateway kits, including Gateway 2.2.6 and earlier supported releases. Use only steps that match the platform and release actually installed.

## Release is not offered

Keep the Update Center open for up to five minutes while its signed catalog refreshes. Confirm that the installed Gateway has the Update Center and that its configured channel is the intended signed channel. A version is not installable if the catalog signature, channel, package size, SHA-256, release identity, platform, or version check fails. Do not edit the catalog cache or disable signature verification. If 2.2.6 is not listed after its public release is announced, retain the displayed error and operation ID for the administrator.

## Download or checksum failure

Re-download the matching platform kit and run `sha256sum -c SHA256SUMS` from the directory containing the official release checksum file. A mismatch, missing asset, or wrong platform means the file must not be installed. Network downloads that continue to make progress may take time; do not launch a second installation while the first operation is active.

## Gateway does not become healthy

Read the Update Center operation status and host recovery-plane status. The updater checks health and release identity and attempts automatic rollback if the candidate cannot activate. After rollback, confirm the previous version and health before retrying. Do not remove the previous image or pre-update backup while the operation is unresolved.

## Still blocked

Record the Gateway version, platform, operation ID, and sanitized error text. Exclude credentials, `.env` contents, access tokens, private keys, and full logs from public reports. Contact the administrator with that limited evidence.


## Gateway 2.2.1

These instructions also apply to Gateway 2.2.1 on supported Linux VM and Unraid hosts. The optional MCP client remains disabled by default; leave the existing signature and backup checks enabled.

## Gateway 2.2.2 troubleshooting

If Gateway 2.2.2 is publicly announced but the signed Update Center still
shows version 2.2.1, allow the normal catalog refresh and inspect the
actual channel, signature-validation and transport error before retrying.
Never edit channel data, disable signatures or manually overwrite the
running Docker image. An optional NOC OAuth Login button being unavailable
can mean the Control MCP issuer or inventory scope is not yet ready.
Retain the pre-update backup and the prior known-good recovery image.


## Gateway 2.2.4

For Gateway 2.2.4, an unavailable or mismatched release signature, unknown SHA-256, expired catalog, missing Project Worker or failed MCP/Web health check is a HOLD. Keep the previous known-good version and use official recovery instead of overriding integrity checks.

## Gateway 2.2.5 troubleshooting

If 2.2.5 is not offered, verify the public signed catalog, installation identity and status refresh before retrying. The cached previous check is not the running version. On installation or health failure, inspect the recovery operation identifier and verify rollback to the known-good image. Do not bypass the catalog signature, SHA-256 integrity check or retry an operation whose outcome is unknown.

## Gateway 2.2.6 MCP monitoring authorization

If `find_clients`, `get_client_details` or `get_ap_link_diagnostics` is not authorized, inspect the actual provider-granted token scopes, active connection state, live discovered tool schemas and permitted site/building ACL. For `monitor:read`, reconnect with explicit browser OAuth/PKCE consent; never edit token scopes or manually create a tool. Missing collection coverage and stale device samples are not proof of an RF fault. The independent native client release channel is unaffected.

## Gateway 2.2.8 operator troubleshooting

If **2.2.8** is announced but no valid update appears, verify the distribution's signed RSA-SHA256 `latest.json`, the release tag, installed platform, expected kit SHA256 and the Update Center's actual catalog status. The source repository or GitHub CI displaying 2.2.8 does not make an installable signed release.

During an interrupted update, inspect the operation ID and its real phase, running container identity, previous known-good image, backup and health. If failure follows Docker cutover, require `failed/rollback_succeeded` with a healthy previous container before retrying. For an in-flight restart the same authenticated operation should progress to `completed`; never edit stored operation JSON or bypass a missing QA gate. Capture sanitized log evidence without credentials.

## Gateway 2.2.9 operator troubleshooting

If **2.2.9** is announced but no valid update appears, verify the distribution's signed RSA-SHA256 `latest.json`, the release tag, installed platform, expected kit SHA256 and the Update Center's actual catalog status. A displayed version number alone does not make an installable signed release.

If `upstream_*` tools fail with `upstream_policy_unavailable`, the MCP policy store is missing while its marker exists: restore it from the backup, or set `MC_UPSTREAM_POLICY_RECREATE=1` once (an empty policy with the default `deny`, with a warning at every start while the variable is set). If an update is refused with `downgrade_not_allowed`, the target is older than the installed version. If a provider connection asks for a new sign-in after the update, the stored refresh authorization was missing or revoked; reconnect with explicit consent. Never edit stored operation files or bypass a missing QA gate; capture sanitized log evidence without credentials.
