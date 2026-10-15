# Security policy

The Peptide Library MCP server (`https://peptidelibrary.app/mcp`) is a hosted, anonymous, read-only service. It has no accounts, stores no personal data and exposes no write operations.

## Reporting a vulnerability

Email **support@peptidelibrary.app** with "Security" in the subject: what you found, how to reproduce it, and the impact you expect. Please don't open a public issue for a security problem. We acknowledge reports within 3 business days.

In scope: the MCP endpoint, its health check (`/mcp/health`) and the documentation page. Please don't run load tests or denial-of-service tests; the endpoint is rate-limited.

## Design notes

- Read-only by construction: the server reads public library data with a restricted, anonymous database role; user tables are not reachable.
- Inputs are validated against strict schemas with length and size limits; user text never reaches SQL except as a bound RPC parameter.
- Errors never include stack traces or internal details.
- Requests are rate-limited per IP at the edge.
- Tool arguments and results are not logged or stored.
