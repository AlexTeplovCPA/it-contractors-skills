# Writing Rules — it-contractors-skills

## Purpose

These writing rules apply to repository-level documentation, `SKILL.md` files, shared references, templates, and example outputs in `it-contractors-skills`.

The goal is consistency.

This repository is client-facing, IT-contractor-specific, and preparation-oriented. The writing should reflect that.

---

## Core Writing Standard

Write for a system that must:

- organize information
- map likely fields
- identify missing items
- preserve uncertainty
- produce outputs a non-practitioner can understand

Do not write as if the repository exists to:
- teach tax theory
- market services
- replace CPA judgment
- impress technical readers

---

## Audience

Assume two audiences:

### 1. End user
A Canadian IT contractor using the workflow.

This person may:
- have incomplete records
- know little about tax forms
- need simple instructions
- want a practical result

### 2. Repository maintainer
A person drafting or refining skills in the repo.

This person needs:
- consistent naming
- predictable structure
- reusable patterns
- clear boundaries

Write so both can understand the intent of the workflow.

---

## Tone

Use a tone that is:

- practical
- structured
- calm
- bounded
- specific

Do not sound:

- promotional
- overly technical
- academic
- legalistic
- overconfident

Good tone:
- direct
- helpful
- matter-of-fact
- careful without sounding vague

---

## Sentence Style

Prefer:

- short to medium sentences
- one idea per sentence when possible
- direct verbs
- plain wording

Avoid:

- long stacked clauses
- abstract wording
- inflated phrasing
- unnecessary repetition

Good:
- Organize the user’s document set.
- Flag missing records.
- Do not assume a receipt exists unless the user confirms it.

Bad:
- The workflow should seek to facilitate a comprehensive and holistic organizational process through which the user’s document universe may be better understood.

---

## Verb Preference

Prefer these verbs:

- organize
- collect
- identify
- map
- review
- flag
- summarize
- prepare
- group
- route

Avoid unnecessary synonym switching.

For example:
- pick `income` and use it consistently
- pick `upload` and use it consistently
- pick `missing items` and use it consistently

Do not rotate through synonyms just for variation.

---

## Vocabulary Rules

Use clear, familiar terms.

Prefer:
- income
- expenses
- tax slips
- missing items
- open questions
- support
- self-entry summary
- CPA handoff summary
- grouped-by-form summary

Avoid vague or inflated terms such as:
- artifacts
- leverage
- optimize
- facilitate
- orchestrate
- stakeholders
- robust solutioning

Use technical tax terms only when they are actually needed.

---

## American Spelling

Use American spelling throughout the repository for consistency.

Examples:
- organize
- categorize
- analyze
- standardize

Do not mix American and British spelling.

---

## No Em Dashes

Do not use em dashes anywhere in the repository.

Use:
- commas
- periods
- parentheses
- colons

instead.

---

## Capitalization Rules

Use sentence case for headings unless a fixed term requires otherwise.

Good:
- `## Output requirements`
- `## Shared input schema`

Avoid title case unless there is a strong reason.

Keep skill names, frontmatter names, and file paths in lowercase where required.

---

## Markdown Style

Prefer:

- short sections
- clear headings
- short bullet lists where helpful
- fenced code blocks for examples
- consistent path formatting with backticks

Avoid:
- overly long bullet lists
- dense walls of text
- decorative formatting
- excessive bolding

Use tables only when they materially improve clarity.

---

## Writing for `SKILL.md`

Write instructions to the model, not to the user.

Good:
- Organize documents by category.
- Mark each document as received, missing, or unclear.
- Do not determine final filing positions.

Bad:
- You should ask the user to kindly provide all possible records.
- This tool is very useful for helping people understand their taxes.

A `SKILL.md` file should be operational, not explanatory.

---

## Structure Expectations for `SKILL.md`

Default sections should usually include:

1. Purpose
2. Core rules
3. Inputs
4. Workflow
5. Output requirements
6. Status guidance
7. Boundaries
8. Related uses
9. References if needed

Not every skill must use the exact same headings, but the overall structure should feel consistent.

---

## Description Field Rules

The YAML `description` field is for skill discovery.

It must say:
- what the skill does
- when to use it

It should be:
- specific
- practical
- concise
- trigger-aware

Good:
- organize the income sources of a canadian it contractor for tax preparation, self-entry, or cpa handoff. use when the user needs to identify where business income came from, match income to supporting records, or check whether any income streams may be missing before preparing form t2125 or related t1 entries.

Bad:
- helps with income
- manages tax things
- advanced contractor workflow logic

Do not turn the description into keyword spam.

---

## Boundaries and Risk Language

Where a workflow touches tax treatment, compliance, deductibility, or legal status, the wording must be careful.

Prefer:
- organize
- flag
- ask follow-up questions
- preserve uncertainty
- recommend CPA review where needed

Avoid:
- confirm
- conclude
- determine
- guarantee
- definitely belongs
- fully deductible

Good:
- This workflow organizes facts and identifies missing support.
- Do not determine final filing positions.
- If facts remain unclear, recommend CPA review.

Bad:
- This expense belongs here.
- This amount is deductible.
- You are ready to file.

---

## Data Handling Notice

Where uploads or sensitive financial records are involved, include a short data-handling notice near the top.

Preferred baseline text:

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips or screenshots, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

Adjust only when the skill genuinely needs different wording.

Do not write long privacy disclaimers unless required.

---

## Accuracy Boundary

Where relevant, state clearly that the workflow organizes information and does not verify completeness or accuracy unless it has a true verification mechanism.

Preferred wording:
- This skill organizes information provided by the user.
- This skill does not verify completeness or accuracy.

Avoid stronger claims than the workflow can support.

---

## Stop-and-Refer Wording

When a question falls outside the workflow boundary, use consistent language.

Preferred phrase:

> That is outside what this workflow covers. It is a question for a CPA before you file.

Use this where:
- the workflow would otherwise drift into advice
- legal conclusions would be required
- filing judgment is necessary
- uncertainty is material

---

## Output Writing Rules

Outputs should be:

- clear
- structured
- plain-language where user-facing
- cautious when support is incomplete

### Internal output style
Internal outputs may be structured and technical.

### User-facing output style
User-facing outputs should be understandable to a non-practitioner.

Good:
- Business income has been identified, but one source still needs supporting records.
- Some meal expenses may relate to business activity, but more detail is needed before confident entry.

Bad:
- Gross revenue recognition state is partially unresolved.
- Deductibility posture remains indeterminate.

---

## Readiness Language

Use consistent readiness labels.

Preferred labels:
- ready for entry
- clarification required
- CPA review recommended
- incomplete
- not applicable

Do not invent alternative status language inside individual skills unless there is a strong reason.

Avoid mixing:
- approved
- acceptable
- complete enough
- looks fine
- okay to file

Use the standard labels.

---

## Naming Consistency

Keep naming consistent across:

- folder names
- frontmatter `name`
- README references
- docs references
- examples where relevant

One skill should have one name everywhere.

Prefer names that reflect function and scope.

Good:
- `collecting-tax-documents`
- `identifying-income-sources`
- `t2125-8523-meals-and-entertainment`

Avoid:
- alternate short forms in different files
- renamed variants without reason
- audience suffixes inside skill names

---

## Shared Schema References

Do not rewrite shared schema definitions inside every skill.

If a skill relies on shared structures, reference the shared files.

Use:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

Do not create slightly different local copies unless there is a real need.

---

## Examples and Templates

Examples should be realistic, not decorative.

Use examples to show:
- expected input shape
- expected output shape
- common edge cases

Do not add examples just to make the repo look more complete.

Templates should be practical and reusable.

---

## Comment and Commit Writing

When writing comments, notes, or commit messages related to the repo:

Use:
- plain English
- imperative mood for commits
- direct descriptions of the change

Good commit messages:
- Add collecting-tax-documents skill
- Refine output wording in generate-self-entry-summary
- Add shared output schema reference

Avoid:
- updated stuff
- fixes
- misc cleanup

---

## What to Avoid Across the Repository

Avoid:

- marketing language
- legalistic filler
- broad tax education sections
- overexplaining obvious points
- duplicated rules across many files
- inconsistent terminology
- speculative instructions
- vague outputs
- overconfident readiness statements

---

## Final Standard

Every file in this repository should feel like it belongs to the same system.

That means:
- same tone
- same boundaries
- same terminology
- same caution level
- same overall writing discipline

When in doubt, prefer:
- simpler wording
- clearer structure
- narrower claims
- stronger consistency