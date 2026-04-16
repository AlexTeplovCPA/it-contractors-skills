---
name: t2125-8523-meals-and-entertainment
description: organize likely meals and entertainment expenses for line 8523 of form t2125 for a canadian it contractor. use when the user needs to review restaurant, coffee meeting, client meal, or similar expenses, separate likely business meals from personal or unclear charges, or prepare a structured summary for self-entry or cpa handoff after expense categories have already been identified.
---

# T2125 8523 Meals and Entertainment

## Purpose

Organize likely meals and entertainment expenses for line 8523 of T2125 after the broader expense picture has already been identified.

This skill reviews candidate meal and entertainment expenses, separates likely business-related items from personal or unclear items, identifies missing support, and prepares a structured mapping for downstream summaries.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading receipts, screenshots, or transaction exports, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- work from identified expense categories, not from vague assumptions
- focus on likely meal and entertainment expenses that may belong in T2125 line 8523
- separate likely business meals from personal, mixed, unsupported, or unclear charges
- preserve uncertainty where support is incomplete or business purpose is weak
- organize and flag, do not advise
- do not determine final deductibility
- do not determine final GST/HST treatment
- do not assume every restaurant or cafe charge is business-related
- do not force unsupported items into line 8523

## Inputs This Skill Can Accept

Prefer any of the following:

- output from `identifying-expense-categories`
- expense log or CSV
- uploaded receipts
- bank or card transaction summaries
- user explanation in chat
- bookkeeping export

Minimum useful input:

- vendor or description suggesting a meal or entertainment cost
- amount
- some explanation of what the expense was for

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
- `facts.business_activity`
- `documents.expense_support`
- `transactions.expense_items`
- `form_context`
- `review_state`

Read from prior skill outputs where available:

- `identifying-expense-categories`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Confirm that meals and entertainment review is relevant

Check whether the available facts suggest one or more expenses that may belong in T2125 line 8523.

Typical indicators:

- restaurant charges
- cafe or coffee meeting charges
- client dinner or lunch charges
- food delivery charges described as business-related
- entertainment charges tied to business meetings or client interaction

If the file does not support a meals and entertainment review, preserve that uncertainty and do not force a mapping.

### 2. Build the candidate meals and entertainment set

Create a working set of expenses that may belong in line 8523.

Typical candidates:

- restaurant meals
- coffee meetings
- client lunches or dinners
- food delivery expenses claimed as business-related
- entertainment-type charges with a stated business purpose

Do not automatically include:

- undocumented personal meals
- groceries with no business context
- travel costs that are only transport or accommodation
- mixed retail purchases where the meal component is unclear
- charges with no plausible business purpose

### 3. Extract key facts for each candidate item

For each candidate item, identify what is known about:

- vendor
- date
- amount
- description
- receipt status
- business purpose explanation
- whether attendees are known
- whether the charge may include a personal component

Keep this factual.  
Do not invent missing details.

### 4. Assess support strength

For each candidate item, assess support such as:

- receipt
- card or bank record
- user explanation
- calendar or meeting note if mentioned
- bookkeeping record

Mark support strength as one of:

- sufficient
- partial
- weak
- none

A receipt alone may still be weak if business purpose is not clear.

### 5. Build the provisional line 8523 mapping

Map candidate items into one of these treatments:

- likely include in line 8523
- include with caution
- exclude_or_clarify
- needs_manual_review
- not_applicable

Use line reference `8523` when the item appears to belong in Meals and entertainment.

Use broad, careful mapping.  
Do not overstate confidence.

### 6. Flag issues that affect line 8523 readiness

Flag issues such as:

- no receipt
- business purpose unclear
- attendee information missing where relevant
- personal and business use may be mixed
- charge may belong in another category
- charge appears duplicated
- support is too weak to rely on directly

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Based on the provisional line 8523 result, indicate likely downstream uses.

Common downstream uses:

- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`
- `generate-missing-items-summary`

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

Also include a clear meals and entertainment mapping grouped into:

- likely included in line 8523
- excluded or separately reviewed items
- unclear items needing clarification

## Status Guidance

Use:

- `ready_for_entry` when likely line 8523 items are sufficiently organized for downstream summary use
- `clarification_required` when meal-related items are identified but support or business purpose is incomplete
- `cpa_review_recommended` when the file includes material mixed-use, unclear business purpose, or repeated weak support
- `incomplete` when major meal-related support is still missing
- `not_applicable` when line 8523 review does not appear relevant from the facts provided

Do not use `ready_for_entry` if the business purpose of key items remains unclear.

## Important Boundaries

Do not:

- determine final deductibility
- state that a restaurant or meal charge is definitely allowable
- treat all cafe or restaurant charges as business expenses
- determine final GST/HST treatment
- state that the user is ready to file

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Likely Included in Line 8523

For each included or provisionally included item, show:

- vendor or item label
- amount if known
- support strength
- confidence level

### Excluded or Separately Reviewed Items

List amounts that should not be treated as straightforward line 8523 expenses at this stage.

### Open Questions

List only the questions that materially affect the line 8523 result.

### Readiness Result

State whether the line 8523 side is:

- ready for next step
- clarification required
- incomplete
- CPA review recommended
- not applicable

### Client-Safe Summary

Write a short plain-language summary that explains:

- what likely belongs in meals and entertainment
- what is still unclear
- what the next step should be

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable expense facts the skill relied on.

### mappings_proposed

Use mapping entries such as:

- likely include in 8523
- include with caution
- exclude_or_clarify
- needs_manual_review
- not_applicable

Use field reference `8523`.

### flags

Use standardized flags such as:

- `missing_support`
- `mapping_uncertain`
- `possible_personal_component`
- `possible_duplication`

### open_questions

Ask only the questions needed to resolve meaningful uncertainty.

Typical useful questions:

- What was the business purpose of this meal?
- Who attended?
- Do you have the receipt?
- Was any personal portion included?

### status

End with one of the repository standard result values.

### client_safe_summary

Use plain language. Keep it short and practical.

## Example

### Example Input

- one restaurant charge described as a client dinner
- one coffee meeting charge with no receipt
- one food delivery charge with no clear business explanation

### Example Output Shape

- restaurant charge provisionally included in line 8523
- coffee meeting charge included with caution or flagged for clarification
- food delivery charge excluded_or_clarify
- one flag for missing support
- one flag for unclear business purpose
- status set to clarification required

## Related Downstream Uses

This skill may feed:

- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`
- `generate-missing-items-summary`