# Fabric Commander Gateway 2.2.6

## MCP OAuth and monitoring integration
- Uses the existing provider-neutral MCP connection wizard. Additional available OAuth scopes are discovered from the provider's metadata and require explicit selection and a new PKCE-protected authorization.
- After authorized reconnect, the available MCP tools are rediscovered and matched to the already approved server trust profile and live, pinned schemas. The actual granted token scopes remain visible. No automatic permission elevation or device changes.
- Control beta.65 monitoring tools can be exposed when the user's OAuth token genuinely contains monitor:read, the installed provider returns those tools and the applicable site/building ACL allows access. Unavailable RF/port data is not invented.

## Release and compatibility
- Less duplicate MeilleurCodeGuard/CI orchestration while retaining required product, MCP, security and trusted release checks.
- Includes matching Gateway and Project Worker binaries for x86_64 Debian/Ubuntu Linux VMs and Unraid. Native clients use their own independent release channels.
- Uses the existing pinned RSA-SHA256 update-catalog trust root and verified platform SHA-256 hashes.
- Operator controls when the public update is installed on PROD through the normal Update Center. Public distribution never automatically installs PROD.
- Source revision: dd4746b593e39b08f01185b470f55af9429b17fc.

## Installation and update

Use only the x86_64 Debian/Ubuntu Linux VM or Unraid kit that matches the Gateway host, verify the official SHA256SUMS and update through the normal signed beta channel. An operator must select and approve installation in the Update Center. Updating alone does not grant monitoring rights.

## Rollback and recovery

The Gateway recovery plane retains the previously known-good image and performs health and matching Project Worker checks after activation. If installation reports a failure, examine the recorded operation and allow the existing safe rollback path; do not start duplicate operations. In isolated QA the original 2.2.6 kit installed and Gateway/WebUI health and matching worker binding passed. A separate full rollback cycle was not run for this version and is not claimed.

## Compatibility and security

The public channel continues to use the existing pinned RSA-SHA256 catalog signature, exact source SHA, per-platform package size and SHA-256 hashes. No gateway RSA/Cosign trust cutover occurred. Unraid and Debian/Ubuntu VM are supported separately; the native Windows, macOS and Linux clients update independently. `monitor:read` requires a new consent and is still subject to provider site/building access control. No direct ChatGPT-to-Control monitoring test after fresh consent has yet been accepted as production evidence. Data missing from a controller is reported as unknown.
