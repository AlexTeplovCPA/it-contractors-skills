---
name: collecting-tax-documents
description: organize the tax documents a canadian it contractor may need for self-entry or cpa handoff. use when the user wants to gather records, prepare for tax filing, check what documents are missing, or organize their file before moving to income, expense, or gst hst review.
---

# Collecting Tax Documents

## Purpose

Organize the user’s tax document set before deeper review begins.

This skill creates a structured inventory of what the user has, what is missing, and what areas are ready or not ready for the next steps.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips, screenshots, or transaction records, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- organize documents only
- do not provide tax advice
- do not determine final filing positions
- do not assume a document exists unless the user confirms it
- separate confirmed items, mentioned-but-not-provided items, missing items, and not-applicable items
- preserve uncertainty where the file is incomplete
- keep the focus on what is needed for the next workflow step

## Inputs This Skill Can Accept

Prefer any of the following:

- user explanation in chat
- uploaded slips
- screenshots
- income summaries
- expense logs
- bookkeeping exports
- bank or card summaries
- gst hst records
- prior-year accountant summary

Minimum useful input:

- whether the user is self-employed, incorporated, or mixed
- whether they have income records
- whether they have expense records
- whether they have any tax slips

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
- `documents`
- `facts.slips_received`
- `review_state`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Establish the file context

Identify:

- tax year
- whether the user is sole proprietor, incorporated, or mixed
- whether the goal is self-entry, CPA handoff, or both

If any of this is unclear, keep the context provisional and continue with the broadest useful document checklist.

### 2. Group documents by category

Organize the file into these sections:

- personal tax slips
- business income support
- business expense support
- gst hst records
- home office support
- vehicle support
- instalment and tax payment records
- corporate or mixed-structure records if relevant

### 3. Ask only for what matters next

Use a short, structured intake sequence.

For a typical sole proprietor IT contractor, prioritize:

- T4 and T4A slips if any
- invoice or income summaries
- platform summaries such as Upwork, Stripe, Wise, PayPal, or Deel if relevant
- expense log, bookkeeping export, or transaction summary
- GST/HST registration and filing records if relevant
- RRSP slips if the user is preparing the personal return
- instalment payment records if relevant

Do not ask for documents unrelated to the user’s apparent structure or workflow goal.

### 4. Mark each item by status

For each document or record, mark it as one of:

- `received`
- `mentioned_not_provided`
- `missing`
- `not_applicable`
- `unclear`

Do not guess.

### 5. Identify blocking gaps

Flag missing items that prevent useful next steps.

Examples:

- no business income support
- no expense summary
- GST/HST mentioned but no records provided
- home office claim mentioned but no supporting details
- instalments mentioned but no payment records provided

Only flag gaps that materially affect readiness.

### 6. Prepare downstream routing

Based on the document inventory, indicate which downstream skills are likely relevant.

Common downstream uses:

- `identifying-income-sources`
- `identifying-expense-categories`
- `checking-gst-hst`
- `reviewing-instalments-and-tax-payments`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

Do not perform downstream logic inside this skill.  
Only prepare the file.

## Output Requirements

Return the result using the shared internal output schema.

At minimum, include:

- `facts_accepted`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

Also include a clear document inventory grouped into:

- confirmed documents
- mentioned but not provided
- missing items
- not applicable items

## Status Guidance

Use:

- `ready_for_entry` when the document set appears strong enough for the next structured review step
- `clarification_required` when the document set is partially present but key items are still missing
- `incomplete` when major parts of the file are missing
- `cpa_review_recommended` when the structure is unusually mixed or unclear

Do not use `ready_for_entry` simply because the user says they have “most documents.”

## Important Boundaries

Do not:

- conclude that the user is ready to file
- say that missing documents are unnecessary
- determine deductibility or compliance positions
- decide GST/HST treatment
- decide PSB status
- conclude whether employment vs business classification is settled

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Document Inventory

Group items by category and status.

### Missing Items

List only the items that matter for the next step.

### Open Questions

List only useful unresolved questions.

### Readiness Result

State whether the file is:

- ready for next step
- needs clarification
- incomplete
- CPA review recommended

### Client-Safe Summary

Write a short plain-language summary of the current file state.

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable file-level facts the skill relied on.

### flags

Use standardized flags such as:

- `missing_support`
- `mapping_uncertain`
- `cross_border_issue`

Only use flags that materially affect the next step.

### open_questions

Ask only the questions needed to move the file forward.

### status

End with one of the repository standard result values.

### client_safe_summary

Use plain language. Keep it short and practical.

## Example

### Example Input

- user has one T4A
- user has a spreadsheet of income
- user has an expense log
- user mentioned GST/HST registration
- user has no instalment payment records yet

### Example Output Shape

- tax slips grouped under personal tax slips
- income spreadsheet grouped under business income support
- expense log grouped under business expense support
- GST/HST records marked as missing
- instalment records marked as missing
- status set to clarification required
- downstream routing prepared for income, expense, and gst hst review

## Related Downstream Uses

This skill may feed:

- `identifying-income-sources`
- `identifying-expense-categories`
- `checking-gst-hst`
- `reviewing-instalments-and-tax-payments`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

## References

See:
- `references/checklist-t1.md`
- `references/checklist-t2125.md`
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`