---
name: organizing-t2125-gross-business-income
description: Organize likely gross business income for form T2125 for a Canadian IT contractor after income sources have already been identified. Use when the user needs to map business income sources into the T2125 gross income area, separate likely business income from employment or other amounts, or prepare a grouped mapping for self-entry or CPA handoff. Accepts prior skill output, income summaries, T4A slips, bookkeeping exports, and platform summaries. Produces a provisional T2125 income mapping with support strength, flags, and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-17
---

# T2125 Gross Business Income

Organize likely gross business income for T2125 after income sources have already been identified.

## Core Rules

- Work from identified income sources, not from vague assumptions.
- Focus on likely business income that may belong in T2125 gross income.
- Separate business income from employment income, reimbursements, and unclear amounts where possible.
- Preserve uncertainty where support is incomplete or classification is mixed.
- Organize and flag, do not advise.
- Do not determine final filing positions.
- Do not conclude employment status or PSB status.
- Do not determine final GST/HST treatment.
- Do not finalize foreign currency conversion methodology if records are incomplete.
- Do not treat all T4A amounts as automatically belonging in T2125.
- Do not treat all deposits as business income.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

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

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.income_channels`, `facts.slips_received`, `facts.foreign_income`, `documents.slips`, `documents.summaries`, `transactions.income_items`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-income-sources`.

## Workflow

### 1. Confirm that T2125 business income is relevant

Check whether available facts suggest self-employed business activity that may belong in T2125.

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
- agency income tied to self-employed activity
- T4A amounts connected to contractor work
- foreign client income tied to the business

Do not automatically include T4 employment income, unclear reimbursements, mixed or unsupported deposits, personal transfers, or receipts with no plausible business source.

### 3. Separate likely business income from other amounts

Group identified amounts into:

- likely T2125 business income
- likely T1 employment income
- likely T1 slip-based non-business amount
- reimbursement or pass-through amount needing clarification
- foreign or platform income requiring separate review
- unclear or mixed amount

Do not settle mixed classification if the facts are weak.

### 4. Assess support strength

For each candidate source, mark support as `sufficient`, `partial`, `weak`, or `none`.

If the source appears real but is not well-supported, preserve it as provisional.

### 5. Build the provisional T2125 income mapping

Map supported or plausibly supported sources into a provisional T2125 gross business income result.

Acceptable mapping logic:

- direct client invoices supported by summaries and deposits: likely include
- platform income supported by platform summary: likely include
- T4A connected to contractor work: include or include_with_caution
- reimbursement mixed into income: exclude_or_clarify
- unexplained deposit: exclude_or_clarify

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

Indicate likely downstream uses:

- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`

Do not run those workflows inside this skill.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable income facts the skill relied on
- `mappings_proposed`: use entries such as likely include in T2125 gross business income, include with caution, exclude_or_clarify, needs_manual_review; use a T2125 field reference consistent with repo standards
- `flags`: use `missing_support`, `mapping_uncertain`, `possible_duplication`, `cross_border_issue` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a business income mapping grouped into:

- likely included in T2125 gross business income (show source label, type, amount if known, support strength, confidence level)
- excluded or separately reviewed amounts
- unclear amounts needing clarification

## Status Guidance

- `ready_for_entry`: likely T2125 business income is sufficiently organized for downstream summary use
- `clarification_required`: business income is mostly identified but support or classification is incomplete
- `cpa_review_recommended`: file is materially mixed, foreign, duplicated, or unclear
- `incomplete`: major business income support is still missing
- `not_applicable`: T2125 business income does not appear relevant from the facts provided

Do not use `ready_for_entry` if the income picture still depends heavily on unsupported explanations.

## Validation

- Every candidate income source is mapped or explicitly excluded.
- Each mapping entry has a confidence level and support strength.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
- No T4 employment income is silently included in the T2125 mapping.
