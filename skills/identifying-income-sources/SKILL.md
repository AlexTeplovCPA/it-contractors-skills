---
name: identifying-income-sources
description: Organize the income sources of a Canadian IT contractor before deeper field mapping begins. Use when the user needs to identify where business income came from, match income to supporting records, separate business income from other amounts, or check whether income streams may be missing before preparing T2125 or related T1 entries. Accepts slips, platform summaries, bookkeeping exports, and chat descriptions. Produces an income-source register with support status, flags, and downstream routing toward T2125, GST/HST, or summary skills.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-17
---

# Identifying Income Sources

Organize the user's income sources before deeper field mapping begins.

## Core Rules

- Organize income sources before trying to finalize field amounts.
- Identify income by channel and support, not by vague tax concepts alone.
- Do not assume deposits are income unless the user confirms the source or support exists.
- Separate business income, slip-based income, reimbursements, and unclear receipts where possible.
- Preserve uncertainty when support is incomplete.
- Organize and flag, do not advise.
- Do not determine final filing positions.
- Do not conclude employment status, contractor status, or PSB status.
- Do not invent income totals.
- Do not assume all T4A amounts belong in T2125.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- user explanation in chat
- uploaded slips such as T4A or T4
- invoice summaries
- platform summaries
- bookkeeping exports
- income summary spreadsheet
- bank deposit summaries
- payment processor summaries such as Stripe, Wise, PayPal, or Deel records

Minimum useful input:

- who paid the user
- how the user was paid
- whether any slips were received
- whether any platform or foreign income existed

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.income_channels`, `facts.slips_received`, `facts.foreign_income`, `documents.slips`, `documents.summaries`, `transactions.income_items`, `review_state`.

## Workflow

### 1. Establish the income context

Determine whether the user had:

- only self-employment income
- self-employment plus employment income
- self-employment plus slip-based contract income
- self-employment plus foreign or platform income
- reimbursements or other unclear receipts
- mixed sole proprietor and corporate activity if mentioned

If the year or business structure is unclear, keep context provisional and continue with the broadest useful intake.

### 2. Identify income channels

Group income by source, not by return line.

Common channel types:

- direct client income
- agency income
- T4A income
- T4 employment income
- platform income
- foreign client income
- processor-linked income
- reimbursements
- other or unclear receipts

For each channel, capture what is known about payer or source label, country and currency if relevant, payment method if known, and whether the source appears connected to business activity.

Do not force classification beyond what the facts support.

### 3. Match each source to available support

For each identified income source, look for support such as:

- T4 or T4A slip
- invoice summary
- bookkeeping record
- platform summary
- payment processor summary
- bank deposit record
- user-prepared income spreadsheet

Mark each support item as: `received`, `mentioned_not_provided`, `missing`, `not_applicable`, or `unclear`.

Do not treat "user remembers it" as the same as documentary support.

### 4. Separate likely business income from other amounts

Group identified amounts into:

- likely T2125 business income
- likely T1 employment income
- likely T1 slip-based non-employment income
- reimbursement or pass-through amounts needing clarification
- foreign or platform income needing separate review
- unclear receipts needing follow-up

Do not give final legal or tax conclusions. Do not settle ambiguous classification where support is weak.

### 5. Identify missing or unclear areas

Flag issues such as:

- source mentioned but no support provided
- deposit history mentioned but not tied to a source
- T4A received but business connection unclear
- foreign income mentioned without summary support
- reimbursement may be mixed into income
- same income may appear in both slip and summary records
- corporate and personal activity may be mixed

Only flag issues that matter for later mapping or readiness.

### 6. Prepare downstream routing

Indicate which downstream skills are likely relevant:

- `organizing-t2125-gross-business-income`
- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`

Do not perform those workflows here.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable income facts the skill relied on
- `mappings_proposed`: broad provisional mappings such as likely T2125 business income, likely T1 employment income, likely T1 T4A-related amount, foreign/platform income requiring separate review; do not overstate confidence
- `flags`: use `missing_support`, `mapping_uncertain`, `possible_duplication`, `cross_border_issue` where applicable; only flag items that materially affect the next step
- `open_questions`: only questions needed to resolve meaningful uncertainty
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`
- `client_safe_summary`: plain language, short and practical

Also include an income-source register grouped into:

- confirmed income sources
- mentioned but unsupported sources
- unclear or mixed sources
- likely non-business or separately reviewed sources

## Status Guidance

- `ready_for_entry`: income picture is sufficiently organized for downstream field mapping
- `clarification_required`: income sources are identified but support or classification is incomplete
- `cpa_review_recommended`: classification is materially mixed or complex
- `incomplete`: major parts of the income picture are still missing

Do not use `ready_for_entry` simply because the user described their income in general terms.

## Validation

- Income-source register covers all identified channels or marks unused ones as `not_applicable`.
- Every source has a support status, and no source is left unlabeled.
- At least one downstream skill is identified in routing.
- `status` is one of the four standard values.
- `client_safe_summary` is present and contains no tax advice.
- No provisional mapping overstates confidence where support is weak.
