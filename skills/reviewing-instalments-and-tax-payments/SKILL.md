---
name: reviewing-instalments-and-tax-payments
description: Review tax instalment payments and prior tax balances for a Canadian IT contractor. Use when the user made quarterly tax instalments during the year, has a prior-year balance owing, or needs to organize tax payment facts for T1 entry or CPA handoff. Accepts prior skill output, CRA notices, and payment records. Produces a provisional instalment and tax payment summary with flags and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Reviewing Instalments and Tax Payments

Review tax instalment payments and prior tax payment facts for a Canadian IT contractor.

## Core Rules

- Organize and flag instalment and payment facts, do not advise on instalment obligations.
- Do not calculate instalment interest or penalties.
- Do not determine whether the user's instalments were sufficient.
- Do not determine the final balance owing or refund.
- Preserve uncertainty where payment dates, amounts, or CRA records are incomplete.
- Do not state that the user's instalments are correct or sufficient.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- CRA instalment reminder notices
- bank records showing tax payments
- My Account payment history description
- prior year T1 return summary
- user explanation in chat

Minimum useful input:

- at least one tax payment made during the year
- approximate date and amount

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.tax_payments`, `documents.cra_notices`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-income-sources`, `organizing-t2125-gross-business-income`.

## Workflow

### 1. Confirm instalment review is relevant

Check whether the user made tax payments during the year or received instalment reminders from CRA. If no payments were made and no reminders received, note this and return an appropriate status.

### 2. Organize instalment payment facts

For each payment, identify:

- approximate payment date
- approximate amount
- payment method if known
- whether the payment matches a CRA instalment reminder amount

Do not reconstruct payment history from incomplete information.

### 3. Organize prior-year balance facts

Identify:

- whether there was a prior-year balance owing
- approximate amount if known
- whether it was paid by the filing deadline

Note that prior-year balances paid after the deadline may carry interest.

### 4. Assess support strength

For each payment, mark support as `sufficient`, `partial`, `weak`, or `none`.

If the user is relying on memory rather than bank records or CRA notices, mark support accordingly.

### 5. Build the provisional payment summary

Summarize:

- total instalment payments made during the year
- prior-year balance paid
- any payments that cannot be confirmed

Map into:

- confirmed payments
- provisional payments (stated but not documented)
- missing or unconfirmed payments

### 6. Flag issues that affect readiness

Flag issues such as:

- payment dates or amounts not confirmed
- CRA instalment reminders not available
- total instalments may be insufficient relative to expected tax
- payment may have been applied to a different period
- prior-year balance payment date unclear

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Indicate likely downstream uses:

- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

Do not run those workflows inside this skill.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable payment facts the skill relied on
- `mappings_proposed`: use entries such as confirmed instalment, provisional instalment, prior-year balance payment, unconfirmed, not_applicable
- `flags`: use `missing_support`, `mapping_uncertain` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: Do you have bank records showing the payment dates and amounts? Did you receive instalment reminders from CRA? Was there a balance owing from the prior year?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a payment summary grouped into:

- confirmed instalment payments (date, amount, support strength)
- provisional or unconfirmed payments
- prior-year balance payment if applicable
- open issues

## Status Guidance

- `ready_for_entry`: instalment and payment facts are sufficiently organized for downstream summary use
- `clarification_required`: some payments are identified but dates, amounts, or support is incomplete
- `cpa_review_recommended`: file includes material payment uncertainty or possible instalment shortfall
- `incomplete`: key payment facts are missing
- `not_applicable`: no instalment payments identified and no prior-year balance

Do not use `ready_for_entry` if payment amounts or dates are unconfirmed.

## Validation

- Every identified payment is listed with date, amount, and support strength or flagged as missing.
- Prior-year balance is noted or flagged as not applicable.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
