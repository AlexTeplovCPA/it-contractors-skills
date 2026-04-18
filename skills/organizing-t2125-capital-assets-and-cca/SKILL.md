---
name: organizing-t2125-capital-assets-and-cca
description: Organize capital asset facts and capital cost allowance information for form T2125 for a Canadian IT contractor. Use when the user has purchased equipment, computers, software, or other assets that may require CCA treatment rather than immediate expensing. Accepts prior skill output, purchase records, and asset descriptions. Produces a provisional capital asset mapping with CCA class candidates, support strength, flags, and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# T2125 Capital Assets and CCA

Organize capital asset facts and CCA information for T2125 after the broader expense picture has already been identified.

## Core Rules

- Work from actual purchase facts, not assumptions.
- Focus on items that may require capital treatment rather than immediate expensing.
- Separate likely capital items from routine operating expenses.
- Preserve uncertainty where capital vs current treatment is unclear.
- Organize and flag, do not advise.
- Do not determine final CCA rates or calculations.
- Do not determine final GST/HST treatment.
- Do not finalize CCA class assignments.
- Do not assume a business-use percentage without support.
- Do not state that an asset is definitely deductible or at a stated rate.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `identifying-expense-categories`
- output from `organizing-t2125-routine-operating-expenses`
- purchase receipts or invoices
- asset list or equipment description
- prior year CCA schedule if available
- user explanation in chat

Minimum useful input:

- at least one item that may qualify as a capital asset
- approximate purchase cost and date
- description of what the item is

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `documents.expense_support`, `transactions.expense_items`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-expense-categories`, `organizing-t2125-routine-operating-expenses`.

## Workflow

### 1. Confirm capital asset review is relevant

Check whether available facts suggest the user acquired items during the year that may require capital treatment.

Typical indicators: computer equipment, peripherals, software licenses, office furniture, vehicles used for business, or other items with multi-year useful life.

If the file does not support a capital asset review, preserve that uncertainty and do not force a mapping.

### 2. Build the candidate capital asset set

Create a working set of items that may require CCA treatment:

- computers and laptops
- monitors and peripherals
- phones used for business
- office furniture and equipment
- software with a multi-year license
- vehicles used for business
- other items with a useful life beyond the current year

Do not automatically include: low-cost items that are likely routine supplies, fully personal items, items with unclear business use.

### 3. Extract key facts for each candidate item

For each candidate, identify: description, purchase date, cost, receipt or invoice status, business-use percentage if stated, and any prior-year CCA history if relevant.

Do not invent missing details.

### 4. Note likely CCA class candidates

For each item, note the likely CCA class category in general terms:

- computer equipment (commonly Class 10 or 50 area)
- software (commonly Class 12 area)
- furniture and fixtures (commonly Class 8 area)
- vehicles (commonly Class 10 or 10.1 area)
- other

Do not assign final class numbers or rates. Flag that final class assignment requires CPA review.

### 5. Assess support strength

For each candidate item, mark support as `sufficient`, `partial`, `weak`, or `none`.

Mixed-use items should be noted as requiring an allocation.

### 6. Build the provisional capital asset mapping

Map candidate items into one of:

- likely capital item
- include with caution
- exclude_or_clarify
- needs_manual_review
- not_applicable

Note items where business-use percentage has not been stated.

### 7. Flag issues that affect readiness

Flag issues such as:

- receipt or invoice missing
- business-use percentage not stated
- item may be fully personal
- item may have been expensed in prior year
- prior-year CCA schedule not available
- item cost may require half-year rule consideration
- vehicle with personal use requires additional facts

Only flag issues that materially affect readiness.

### 8. Prepare downstream routing

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

- `facts_accepted`: usable asset facts the skill relied on
- `mappings_proposed`: use entries such as likely capital item, include with caution, exclude_or_clarify, needs_manual_review, not_applicable; note likely CCA class area where identifiable
- `flags`: use `missing_support`, `mapping_uncertain`, `possible_personal_component`, `unclear_classification` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: What was the purchase date? What is the total cost? Do you have a receipt? What percentage of use is for business?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a capital asset mapping grouped into:

- likely capital items (show description, cost if known, likely CCA class area, business-use percentage if stated, support strength)
- excluded or separately reviewed items
- unclear items needing clarification

## Status Guidance

- `ready_for_entry`: capital asset facts are sufficiently organized for downstream summary use
- `clarification_required`: some capital items are identified but cost, use percentage, or support is incomplete
- `cpa_review_recommended`: file includes material classification uncertainty, mixed-use assets, or missing prior-year schedule
- `incomplete`: major capital asset facts are still missing
- `not_applicable`: capital asset review does not appear relevant from the facts provided

Do not use `ready_for_entry` if business-use percentages are missing for mixed-use assets or if prior-year CCA is relevant but not available.

## Validation

- Every candidate item is mapped or explicitly excluded.
- Each included item has a cost, purchase date, and support strength noted or flagged as missing.
- Business-use percentage is stated or flagged as unresolved for mixed-use items.
- CCA class area is noted in general terms and flagged for CPA confirmation.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
