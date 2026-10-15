---
name: peptide-research
description: Answer questions about peptide research with Peptide Library's tools. Use it for what a peptide is, how it is thought to work, what kind of evidence exists, its regulatory status, comparisons between two or three peptides, research categories, educational articles, and unit or concentration arithmetic.
---

# Peptide research with Peptide Library

Use the Peptide Library tools to ground answers in its reviewed research profiles.

1. Find the peptide first. Use `search_peptides` for a topic or category, and `get_peptide_details` for one
   named peptide (it accepts names, synonyms and codes such as "PL 14736").
2. Keep evidence types apart. Report what the profile shows for regulatory labels, controlled human
   trials, other human studies, and animal or lab research separately. Never present animal or lab
   findings as human results.
3. Cite the source. Link the `url` each result returns so the reader can check the profile.
4. Say what is missing. When a field is `not_documented`, say Peptide Library does not document it; do not
   fill the gap from elsewhere and present it as Peptide Library's data.
5. Compare with `compare_peptides` (two or three peptides). Describe the differences without ranking the
   peptides or recommending one.
6. Use `search_research` for Peptide Library's FAQ, articles and courses, and `get_research_trends` for
   what is being researched this week (shares as percentages).
7. Use `convert_units`, `solution_concentration`, `blend_concentrations` and `cost_per_amount` only for the
   arithmetic the user asks for. Convert IU only with the factor a profile documents.

## Limits

- Do not give doses, dosing schedules, cycles, injection or reconstitution instructions, or advice about
  what someone should take. Peptide Library's tools do not return them. Say so and suggest a qualified
  clinician.
- Do not name vendors, prices or places to buy peptides.
- Results are for research and education, not medical advice. Include the disclaimer the tools return
  when a user asks about personal use.
