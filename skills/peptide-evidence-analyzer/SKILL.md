---
name: peptide-evidence-analyzer
description: Judge how reliable the human evidence for a peptide is, using Peptide Library's published Human Evidence Quality assessments. Use when a question asks how strong or trustworthy the evidence is, what the human clinical studies actually show for a specific claim, how well a study was designed, its risk of bias (RoB 2, ROBINS-I), or the GRADE certainty of an outcome, for peptides such as BPC-157, GHK-Cu, MOTS-c, SS-31 (elamipretide) and TB-500. Reports assessed claims, reviewed studies and evidence gaps without overstating them. Research and education only; never gives dosing or treatment advice.
license: MIT
compatibility: Needs network access to peptidelibrary.app or api.peptidelibrary.app. Works best with the remote MCP server at https://peptidelibrary.app/mcp (tools get_evidence_summary and get_human_study); falls back to the public REST API.
metadata:
  version: "1.1.0"
  homepage: https://peptidelibrary.app/research/evidence-quality
  repository: https://github.com/ryandelauz/peptide-library-mcp
---

# Peptide Evidence Analyzer

Peptide Library's Human Evidence Quality layer answers one question: **what do the human studies of a compound show for one specific claim, and how reliable is that?** Use this skill when a user wants evidence quality rather than a general profile. For a general profile, mechanism or regulatory status, use `peptide-library-research`.

## Access

**MCP (preferred).** Server `https://peptidelibrary.app/mcp` (anonymous, read-only).

- `search_peptides` finds the peptide id.
- `get_evidence_summary` (`peptide`: id or name) returns each claim with its state, per-outcome certainty, the reviewed human studies and the evidence gaps.
- `get_human_study` (`study_id`: an id such as `PLS-00026`) returns one study: design, participants, outcomes as the authors reported them, limitations, risk of bias and its sources.

**REST (fallback).** `https://api.peptidelibrary.app/v1`, no key:

- `GET /research/evidence-quality/peptides/{peptide}`
- `GET /research/evidence-quality/peptides/{peptide}/claims/{claim}`
- `GET /research/studies/{id}`
- `GET /research/evidence-quality/assessments` (every published assessment)
- `GET /research/evidence-quality/methodology`

Pages: `https://peptidelibrary.app/research/evidence-quality/<peptide>`, `/research/evidence-quality/<peptide>/<claim>` and `/research/studies/<id>` (lowercase).

## Workflow

1. Resolve the peptide (`search_peptides`), then call `get_evidence_summary`.
2. If the status is `not_assessed`, say that no published assessment exists yet. That is not evidence for or against the claim. Offer the general profile instead (`get_peptide_details`).
3. For each claim the user cares about, report:
   - the claim's state;
   - for each assessed outcome, its GRADE certainty (high, moderate, low or very low) and the plain summary;
   - how many human studies were identified, reviewed and randomized. Keep these counts apart.
4. For a study the answer leans on, call `get_human_study`. Report its design, its participant numbers (if documented), the outcomes as reported, its limitations and its risk-of-bias judgement with the tool used:
   - RoB 2 for randomized trials;
   - ROBINS-I for nonrandomized comparative studies;
   - a structured appraisal for uncontrolled designs and case reports.
5. Report the evidence gaps the data lists (research activity, human research, evidence quality, clinical relevance, safety). They describe what is missing, never a verdict that something doesn't work.
6. Link every claim and study page the results return.

## Reading the states correctly

- A claim is something under investigation, never an established benefit. Phrase it that way ("the claim that GHK-Cu improves signs of skin aging").
- "Not assessed", "in progress" and "insufficient information" are operational states, not GRADE categories. None of them means "doesn't work".
- An assessment marked `automated` was produced by AI under the published rules and was not reviewed by a person. Say so. Only call it reviewed when the data says `reviewed`.
- Research volume is not evidence strength. Publications, studies, registrations and outcomes are counted separately. One study can have several reports, and it counts once.
- `authors_concluded` paraphrases the authors' own conclusion, not Peptide Library's assessment. Attribute it to the authors.
- Don't recompute or estimate certainty, effect sizes or participant counts. If a number is null, say it isn't documented.

## Scope

Research and education only; not medical advice. Never give dose amounts, routes, durations, regimens or treatment recommendations. The data deliberately leaves them out, so don't fill them in from elsewhere. Cite only the study's own reports and the Peptide Library pages returned. Methodology: https://peptidelibrary.app/research/evidence-quality/methodology
