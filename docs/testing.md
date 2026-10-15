# Testing the hosted server

With Node.js 20+ and the official MCP Inspector:

```bash
URL=${PEPTIDE_LIBRARY_MCP_URL:-https://peptidelibrary.app/mcp}
npx -y @modelcontextprotocol/inspector --cli "$URL" --transport http --method tools/list --strict
npx -y @modelcontextprotocol/inspector --cli "$URL" --transport http --method tools/call --tool-name search_peptides --tool-arg query=semaglutide
npx -y @modelcontextprotocol/inspector --cli "$URL" --transport http --method tools/call --tool-name get_peptide_details --tool-arg peptide=BPC-157
npx -y @modelcontextprotocol/inspector --cli "$URL" --transport http --method resources/read --uri peptidelibrary://evidence-levels
curl -s https://peptidelibrary.app/mcp/health
```

What to check:

- `tools/list` returns 10 tools, all `readOnlyHint: true`, and `--strict` reports no schema problems.
- Results include a `peptidelibrary.app` URL, `source`, `disclaimer` and `retrieved_at`.
- No result contains a dose, regimen, vendor or price.
- An unknown peptide returns a `not_found` error with suggestions, not invented data.

Please don't load-test the hosted endpoint; it is rate-limited.
