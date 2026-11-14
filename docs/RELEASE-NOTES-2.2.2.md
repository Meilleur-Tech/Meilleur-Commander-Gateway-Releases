# Gateway 2.2.2 release information

## Changes and improvements

Fabric Commander Gateway 2.2.2 adds an MCP integrations view in the private
Gateway WebUI. It distinguishes incoming MCP clients from optional upstream
MCP servers and reports observed readiness without claiming that a stored
server registration is connected.

The optional NOC & Control upstream client supports OAuth 2.1 authorization
code with PKCE S256, explicit browser consent, token refresh and safe
repeatable revocation. Login is offered only when the Control server actually
advertises the necessary inventory:read scope, and pending token revocation
prevents a new Login. The MCP integration remains disabled by default.

## Installation and update

Choose the matching Unraid or Linux-VM 2.2.2 package for your host. Only after
the immutable signed public release and beta catalog promotion, the Gateway
Update Center should offer a direct update from installed 2.2.0 to 2.2.2.
A 2.2.1 intermediate installation is not intended. Keep a verified pre-update
backup, confirm sufficient space, and install only via the official signed
update channel after inspecting the target version. PROD installation is an
explicit owner action, never part of public publication.

## Rollback and recovery

Retain the previous known-good 2.2.0 image and verified backup until the
installed Gateway and Project Worker report healthy, matching identities
and completed update status. The existing recovery plane implements rollback
if the candidate fails to activate. Do not force-install images via
unverified Docker commands when normal recovery reports a problem.

## Compatibility and security

The Gateway 2.2.2 packages target x86_64 Debian/Ubuntu Linux virtual machines
and Unraid hosts. Native Windows/macOS/Linux desktop clients are independent.
Exact product source:
39a42e9a813e108e20d2c67aa1315c6c14b31ab5.
Gateway OCI:
sha256:caffc7b043b2780b329568f5a9da698e4e759d042b3c7603f28648f519dc9dd5.
Project Worker OCI:
sha256:64ec9b62dd1377746d9f14e5aea5178749ad0e4f6274a79e9e3f7331fc3cc4e4.
Both platform kits originate from the same trusted build and have passed
recursive public binary/secret auditing. The official manifest, SHA-256
inventory and RSA-SHA256-signed latest catalog bind the customer package
identity. Signature checks must never be disabled.

## Known limits and publication status

These are advance customer-facing notes. The availability of this document
does **not** imply 2.2.2 is published or installed. Until a verified signed
catalog is promoted, the current Public Latest remains 2.2.1. Live NOC OAuth
callback/consent, independent Control MCP enablement, Site/AP calls, negative
tenant ACL tests and installed QA rollback require separate real acceptance;
synthetic source tests do not establish that field status.
