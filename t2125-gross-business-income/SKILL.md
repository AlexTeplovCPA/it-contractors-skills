---
name: t2125-gross-business-income
description: organize likely gross business income for form t2125 for a canadian it contractor. use when the user needs to map business income sources into the main t2125 income area, separate likely business income from employment or other amounts, or prepare a grouped summary for self-entry or cpa handoff after income sources have already been identified.
---

# T2125 Gross Business Income

## Purpose

Organize likely gross business income for T2125 after the income sources have already been identified.

This skill takes the organized income picture, groups the amounts that appear to relate to self-employed business activity, and prepares a structured mapping for downstream summaries.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips, screenshots, or income summaries, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- work from identified income sources, not from vague assumptions
- focus on likely business income that may belong in T2125 gross income
- separate business income from employment income, reimbursements, and unclear amounts where possible
- preserve uncertainty where support is incomplete or classification is mixed
- organize and flag, do not advise
- do not determine final filing positions
- do not conclude employment status or PSB status
- do not determine final GST/HST treatment
- do not finalize foreign currency conversion methodology if the records are incomplete

## Inputs This Skill Can Accept

Prefer any of the following:

- output from `identifying-income-sources`
- income summary spreadsheet
- bookkeeping export
- invoice summaries
- T4A slips
- platform summaries
- bank deposit summaries
- payment processor summaries

Minimum useful input:

- at least one identified income source
- some indication of whether the source appears business-related
- some support or explanation for the amount

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
- `form_context`
- `review_state`

Read from prior skill outputs where available:

- `identifying-income-sources`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Confirm that T2125 business income is relevant

Check whether the available facts suggest self-employed business activity that may belong in T2125.

Typical indicators:

- direct client invoices
- contract income outside payroll
- platform income tied to contractor work
- agency income tied to contractor work
- T4A linked to self-employed activity
- recurring client payments for IT services

If the file does not support a T2125 business income review, preserve that uncertainty and do not force a mapping.

### 2. Gather candidate business income sources

Create a working set of income sources that may belong in T2125 gross business income.

Typical candidates:

- direct client income
- platform income
- agency income that appears to relate to self-employed activity
- T4A amounts that appear connected to contractor work
- foreign client income tied to the business

Do not automatically include:

- T4 employment income
- unclear reimbursements
- mixed or unsupported deposits
- personal transfers
- receipts with no plausible business source

### 3. Separate likely business income from other amounts

Group identified amounts into these buckets:

- likely T2125 business income
- likely T1 employment income
- likely T1 slip-based non-business amount
- reimbursement or pass-through amount needing clarification
- foreign or platform income requiring separate review
- unclear or mixed amount

Do not settle mixed classification if the facts are weak.

### 4. Assess support strength

For each candidate business income source, assess support such as:

- slip
- invoice summary
- bookkeeping record
- platform summary
- deposit record
- user-prepared income summary

Mark support strength as one of:

- sufficient
- partial
- weak
- none

If the source appears real but is not well-supported, preserve it as provisional.

### 5. Build the provisional T2125 income mapping

Map supported or plausibly supported business income sources into a provisional T2125 gross business income result.

Use broad, careful mapping.

Examples of acceptable mapping logic:

- direct client invoices supported by summaries and deposits → likely include
- platform income supported by platform summary → likely include
- T4A connected to contractor work → likely include or include_with_caution
- reimbursement mixed into income → exclude_or_clarify
- unexplained deposit → exclude_or_clarify

Do not invent a final amount from incomplete support.

### 6. Flag issues that affect T2125 income readiness

Flag issues such as:

- incomplete invoice support
- platform income missing payout detail
- T4A business connection unclear
- reimbursement included in income total
- same amount may appear twice across slip and summary
- foreign currency income needs separate review
- corporate and personal activity may be mixed

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Based on the provisional T2125 income result, indicate likely downstream uses.

Common downstream uses:

- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

Do not run those workflows inside this skill.

## Output Requirements

Return the result using the shared internal output schema.

At minimum, include:

- `facts_accepted`
- `mappings_proposed`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

Also include a clear business income mapping grouped into:

- likely included in T2125 gross business income
- excluded or separately reviewed amounts
- unclear amounts needing clarification

## Status Guidance

Use:

- `ready_for_entry` when likely T2125 business income is sufficiently organized for downstream summary use
- `clarification_required` when business income is mostly identified but support or classification is incomplete
- `cpa_review_recommended` when the file is materially mixed, foreign, duplicated, or unclear
- `incomplete` when major business income support is still missing
- `not_applicable` when T2125 business income does not appear relevant from the facts provided

Do not use `ready_for_entry` if the income picture still depends heavily on unsupported explanations.

## Important Boundaries

Do not:

- treat all T4A amounts as automatically belonging in T2125
- treat all deposits as business income
- conclude employment vs contractor status
- conclude PSB status
- determine final GST/HST treatment
- determine final foreign exchange treatment from weak records
- state that the user is ready to file

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Likely Included in T2125 Gross Business Income

For each included or provisionally included source, show:

- source label
- source type
- amount if known
- support strength
- confidence level

### Excluded or Separately Reviewed Amounts

List amounts that should not be treated as straightforward T2125 business income at this stage.

### Open Questions

List only the questions that materially affect the T2125 income result.

### Readiness Result

State whether the T2125 income side is:

- ready for next step
- clarification required
- incomplete
- CPA review recommended
- not applicable

### Client-Safe Summary

Write a short plain-language summary that explains:

- what likely belongs in T2125 gross business income
- what is still unclear
- what the next step should be

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable income facts the skill relied on.

### mappings_proposed

Use mapping entries such as:

- likely include in T2125 gross business income
- include with caution
- exclude_or_clarify
- needs_manual_review

Use a T2125 field reference that stays consistent with repo standards.

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

- direct client invoice summary present
- one T4A uploaded
- Upwork income summary uploaded
- one reimbursement appears in the income log
- no complete invoice set for one smaller client

### Example Output Shape

- direct client income provisionally included in T2125 gross business income
- Upwork income provisionally included, with cross-border flag
- T4A included with caution because business link is plausible but should remain visible
- reimbursement excluded pending clarification
- one unsupported client source flagged
- status set to clarification required

## Related Downstream Uses

This skill may feed:

- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`