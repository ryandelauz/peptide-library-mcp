# Peptide Library MCP Server and Agent Skills

[![skills.sh](https://skills.sh/b/ryandelauz/peptide-library-mcp)](https://skills.sh/ryandelauz/peptide-library-mcp)

Evidence-based peptide research for AI assistants: cited research profiles, human and preclinical evidence kept apart, human evidence quality (risk of bias, GRADE), mechanisms, FDA/WADA status, comparisons and educational arithmetic. Peptide Library is an independent research library ([methodology](https://peptidelibrary.app/methodology)); this repository is how agents connect to it, through a remote [Model Context Protocol](https://modelcontextprotocol.io) server or as installable Agent Skills.

Use it when an assistant needs a citable answer to questions like "how much of the BPC-157 research is in humans?" or "what is the FDA status of tirzepatide?", instead of guessing from training data.

**Website:** https://peptidelibrary.app
**Server URL:** `https://peptidelibrary.app/mcp`
**Documentation:** https://peptidelibrary.app/developers/mcp

The server is hosted by Peptide Library. It is free, anonymous and read-only: no account, no API key and nothing to install. This repository holds its public documentation, Agent Skills, client configuration examples and registry metadata; the server itself runs from Peptide Library's private codebase.

## Install as an Agent Skill

```bash
npx skills add ryandelauz/peptide-library-mcp
```

This installs two skills ([Agent Skills](https://agentskills.io) format, via the [skills CLI](https://skills.sh)) into Claude Code, Codex, Cursor and the other agents the CLI supports:

| Skill | Use it for |
|---|---|
| [`peptide-library-research`](skills/peptide-library-research/SKILL.md) | General peptide research: profiles, evidence tiers, mechanisms, regulatory status, comparisons, literature trends |
| [`peptide-evidence-analyzer`](skills/peptide-evidence-analyzer/SKILL.md) | How reliable the human evidence is for a claim: reviewed studies, risk of bias (RoB 2, ROBINS-I), GRADE certainty, evidence gaps |

Install one with `npx skills add ryandelauz/peptide-library-mcp --skill peptide-evidence-analyzer`. The skills use the MCP server when it's connected and fall back to the public REST API.

**Claude Code plugin** (MCP server and both skills in one step):

```bash
claude plugin marketplace add ryandelauz/peptide-library-mcp
claude plugin install peptide-library@peptide-library
```

## What it does

| Tool | Description |
|---|---|
| `search_peptides` | Fuzzy search by name, synonym or alias, with research-category and research-area filters and pagination |
| `get_peptide_details` | Research profile: classification, mechanism and targets, evidence by tier (regulatory label, controlled human trials, other human studies, animal and in-vitro research) with cited sources, safety, FDA/WADA status, review dates |
| `compare_peptides` | Side-by-side comparison of 2 or 3 profiles on structured fields; never ranks |
| `search_research` | Search Peptide Library's FAQ, per-peptide FAQs, articles and courses, with links |
| `get_peptide_categories` | Research categories with descriptions, counts and member profiles |
| `get_research_trends` | This week's most-researched peptides in the community, as percentages |
| `get_evidence_summary` | What reviewed human research shows for one peptide, claim by claim: GRADE certainty per outcome or "not yet assessed", reviewed studies, evidence gaps |
| `get_human_study` | One reviewed human study: design, participants, outcomes as the authors reported them, limitations and risk of bias, with sources |
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

### OpenAI Codex

`~/.codex/config.toml`:

```toml
[mcp_servers.peptide-library]
url = "https://peptidelibrary.app/mcp"
```

### Windsurf

`~/.codeium/windsurf/mcp_config.json`:

```json
{ "mcpServers": { "peptide-library": { "serverUrl": "https://peptidelibrary.app/mcp" } } }
```

### Gemini CLI

```bash
gemini extensions install https://github.com/ryandelauz/peptide-library-mcp
```

The extension ([gemini-extension.json](gemini-extension.json)) connects the remote server; no key needed.

### VS Code

`.vscode/mcp.json`: [examples/vscode-mcp.json](examples/vscode-mcp.json)

### Cline

Cline → MCP Servers → Configure MCP Servers, then add the entry from [llms-install.md](llms-install.md)
(`"type": "streamableHttp"`, `"url": "https://peptidelibrary.app/mcp"`). Agents installing the server can
follow that file directly.

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

## Evidence standards

Every finding is labelled by the kind of evidence behind it, and the tiers are never merged:

| Tier | What it means |
|---|---|
| Regulatory | Approved labelling and agency records (FDA and WADA status) |
| Controlled human trials | Randomized or otherwise controlled studies in people |
| Other human research | Observational studies, case series, case reports |
| Animal research | In vivo studies in animals |
| In vitro | Cell, tissue and biochemical studies |

Human Evidence Quality goes one step further for selected peptides: each claim is broken into questions, each human study gets a risk-of-bias judgement with the tool that fits its design (RoB 2, ROBINS-I or a structured appraisal), and each outcome a GRADE certainty. These assessments are automated under published rules and labelled `automated`; "not assessed" and "insufficient information" are states, not verdicts. Methodology: https://peptidelibrary.app/research/evidence-quality/methodology

## Endpoint details

- Transport: Streamable HTTP (POST), stateless. Protocol revision 2026-07-28 and 2025-era clients (2024-11-05 to 2025-11-25).
- Authentication: none; every tool is read-only (`readOnlyHint: true`).
- Limits: about 300 requests per minute per IP, 64 KB per request, 25 results per page.
- Health check: `GET https://peptidelibrary.app/mcp/health`.

## Where it's listed

- [Official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=app.peptidelibrary/peptide-library): `app.peptidelibrary/peptide-library`
- [Glama](https://glama.ai/mcp/connectors/app.peptidelibrary/peptide-library)
- [skills.sh](https://skills.sh/ryandelauz/peptide-library-mcp/peptide-library-research)

## Security and privacy

Anonymous and read-only: there is no authentication, and no tool can read or change an account. Every tool is annotated `readOnlyHint: true`. Report security issues as described in [SECURITY.md](SECURITY.md).

### Privacy

No account and no personal data. Peptide Library keeps daily counts of requests, tool calls, errors and the client name your assistant reports; it does not store tool arguments, results or IP addresses. The hosting provider processes IPs to apply rate limits. Full policy: https://peptidelibrary.app/privacy#mcp-server

## REST API

The same research data (plus the vendor directory and prices, with a free key) is available as a REST API for apps and scripts: `https://api.peptidelibrary.app/v1`, with an OpenAPI 3.1 spec, Postman collection and TypeScript and Python SDKs. Docs: https://peptidelibrary.app/developers · Repo: https://github.com/ryandelauz/peptide-library-api

## Data

Profiles follow Peptide Library's [editorial policy](https://peptidelibrary.app/editorial-policy) and [methodology](https://peptidelibrary.app/methodology): claims cite PubMed, DOI, trial registries and FDA or WADA records, and evidence is labelled by kind.

## Links

- Website: https://peptidelibrary.app
- Research center: https://peptidelibrary.app/research
- Developer API: https://peptidelibrary.app/developers
- iOS app: https://apps.apple.com/us/app/peptide-library-peptide-log/id6755092737
- Android app: https://play.google.com/store/apps/details?id=com.peptidelibrary.app
- Support: https://peptidelibrary.app/support · support@peptidelibrary.app
- Security: [SECURITY.md](SECURITY.md)

## License

Documentation and examples in this repository: [MIT](LICENSE). The hosted service and Peptide Library content are subject to the [terms of service](https://peptidelibrary.app/terms).
