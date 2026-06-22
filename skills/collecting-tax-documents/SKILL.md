---
name: collecting-tax-documents
description: Organize the tax document set for a Canadian IT contractor before deeper review begins. Use when the user wants to gather records, check what is missing, prepare for CPA handoff, or organize their file before moving to income, expense, or GST/HST review. Accepts slips, summaries, exports, and chat descriptions. Produces a grouped document inventory with status, blocking gaps, and downstream routing toward income, expense, GST/HST, instalments, or summary skills.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-17
---

# Collecting Tax Documents

Organize the user's tax document set before deeper review begins.

## Core Rules

- Organize documents only.
- Do not provide tax advice.
- Do not determine final filing positions.
- Do not assume a document exists unless the user confirms it.
- Separate confirmed items, mentioned-but-not-provided items, missing items, and not-applicable items.
- Preserve uncertainty where the file is incomplete.
- Do not conclude the user is ready to file.
- Do not say missing documents are unnecessary.
- Do not decide deductibility, GST/HST treatment, PSB status, or employment vs. business classification.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- user explanation in chat
- uploaded slips
- screenshots
- income summaries
- expense logs
- bookkeeping exports
- bank or card summaries
- GST/HST records
- prior-year accountant summary

Minimum useful input:

- whether the user is self-employed, incorporated, or mixed
- whether they have income records
- whether they have expense records
- whether they have any tax slips

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `documents`, `facts.slips_received`, `review_state`.

## Workflow

### 1. Establish file context

Identify:

- tax year
- whether the user is sole proprietor, incorporated, or mixed
- whether the goal is self-entry, CPA handoff, or both

If unclear, keep context provisional and continue with the broadest useful document checklist.

### 2. Group documents by category

Organize into:

- personal tax slips
- business income support
- business expense support
- GST/HST records
- home office support
- vehicle support
- instalment and tax payment records
- corporate or mixed-structure records if relevant

### 3. Ask only for what matters next

For a typical sole proprietor IT contractor, prioritize:

- T4 and T4A slips if any
- invoice or income summaries
- platform summaries such as Upwork, Stripe, Wise, PayPal, or Deel if relevant
- expense log, bookkeeping export, or transaction summary
- GST/HST registration and filing records if relevant
- RRSP slips if the user is preparing the personal return
- instalment payment records if relevant

Do not ask for documents unrelated to the user's apparent structure or workflow goal.

### 4. Mark each item by status

For each document or record, mark as one of:

- `received`
- `mentioned_not_provided`
- `missing`
- `not_applicable`
- `unclear`

Do not guess.

### 5. Identify blocking gaps

Flag missing items that prevent useful next steps:

- no business income support
- no expense summary
- GST/HST mentioned but no records provided
- home office claim mentioned but no supporting details
- instalments mentioned but no payment records provided

Only flag gaps that materially affect readiness.

### 6. Prepare downstream routing

Indicate which downstream skills are likely relevant:

- `identifying-income-sources`
- `identifying-expense-categories`
- `checking-gst-hst`
- `reviewing-instalments-and-tax-payments`
- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`

Do not perform downstream logic inside this skill.

## Resource Map

- `references/checklist-t1.md`: read when reviewing personal slip completeness
- `references/checklist-t2125.md`: read when reviewing business income or expense support
- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: file-level facts the skill relied on
- `flags`: use `missing_support`, `mapping_uncertain`, `cross_border_issue` where applicable; only flag items that materially affect the next step
- `open_questions`: only questions needed to move the file forward
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`
- `client_safe_summary`: plain language, short and practical

Also include a document inventory grouped into:

- confirmed documents
- mentioned but not provided
- missing items
- not applicable items

## Status Guidance

- `ready_for_entry`: document set is strong enough for the next structured review step
- `clarification_required`: file is partially present but key items are still missing
- `incomplete`: major parts of the file are missing
- `cpa_review_recommended`: structure is unusually mixed or unclear

Do not use `ready_for_entry` simply because the user says they have "most documents."

## Validation

- Document inventory covers all eight categories or marks unused ones as `not_applicable`.
- Every item has a status, and no item is left unlabeled.
- At least one downstream skill is identified in routing.
- `status` is one of the four standard values.
- `client_safe_summary` is present and contains no tax advice.
- If `ready_for_entry`, confirm no blocking gaps remain.
