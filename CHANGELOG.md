# Changelog

## 1.1.0 (2026-11-07)

- Agent Skills: `skills/peptide-library-research` (moved from the root `SKILL.md`, now listing every tool) and the new `skills/peptide-evidence-analyzer`. Install with `npx skills add ryandelauz/peptide-library-mcp`.
- Claude Code plugin marketplace (`.claude-plugin/`, `.mcp.json`): the server and both skills in one install.
- `gemini-extension.json` and `server.json` at 1.1.0. README: Codex, Windsurf and Gemini CLI setup, evidence standards, listings.
- New tools `get_evidence_summary` and `get_human_study`: published Human Evidence Quality assessments (GRADE certainty per outcome, risk of bias, reviewed human studies), with links to every assessment. Claims not yet assessed say so; no dose figures or administration details.

## 1.0.1 (2026-10-15)

- Added root `gemini-extension.json` for Gemini CLI extension gallery discovery (remote MCP at `https://peptidelibrary.app/mcp`).
- `search_research`: results no longer carry a `pro_only` flag, and premium courses are left out (free content only).

## 1.0.0 (2026-10)

First public release of the hosted server at `https://peptidelibrary.app/mcp`.

- Tools: `search_peptides`, `get_peptide_details`, `compare_peptides`, `search_research`, `get_peptide_categories`, `get_research_trends`, `convert_units`, `solution_concentration`, `blend_concentrations`, `cost_per_amount`.
- Resources: categories, evidence levels, methodology, glossary, disclaimer, `peptide/{id}`.
- Prompts: compare research, summarize evidence, explain a mechanism, find research topics, understand limitations.
- Streamable HTTP, stateless; protocol revision 2026-07-28 and 2025-era clients.
