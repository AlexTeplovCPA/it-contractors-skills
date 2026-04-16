---
name: identifying-expense-categories
description: organize the expense categories of a canadian it contractor for tax preparation, self-entry, or cpa handoff. use when the user needs to sort business expenses into major buckets, identify possible capital items, separate mixed or unclear spending, or check what expense support is missing before preparing t2125 fields or related summaries.
---

# Identifying Expense Categories

## Purpose

Organize the user’s expense universe before deeper field mapping begins.

This skill groups expenses into practical categories, identifies missing or weak support, separates likely current expenses from possible capital items, and prepares the file for downstream T2125 field review.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips, screenshots, receipts, or transaction exports, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- organize expenses before trying to finalize field-level treatment
- group expenses by practical category first, not by guesswork about final deductibility
- separate likely routine expenses from possible capital items
- preserve uncertainty where support is incomplete or mixed
- identify missing or weak support that affects downstream review
- organize and flag, do not advise
- do not determine final deductibility
- do not determine final GST/HST treatment
- do not force every expense into a final T2125 line at this stage

## Inputs This Skill Can Accept

Prefer any of the following:

- expense log or CSV
- bookkeeping export
- bank or card transaction summaries
- uploaded receipts
- screenshots
- user explanation in chat
- vendor/category spreadsheet

Minimum useful input:

- vendor or expense description
- amount
- date or approximate timing
- user explanation of what the expense was for

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
- `facts.business_activity`
- `facts.home_office`
- `facts.vehicle_use`
- `documents.expense_support`
- `transactions.expense_items`
- `review_state`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Establish the expense context

Identify the broad expense pattern first.

Determine whether the file appears to include:

- routine operating expenses
- meals and entertainment
- travel
- home office related costs
- vehicle-related costs
- professional fees
- subcontractor or outside service costs
- one-time equipment or possible capital items
- other unclear or mixed expenses

If the source data is incomplete, continue with the broadest useful categorization and preserve uncertainty.

### 2. Group expenses into practical categories

Sort expenses into major working categories such as:

- software and cloud tools
- office and admin expenses
- internet and phone
- meals and entertainment
- travel
- professional fees
- subcontractors and outside services
- workspace or rent-related costs
- home office related costs
- vehicle-related costs
- equipment and possible capital items
- unclear or other expenses

Use practical grouping first. Do not force a final tax treatment unless the category is clearly obvious and low-risk.

### 3. Assess support quality

For each category or item, identify what support exists.

Examples:

- receipt
- invoice
- bookkeeping entry
- expense log entry
- bank or card record
- user explanation only

Mark support status as one of:

- received
- mentioned_not_provided
- missing
- not_applicable
- unclear

Do not treat weak memory-based descriptions as strong support.

### 4. Separate likely routine expenses from possible capital items

Identify expenses that may require a later capital review.

Common examples:

- laptop purchases
- monitors
- phones
- desks or office furniture
- equipment bundles
- other large one-time purchases

Do not finalize the treatment here. Route likely capital items forward for later review.

### 5. Flag mixed or unclear items

Flag issues such as:

- personal and business use may be mixed
- business purpose unclear
- category unclear
- same charge may appear duplicated
- one expense may belong in a different review area
- home office or internet costs may require allocation
- meal or travel wording is too weak to rely on directly

Only flag issues that matter for downstream mapping or readiness.

### 6. Prepare downstream routing

Based on the organized expense picture, indicate which downstream skills are likely relevant.

Common downstream uses:

- `t2125-routine-operating-expenses`
- `t2125-8523-meals-and-entertainment`
- `t2125-business-use-of-home`
- `t2125-capital-assets-and-cca`
- `t2125-other-expenses-review`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

Do not run downstream logic inside this skill.  
Only prepare the expense side of the file for later review.

## Output Requirements

Return the result using the shared internal output schema.

At minimum, include:

- `facts_accepted`
- `mappings_proposed`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

Also include a clear expense category map grouped into:

- confirmed categories
- possible capital items
- mixed or unclear items
- missing-support items

## Status Guidance

Use:

- `ready_for_entry` when the expense picture appears sufficiently organized for downstream field mapping
- `clarification_required` when categories are mostly identified but support or classification is incomplete
- `cpa_review_recommended` when the expense picture includes material mixed-use, capital, or unclear items
- `incomplete` when major expense information is still missing

Do not use `ready_for_entry` if significant categories remain weakly supported or materially unclear.

## Important Boundaries

Do not:

- determine final deductibility
- state that a category is definitely allowable
- finalize capital vs current treatment where uncertainty remains
- determine final GST/HST treatment
- conclude that mixed-use items are fully business
- state that the user is ready to file

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Expense Category Map

For each category, show:

- category label
- representative items or examples
- support status
- likely downstream area

### Possible Capital Items

List items that may need separate capital review.

### Mixed or Unclear Items

List only the items that materially affect the next step.

### Open Questions

List only useful unresolved questions.

### Readiness Result

State whether the expense side of the file is:

- ready for next step
- clarification required
- incomplete
- CPA review recommended

### Client-Safe Summary

Write a short plain-language summary that explains:

- what categories were identified
- what still looks unclear
- what the next step should be

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable expense facts the skill relied on.

### mappings_proposed

Use broad, provisional mappings where supported, such as:

- likely routine operating expenses
- likely meals and entertainment
- likely home office related costs
- likely capital items requiring separate review
- likely unclear or other expenses

Do not overstate confidence.

### flags

Use standardized flags such as:

- `missing_support`
- `mapping_uncertain`
- `possible_personal_component`
- `possible_capital_item`
- `possible_duplication`

### open_questions

Ask only the questions needed to resolve meaningful uncertainty.

### status

End with one of the repository standard result values.

### client_safe_summary

Use plain language. Keep it short and practical.

## Example

### Example Input

- user uploaded an expense log
- recurring AWS and GitHub charges appear in the file
- one restaurant charge is described as a client dinner
- internet bills may be partly personal and partly business
- one laptop purchase appears in the transaction list
- one coffee meeting has no receipt

### Example Output Shape

- routine software and cloud expenses identified
- meal expense grouped separately
- internet expenses flagged as possibly mixed-use
- laptop purchase flagged as a possible capital item
- one item missing support
- status set to clarification required
- downstream routing to routine expenses, meals, and capital-assets review

## Related Downstream Uses

This skill may feed:

- `t2125-routine-operating-expenses`
- `t2125-8523-meals-and-entertainment`
- `t2125-business-use-of-home`
- `t2125-capital-assets-and-cca`
- `t2125-other-expenses-review`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`