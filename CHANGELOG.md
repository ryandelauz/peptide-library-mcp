# Changelog

## 1.0.1 (2026-10-15)

- `search_research`: results no longer carry a `pro_only` flag, and premium courses are left out (free content only).
- Added root `gemini-extension.json` for Gemini CLI extension gallery discovery (remote MCP at `https://peptidelibrary.app/mcp`).

## 1.0.0 (2026-10)

First public release of the hosted server at `https://peptidelibrary.app/mcp`.

- Tools: `search_peptides`, `get_peptide_details`, `compare_peptides`, `search_research`, `get_peptide_categories`, `get_research_trends`, `convert_units`, `solution_concentration`, `blend_concentrations`, `cost_per_amount`.
- Resources: categories, evidence levels, methodology, glossary, disclaimer, `peptide/{id}`.
- Prompts: compare research, summarize evidence, explain a mechanism, find research topics, understand limitations.
- Streamable HTTP, stateless; protocol revision 2026-07-28 and 2025-era clients.
