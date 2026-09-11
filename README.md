# LeanTrading MCP

Connect Cursor, Claude, and other MCP clients to the hosted LeanTrading
assistant surface through OAuth 2.1/PKCE.

## Hosted server

```text
https://www.leantrading.io/api/mcp
```

The server requires a LeanTrading OAuth connection and an eligible paid
Pro/Elite/Blueprint/Admin account. Product Tester, Explorer, and free accounts
are not granted hosted MCP access.

## Installation

This repository contains the marketplace metadata and Cursor plugin wrapper.
It does not contain credentials and does not require a manually copied
Supabase session JWT.

The default OAuth request is read-only. Chart, write, and execute capabilities
must be explicitly requested by the client and remain subject to LeanTrading
scope checks and confirmation boundaries.

## Safety boundaries

- OAuth authorization uses PKCE with the S256 method.
- Access and refresh tokens are not stored in plaintext by the server.
- Entitlements are checked again on every hosted MCP call.
- Webhook secrets are redacted and are not returned by the MCP tools.
- Silent broker order placement is not exposed as an MCP operation.
- Chart and alert mutations require stronger scopes and confirmation flows.

Marketplace listing is not a security certification. Review the source,
requested scopes, and the LeanTrading privacy/security notices before
connecting an account.

## Repository packaging

This directory is the export bundle for the public
`LeanTrading/leantrading-mcp` repository. It contains metadata and a thin
wrapper for the hosted service; it does not contain the private server source.

Before submitting it to a marketplace:

1. Keep the repository public and limited to this bundle.
2. Keep the repository URL in `server.json` and `plugin.json` synchronized.
3. Keep the hosted endpoint and version in all metadata synchronized with the
   deployed server.
4. Publish the approved data-retention and deletion policy before final
   marketplace submission.

## Privacy note

MCP requests can expose the user's requested LeanTrading system context,
intelligence, risk-preview, advisory, and charting data to the connected
client. Hosted MCP calls are audited using server-side metadata such as user,
client, event, tool, status, and structured metadata; raw tool arguments are
not stored. This metadata is retained only as long as necessary to provide the
service, protect it, and comply with legal obligations, then deleted or
anonymized when no longer needed. Account deletion remains subject to short
backup cycles and statutory retention duties.

MCP hosting and database/authentication subprocessors include Vercel and
Supabase. Data-protection requests can be sent to `info@leantrading.de`.
