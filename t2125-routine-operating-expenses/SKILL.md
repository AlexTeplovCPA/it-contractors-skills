---
name: t2125-routine-operating-expenses
description: organize likely routine operating expenses for form t2125 for a canadian it contractor. use when the user needs to group recurring business expenses into practical t2125 expense buckets, separate routine operating costs from meals, home office, travel, vehicle, or possible capital items, or prepare a structured summary for self-entry or cpa handoff after expense categories have already been identified.
---

# T2125 Routine Operating Expenses

## Purpose

Organize likely routine operating expenses for T2125 after the broader expense picture has already been identified.

This skill takes the organized expense categories, groups the items that appear to be recurring or ordinary business operating costs, and prepares a structured mapping for downstream summaries.

This skill organizes information provided by the user. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading receipts, screenshots, or transaction exports, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- work from identified expense categories, not from vague assumptions
- focus on likely routine operating expenses that may belong in ordinary T2125 expense areas
- separate routine operating costs from meals, travel, vehicle, home office, subcontractors, professional fees, and possible capital items where possible
- preserve uncertainty where support is incomplete or classification is mixed
- organize and flag, do not advise
- do not determine final deductibility
- do not determine final GST/HST treatment
- do not force mixed-use items into a fully business amount without support
- do not finalize capital vs current treatment where the facts remain unclear

## Inputs This Skill Can Accept

Prefer any of the following:

- output from `identifying-expense-categories`
- expense log or CSV
- bookkeeping export
- bank or card transaction summaries
- uploaded receipts
- user explanation in chat
- vendor/category spreadsheet

Minimum useful input:

- at least one identified expense item or expense category
- some indication of what the expense was for
- some support or explanation for the amount

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
- `form_context`
- `review_state`

Read from prior skill outputs where available:

- `identifying-expense-categories`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`

## Workflow

### 1. Confirm routine operating expense review is relevant

Check whether the available facts suggest ordinary business expenses that are not better handled by a separate downstream skill.

Typical indicators:

- recurring software subscriptions
- cloud hosting or infrastructure costs
- office supplies
- internet and phone costs used for business
- low-risk admin costs
- minor workspace-related costs not requiring separate home office treatment
- small recurring tools used in contractor work

If the file does not support a routine operating expense review, preserve that uncertainty and do not force a mapping.

### 2. Build the candidate routine expense set

Create a working set of expenses that may belong in routine T2125 operating expense areas.

Typical candidates:

- software and cloud tools
- office and admin costs
- internet and phone expenses
- minor workspace-related costs
- recurring developer tools or subscriptions
- low-risk supplies and small business-use purchases

Do not automatically include:

- restaurant and meal charges
- travel-related costs
- vehicle-related costs
- home office allocations
- large one-time equipment purchases
- obvious professional fees
- obvious subcontractor payments
- unclear or unsupported charges with no plausible business link

### 3. Separate routine items from other review areas

Group identified amounts into these buckets:

- likely routine operating expenses
- likely meals and entertainment
- likely home office related costs
- likely travel costs
- likely professional fees
- likely subcontractor or outside service costs
- likely possible capital items
- unclear or mixed-use amounts

Do not settle mixed classification if the facts are weak.

### 4. Assess support strength

For each candidate routine expense or grouped category, assess support such as:

- receipt
- invoice
- expense log entry
- bookkeeping record
- bank or card record
- user explanation only

Mark support strength as one of:

- sufficient
- partial
- weak
- none

If the expense appears business-related but is not well-supported, preserve it as provisional.

### 5. Build the provisional routine operating expense mapping

Map supported or plausibly supported routine expenses into broad T2125 routine operating groupings.

Acceptable broad groupings include:

- software and cloud
- office and admin
- internet and phone
- routine supplies
- minor workspace-related costs
- other routine operating items

Use practical grouping first.  
Do not overstate confidence in final line-level placement where the category could still shift.

### 6. Flag issues that affect readiness

Flag issues such as:

- support missing for recurring expenses
- internet or phone appears mixed-use
- same expense may appear duplicated
- one-time larger purchase may not be routine
- description too vague to support category
- expense may belong to a different downstream skill
- software or service may partly relate to a non-business activity

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Based on the provisional routine operating expense result, indicate likely downstream uses.

Common downstream uses:

- `t2125-8523-meals-and-entertainment`
- `t2125-business-use-of-home`
- `t2125-capital-assets-and-cca`
- `t2125-other-expenses-review`
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

Also include a clear routine operating expense mapping grouped into:

- likely included routine operating expenses
- excluded or separately reviewed amounts
- unclear or mixed-use amounts

## Status Guidance

Use:

- `ready_for_entry` when likely routine operating expenses are sufficiently organized for downstream summary use
- `clarification_required` when routine expenses are mostly identified but support or classification is incomplete
- `cpa_review_recommended` when the file includes material mixed-use, unclear categorization, or possible misgrouping
- `incomplete` when major routine expense support is still missing
- `not_applicable` when routine operating expense review does not appear relevant from the facts provided

Do not use `ready_for_entry` if routine operating expenses still depend heavily on unsupported explanations or if several items may actually belong in other categories.

## Important Boundaries

Do not:

- determine final deductibility
- state that an expense is definitely allowable
- treat mixed-use internet or phone as fully business without support
- finalize capital vs current treatment
- determine final GST/HST treatment
- state that the user is ready to file

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

### Likely Included Routine Operating Expenses

For each included or provisionally included item or group, show:

- category label
- representative vendor or item
- amount if known
- support strength
- confidence level

### Excluded or Separately Reviewed Amounts

List amounts that should not be treated as straightforward routine operating expenses at this stage.

### Open Questions

List only the questions that materially affect the routine operating expense result.

### Readiness Result

State whether the routine operating expense side is:

- ready for next step
- clarification required
- incomplete
- CPA review recommended
- not applicable

### Client-Safe Summary

Write a short plain-language summary that explains:

- what likely belongs in routine operating expenses
- what is still unclear
- what the next step should be

## Output Pattern

Use this structure by default.

### facts_accepted

Capture the usable expense facts the skill relied on.

### mappings_proposed

Use mapping entries such as:

- likely include as routine operating expense
- include with caution
- exclude_or_clarify
- carry_to_other_field
- needs_manual_review

Use broad routine operating groupings that stay consistent with repo standards.

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

- recurring AWS and GitHub charges appear in the expense log
- QuickBooks annual subscription is present
- internet bills appear in the transaction list
- one laptop purchase appears in the same file
- one restaurant charge also appears in the file
- the user has receipts for most recurring software expenses

### Example Output Shape

- AWS, GitHub, and QuickBooks grouped as likely routine operating expenses
- internet expenses included with caution because mixed-use is possible
- laptop purchase excluded for separate capital review
- restaurant charge excluded for separate meals review
- status set to clarification required if one or more routine items remain weakly supported

## Related Downstream Uses

This skill may feed:

- `t2125-8523-meals-and-entertainment`
- `t2125-business-use-of-home`
- `t2125-capital-assets-and-cca`
- `t2125-other-expenses-review`
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`