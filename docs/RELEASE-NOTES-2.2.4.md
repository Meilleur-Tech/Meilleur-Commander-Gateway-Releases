# Fabric Commander Gateway 2.2.4
Version 2.2.4 extends the Gateway MCP client to interoperate with modern MCP protocol 2026-07-28 and legacy 2025-11-25 servers. The upstream MCP SDK stack uses FastMCP 4.2.0, MCP Python SDK 2.3.0 and httpx2. Generic upstream MCP server connections can be registered in the Gateway operator interface, with separate tool/schema approval and least-privilege authorization.

Important security behavior: tool input and declared output schemas are pinned and validated; changes cause an approval hold. Unknown or unsuccessful remote tool outcomes are not automatically retried. OAuth 2.1 with PKCE can be configured for supported providers, including explicit browser consent and per-provider token isolation. Generic provider login may require the provider to pre-register the client ID and callback address; discovery alone does not mean authenticated or authorized.

Compatibility: official Unraid and Linux x86_64 VM kits contain the same frozen Gateway and Project Worker OCI images. Native Windows, macOS and Linux clients are distributed independently. New MCP integrations remain opt-in; installing 2.2.4 does not automatically authorize NOC, Home Assistant, Lexit or other upstream servers.

Installation: only use the matching immutable published package and signed beta update catalog. Verify exact SHA-256, pinned RSA-SHA256 signature, Gateway/Worker identity and readiness before applying the update. Keep a verified pre-update backup and previous known-good version. Use the normal Gateway Update Center and recovery-plane rollback rather than forced Docker replacement. Control beta.60 live OAuth/browser consent and ChatGPT end-to-end tools are separate acceptance tasks, not guaranteed by installing this Gateway release.

Frozen reviewed product source: 5ce97bfe3f28b6e8f659a77811be6bcffe7e6466.
