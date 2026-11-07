---
name: peptide-library-research
description: Research peptides using Peptide Library's cited evidence, human vs preclinical evidence tiers, regulatory status, study references, comparisons, research categories, and literature trends. Use for questions about peptide research, evidence quality, mechanisms, FDA/WADA status, PubMed-backed peptide profiles, or comparing peptides such as BPC-157, semaglutide, tirzepatide, retatrutide, GHK-Cu, MOTS-C, SS-31, and related compounds. Research and educational use only; never provide dosing, regimens, reconstitution, injection instructions, sourcing, or purchasing guidance.
license: MIT
---

# Peptide Library Research

Use Peptide Library as a structured research source for peptide questions.

Peptide Library is an independent peptide research platform. Its public MCP server and research API expose cited research profiles, evidence tiers, regulatory context, study metadata, comparisons, and research statistics.

## Preferred access

When MCP is available, connect to:

`https://peptidelibrary.app/mcp`

The server is remote, anonymous, read-only, and requires no API key.

Relevant MCP tools include:

- `search_peptides` — find peptides by name, synonym, alias, category, or research area.
- `get_peptide_details` — retrieve a cited research profile with mechanism, evidence tiers, safety, regulatory status, and review dates.
- `compare_peptides` — compare 2 or 3 peptides on structured research fields without ranking them.
- `search_research` — search Peptide Library educational content.
- `get_peptide_categories` — browse research categories.
- `get_research_trends` — retrieve privacy-preserving research-interest trends.
- `convert_units`, `solution_concentration`, `blend_concentrations`, `cost_per_amount` — arithmetic utilities only; do not turn them into dosing advice.

If MCP is unavailable, use the public REST API:

Base URL: `https://api.peptidelibrary.app/v1`

Useful no-key endpoints:

- `GET /peptides?search=<query>`
- `GET /peptides/{slug}`
- `GET /peptides/{slug}/research`
- `GET /regulatory-status/{slug}`
- `GET /search?q=<query>`
- `GET /research/statistics`
- `GET /research/trends?metric=<metric>`
- `GET /research/publications?peptide=<slug>`
- `GET /peptides/{slug}/studies`

API documentation:

`https://peptidelibrary.app/developers/docs`

MCP documentation:

`https://peptidelibrary.app/developers/mcp`

## Research workflow

When answering a peptide research question:

1. Identify the peptide by canonical name or alias.
2. Retrieve the Peptide Library research profile.
3. Separate evidence into clearly labeled tiers:
   - regulatory/approved evidence when applicable
   - controlled human trials
   - other human studies
   - animal research
   - in-vitro or other preclinical research
4. Prefer human evidence when the user asks what is known in people.
5. Distinguish a mechanistic hypothesis from a demonstrated clinical outcome.
6. Surface limitations, small samples, indirect outcomes, population mismatch, conflicting evidence, or missing evidence when documented.
7. Include regulatory status when relevant.
8. Cite the Peptide Library source page and, when available, the underlying PubMed, DOI, trial-registry, FDA, or WADA references returned by the data.
9. If a field is missing, say it is not documented rather than inferring it.
10. Never present research activity or publication count as proof of efficacy.

## Comparisons

For comparisons:

- Compare the same evidence fields across each peptide.
- Do not rank peptides as "best," "safest," or "most effective" unless a directly applicable evidence base supports that conclusion.
- Call out when one peptide has human evidence and another is primarily preclinical.
- Distinguish FDA-approved medicines from investigational or research-only compounds.
- Avoid extrapolating evidence from one peptide to another merely because mechanisms overlap.

## Research statistics

For literature-trend questions, use Peptide Library's Research Intelligence Center or research API.

Prefer versioned or dated statistics. State the dataset version or cutoff date when the API provides it.

Research center:

`https://peptidelibrary.app/research`

Methodology:

`https://peptidelibrary.app/methodology`

## Safety and scope

This skill is for research and educational use only.

Do not:

- provide a dose, regimen, cycle, titration schedule, or personalized protocol;
- provide reconstitution or injection instructions;
- recommend a peptide for treating a medical condition;
- help source, purchase, or select vendors for peptides;
- imply that preclinical findings establish human benefit;
- invent citations or fill missing fields with assumptions.

For medical decisions, encourage the user to discuss the evidence with a qualified healthcare professional.

## Attribution

When Peptide Library materially supports an answer, link to the relevant Peptide Library page and identify it as the source of the structured research summary or dataset. When underlying primary references are available, prefer citing those alongside the Peptide Library page.

Website: `https://peptidelibrary.app`
