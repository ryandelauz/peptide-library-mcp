# Peptide Library MCP Server

A remote Model Context Protocol server providing structured peptide research information, educational comparison tools, and research resources for compatible AI assistants.

**Website:** https://peptidelibrary.app
**Server URL:** `https://peptidelibrary.app/mcp`
**Documentation:** https://peptidelibrary.app/developers/mcp

The server is hosted by Peptide Library. It is free, anonymous and read-only: no account, no API key and nothing to install. This repository holds its public documentation, client configuration examples and registry metadata; the server itself runs from Peptide Library's private codebase.

## What it does

| Tool | Description |
|---|---|
| `search_peptides` | Fuzzy search by name, synonym or alias, with research-category and research-area filters and pagination |
| `get_peptide_details` | Research profile: classification, mechanism and targets, evidence by tier (regulatory label, controlled human trials, other human studies, animal and in-vitro research) with cited sources, safety, FDA/WADA status, review dates |
| `compare_peptides` | Side-by-side comparison of 2 or 3 profiles on structured fields; never ranks |
| `search_research` | Search Peptide Library's FAQ, per-peptide FAQs, articles and courses, with links |
| `get_peptide_categories` | Research categories with descriptions, counts and member profiles |
| `get_research_trends` | This week's most-researched peptides in the community, as percentages |
| `convert_units` | mg ↔ mcg, and IU only with a peptide's documented IU-per-mg factor |
| `solution_concentration` | Amount ÷ volume as mg/mL, mcg/mL (IU/mL with a documented factor) |
| `blend_concentrations` | Per-component concentration and share in one volume |
| `cost_per_amount` | Total cost and cost per mg/mcg/IU from a price you enter |

**Resources:** `peptidelibrary://categories`, `peptidelibrary://evidence-levels`, `peptidelibrary://methodology`, `peptidelibrary://glossary`, `peptidelibrary://disclaimer`, `peptidelibrary://peptide/{id}`.

**Prompts:** `compare_peptide_research`, `summarize_peptide_evidence`, `explain_mechanism`, `find_research_topics`, `understand_research_limitations`.

Every result includes the Peptide Library URL it came from and a research-use disclaimer. Fields the library doesn't have are returned as `not_documented`.

### What it will not do

- Give doses, regimens, cycles, reconstitution or injection instructions.
- List vendors, prices or purchase links.
- Read or change any account or personal data.
- Rank peptides or invent studies or citations.

Research and educational use only. Not medical advice. Peptide Library does not sell peptides.

## Connect

### Claude (claude.ai and Claude Desktop)

Customize → Connectors → **Add custom connector** → name `Peptide Library`, URL `https://peptidelibrary.app/mcp`. On Team and Enterprise plans an owner adds it under Organization settings → Connectors. Free plans allow one custom connector.

### Claude Code

```bash
claude mcp add --transport http peptide-library https://peptidelibrary.app/mcp
```

### ChatGPT

Where your plan or workspace allows custom MCP servers: Plugins → **+** → **Add custom MCP server** → URL `https://peptidelibrary.app/mcp`, Authentication **No authentication** → **Create as a plugin**. Then type `@` in a chat to use it. See [examples/chatgpt.md](examples/chatgpt.md).

### Cursor

`~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project): [examples/cursor-mcp.json](examples/cursor-mcp.json)

```json
{ "mcpServers": { "peptide-library": { "url": "https://peptidelibrary.app/mcp" } } }
```

### VS Code

`.vscode/mcp.json`: [examples/vscode-mcp.json](examples/vscode-mcp.json)

### Any MCP client

Streamable HTTP at `https://peptidelibrary.app/mcp`, no authentication. Generic config: [examples/mcp.json](examples/mcp.json).

### MCP Inspector

```bash
npx -y @modelcontextprotocol/inspector --cli https://peptidelibrary.app/mcp --transport http --method tools/list
```

## Example questions

- What does the research say about BPC-157, and how much of it is in humans?
- Compare semaglutide and tirzepatide: mechanism, evidence and regulatory status.
- Which peptides in the library are studied for cognition?
- What is the FDA and WADA status of bremelanotide (PT-141)?
- If 10 mg is dissolved in 2 mL, what is the concentration in mcg/mL?

## Endpoint details

- Transport: Streamable HTTP (POST), stateless. Protocol revision 2026-07-28 and 2025-era clients (2024-11-05 to 2025-11-25).
- Authentication: none; every tool is read-only (`readOnlyHint: true`).
- Limits: about 300 requests per minute per IP, 64 KB per request, 25 results per page.
- Health check: `GET https://peptidelibrary.app/mcp/health`.

## Privacy

No account and no personal data. Peptide Library keeps daily counts of requests, tool calls, errors and the client name your assistant reports; it does not store tool arguments, results or IP addresses. The hosting provider processes IPs to apply rate limits. Full policy: https://peptidelibrary.app/privacy#mcp-server

## Data

Profiles follow Peptide Library's [editorial policy](https://peptidelibrary.app/editorial-policy) and [methodology](https://peptidelibrary.app/methodology): claims cite PubMed, DOI, trial registries and FDA or WADA records, and evidence is labelled by kind.

## Links

- Website: https://peptidelibrary.app
- iOS app: https://apps.apple.com/us/app/peptide-library-peptide-log/id6755092737
- Android app: https://play.google.com/store/apps/details?id=com.peptidelibrary.app
- Support: https://peptidelibrary.app/support · support@peptidelibrary.app
- Security: [SECURITY.md](SECURITY.md)

## License

Documentation and examples in this repository: [MIT](LICENSE). The hosted service and Peptide Library content are subject to the [terms of service](https://peptidelibrary.app/terms).
