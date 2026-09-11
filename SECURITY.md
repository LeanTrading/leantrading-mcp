# Security notes

## Scope

This package is a thin marketplace wrapper for the hosted LeanTrading MCP
endpoint. It contains no API keys, OAuth tokens, broker credentials, or local
execution code.

## Authentication and authorization

The hosted endpoint uses OAuth 2.1 authorization-code flow with PKCE/S256.
Access is limited by the user's LeanTrading entitlement and the scopes granted
by the OAuth client. Marketplace installs start with `mcp:read`; higher-risk
capabilities are not implicit.

## Data handling

The connected client may send tool arguments to LeanTrading and receive
user-authorized strategy, risk, advisory, or charting data in return. The
server-side audit trail is intended to contain tool-call status metadata rather
than raw tool arguments. The approved retention and deletion policy must be
published before the final marketplace submission.

Never place any of the following in this repository:

- Supabase access tokens
- OAuth authorization codes or refresh tokens
- webhook secrets
- broker credentials
- production environment files

## Reporting

Report suspected vulnerabilities or unauthorized actions to
`info@leantrading.de`. Do not include credentials, access tokens, or production
secrets in the initial report. Marketplace approval does not replace an
independent security review; affected MCP tokens should be revoked immediately
when exposure is suspected.
