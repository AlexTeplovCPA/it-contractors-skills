---
name: identifying-income-sources
description: organize the income sources of a canadian it contractor for tax preparation, self-entry, or cpa handoff. use when the user needs to identify where business income came from, match income to supporting records, separate business income from other amounts, or check whether any income streams may be missing before preparing t2125 or related t1 entries.
---

# Identifying Income Sources

## Purpose

Organize the user’s income sources before deeper field mapping begins.

This skill identifies how money came in during the tax year, groups income by source, links each source to available support, and flags missing or unclear areas that may affect later T2125 or T1 preparation.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips or screenshots, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- organize income sources before trying to finalize field amounts
- identify income by channel and support, not by vague tax concepts alone
- do not assume deposits are income unless the user confirms the source or support exists
- separate business income, slip-based income, reimbursements, and unclear receipts where possible
- preserve uncertainty when support is incomplete
- organize and flag, do not advise
- do not determine final filing positions
- do not conclude employment status, contractor status, or PSB status

## Inputs This Skill Can Accept

Prefer any of the following:

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

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
- `facts.business_activity`
- `facts.income_channels`
- `facts.slips_received`
- `facts.foreign_income`
- `documents.slips`
- `documents.summaries`
- `transactions.income_items`
- `review_state`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Establish the income context

Identify the broad pattern first.

Determine whether the user had:

- only self-employment income
- self-employment plus employment income
- self-employment plus slip-based contract income
- self-employment plus foreign or platform income
- reimbursements or other unclear receipts
- mixed sole proprietor and corporate activity if mentioned

If the year or business structure is unclear, keep the context provisional and continue with the broadest useful intake.

### 2. Identify income channels

Group income by source, not by return line.

Common channel types include:

- direct client income
- agency income
- T4A income
- T4 employment income
- platform income
- foreign client income
- processor-linked income
- reimbursements
- other or unclear receipts

For each channel, capture what is known about:

- payer or source label
- country if relevant
- currency if relevant
- payment method if known
- whether the source appears connected to business activity

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

Mark each support item by status:

- received
- mentioned_not_provided
- missing
- not_applicable
- unclear

Do not treat “user remembers it” as the same as documentary support.

### 4. Separate likely business income from other amounts

Use the available facts to organize likely routing.

Typical buckets:

- likely T2125 business income
- likely T1 employment income
- likely T1 slip-based non-employment income
- reimbursement or pass-through amounts needing clarification
- foreign or platform income needing separate review
- unclear receipts needing follow-up

Do not give final legal or tax conclusions.  
Do not settle ambiguous classification where support is weak.

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

Based on the organized income picture, indicate which downstream skills are likely relevant.

Common downstream uses:

- `t2125-gross-business-income`
- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

Do not perform those workflows here.  
Only prepare the income side of the file for them.

## Output Requirements

Return the result using the shared internal output schema.

At minimum, include:

- `facts_accepted`
- `mappings_proposed`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

Also include a clear income-source register grouped into:

- confirmed income sources
- mentioned but unsupported sources
- unclear or mixed sources
- likely non-business or separately reviewed sources

## Status Guidance

Use:

- `ready_for_entry` when the income picture appears sufficiently organized for downstream field mapping
- `clarification_required` when income sources are identified but support or classification is incomplete
- `cpa_review_recommended` when classification is materially mixed or complex
- `incomplete` when major parts of the income picture are still missing

Do not use `ready_for_entry` simply because the user described their income in general terms.

## Important Boundaries

Do not:

- invent income totals
- assume all deposits are income
- assume all T4A amounts belong in T2125
- conclude employment vs contractor status
- conclude PSB status
- determine final GST/HST treatment
- state that the user is ready to file

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Income Source Register

For each source, show:

- source label
- channel type
- slip or non-slip
- currency if relevant
- support status
- likely downstream area

### Missing Support

List only the missing records that materially affect the next step.

### Open Questions

List only useful unresolved questions.

### Readiness Result

State whether the income side of the file is:

- ready for next step
- clarification required
- incomplete
- CPA review recommended

### Client-Safe Summary

Write a short plain-language summary that explains:

- what income sources were identified
- what is still missing or unclear
- what the next step should be

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable income facts the skill relied on.

### mappings_proposed

Use broad, provisional mappings where supported, such as:

- likely T2125 business income
- likely T1 employment income
- likely T1 T4A-related amount
- foreign/platform income requiring separate review

Do not overstate confidence.

### flags

Use standardized flags such as:

- `missing_support`
- `mapping_uncertain`
- `possible_duplication`
- `cross_border_issue`

### open_questions

Ask only the questions needed to resolve meaningful uncertainty.

### status

End with one of the repository standard result values.

### client_safe_summary

Use plain language. Keep it short and practical.

## Example

### Example Input

- User had two direct clients
- User received one T4A
- User had Upwork income in USD
- User is unsure whether one reimbursed software payment was included in income
- User has an uploaded T4A and a platform summary, but no complete invoice set

### Example Output Shape

- direct client income identified but support incomplete
- T4A identified and linked to a likely income source
- Upwork income identified as foreign/platform income
- reimbursement flagged for clarification
- status set to clarification required
- downstream routing to T2125 gross income and foreign/platform income review

## Related Downstream Uses

This skill may feed:

- `t2125-gross-business-income`
- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`