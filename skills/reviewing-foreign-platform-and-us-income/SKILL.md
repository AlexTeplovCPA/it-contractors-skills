---
name: reviewing-foreign-platform-and-us-income
description: Review foreign income, US-source income, and platform income facts for a Canadian IT contractor. Use when the user earns income from US clients, foreign platforms, or non-Canadian sources and needs to organize amounts, withholding, and reporting facts for T1 and T2125 entry or CPA handoff. Accepts prior skill output, platform payment records, and foreign tax documents. Produces a provisional foreign income summary with source flags, withholding notes, and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Reviewing Foreign Platform and US Income

Review foreign income, US-source income, and platform income facts for a Canadian IT contractor.

## Core Rules

- Organize and flag foreign income facts, do not advise on treaty positions or residency.
- Do not determine final foreign tax credit entitlement.
- Do not determine final treaty treatment.
- Do not convert amounts using a rate you select; note the need for an annual average or transaction-date rate.
- Preserve uncertainty where income source, currency, or withholding facts are incomplete.
- Do not state that foreign income is or is not taxable in Canada.
- Do not state that a treaty exemption applies.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `identifying-income-sources`
- output from `organizing-t2125-gross-business-income`
- platform payment summaries (e.g. Upwork, Toptal, Stripe, PayPal)
- US 1099 forms or equivalent
- wire transfer or payment records
- user explanation in chat

Minimum useful input:

- at least one income item from a foreign source or foreign platform
- approximate amount and currency

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.foreign_income`, `documents.income_records`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-income-sources`, `organizing-t2125-gross-business-income`.

## Workflow

### 1. Confirm foreign income review is relevant

Check whether the user has income from sources outside Canada. If all income appears Canadian, return not_applicable.

### 2. Identify foreign income sources

For each foreign income item, identify:

- platform or payer name
- country of source
- currency
- approximate amount
- whether a 1099 or equivalent foreign tax document exists
- whether withholding was applied

### 3. Organize currency conversion facts

Note that Canadian tax reporting requires amounts in Canadian dollars. Flag items where:

- the currency conversion rate has not been stated
- amounts are given in USD or another foreign currency only
- the user has not indicated which conversion method they intend to use

Do not select a conversion rate. Note that the Bank of Canada annual average rate is commonly used.

### 4. Organize withholding facts

For each income source, identify:

- whether foreign tax was withheld
- the approximate withholding amount if known
- whether a foreign tax credit may be available

Do not calculate the foreign tax credit. Flag for CPA review where withholding appears material.

### 5. Note T1 and T2125 reporting implications

Identify which forms may be relevant:

- T2125 for foreign self-employment income
- T1 line for foreign employment income if applicable
- T1135 if foreign property may be relevant (flag only, do not assess)

Do not conclude which lines apply. Flag ambiguity for CPA review.

### 6. Assess support strength

For each income source, mark support as `sufficient`, `partial`, `weak`, or `none`.

### 7. Flag issues that affect readiness

Flag issues such as:

- 1099 or foreign tax slip not available
- withholding amount unclear
- currency conversion not addressed
- income source classification uncertain
- T1135 may be relevant
- treaty position may affect treatment

Only flag issues that materially affect readiness.

### 8. Prepare downstream routing

Indicate likely downstream uses:

- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`
- `generating-self-entry-summary`

Do not run those workflows inside this skill.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable foreign income facts the skill relied on
- `mappings_proposed`: use entries such as include in T2125 gross income, include with caution, exclude_or_clarify, needs_manual_review, not_applicable; note currency and withholding facts
- `flags`: use `missing_support`, `cross_border_issue`, `mapping_uncertain`, `gst_hst_issue` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: What currency were you paid in? Was any tax withheld? Do you have a 1099 or equivalent document?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a foreign income summary grouped into:

- identified foreign income sources (show platform or payer, country, currency, approximate amount, withholding if known, support strength)
- currency conversion status
- withholding and foreign tax credit notes
- open issues

## Status Guidance

- `ready_for_entry`: foreign income facts are sufficiently organized for downstream summary use
- `clarification_required`: some foreign income is identified but currency, withholding, or support is incomplete
- `cpa_review_recommended`: file includes treaty uncertainty, material withholding, or T1135 indicators
- `incomplete`: key foreign income documents are missing
- `not_applicable`: no foreign income identified

Do not use `ready_for_entry` if currency conversion facts are unresolved or withholding amounts are unknown.

## Validation

- Every foreign income source is listed and mapped or flagged.
- Currency conversion need is noted for each non-CAD item.
- Withholding status is noted for each source.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
