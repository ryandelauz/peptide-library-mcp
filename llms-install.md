# Installing the Peptide Library MCP server (for AI agents)

Peptide Library is a hosted, remote MCP server. There is nothing to clone, build or install, and it needs
no API key, account or environment variables.

- URL: `https://peptidelibrary.app/mcp`
- Transport: Streamable HTTP
- Authentication: none

## Cline

Add this entry to `cline_mcp_settings.json` (Cline → MCP Servers → Configure MCP Servers), keeping any
servers already there:

```json
{
  "mcpServers": {
    "peptide-library": {
      "type": "streamableHttp",
      "url": "https://peptidelibrary.app/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Every tool is read-only, so it is safe to auto-approve them if the user wants to.

## Other clients

Any client that supports remote MCP servers uses the same URL:

```json
{ "mcpServers": { "peptide-library": { "url": "https://peptidelibrary.app/mcp" } } }
```

## Check that it works

1. The server should list 10 tools, including `search_peptides`, `get_peptide_details` and
   `compare_peptides`.
2. Ask: "What does the research say about BPC-157?" The answer should come from `get_peptide_details` and
   link to `https://peptidelibrary.app/library/bpc-157`.
3. If the connection fails, check `https://peptidelibrary.app/mcp/health` (returns `{"ok": true}` when the
   service is up).

The server returns research and educational information only: no doses, dosing schedules, vendors or
prices. Setup page for people: https://peptidelibrary.app/developers/mcp
