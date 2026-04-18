---
name: organizing-t2125-business-use-of-home
description: Organize business-use-of-home facts and amounts for form T2125 for a Canadian IT contractor. Use when the user works from a home office and needs to identify eligible home expenses, calculate a reasonable workspace allocation, and prepare a structured mapping for self-entry or CPA handoff. Accepts prior skill output, expense lists, floor plan descriptions, and lease or mortgage details. Produces a provisional business-use-of-home mapping with allocation method, support strength, flags, and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# T2125 Business Use of Home

Organize business-use-of-home facts and amounts for T2125 after the broader expense picture has already been identified.

## Core Rules

- Work from actual home expense facts, not assumptions.
- Focus on the workspace allocation and eligible home expenses that may belong in the T2125 business-use-of-home section.
- Preserve uncertainty where the allocation method or support is incomplete.
- Organize and flag, do not advise.
- Do not determine final deductibility.
- Do not determine final GST/HST treatment.
- Do not assume a percentage without facts to support it.
- Do not force home expenses into the calculation without support.
- Do not state that any allocation is definitely correct.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `identifying-expense-categories`
- description of home and workspace
- lease or mortgage details
- utility bills
- home insurance records
- property tax records
- user explanation in chat

Minimum useful input:

- description of workspace used for business
- total home area or a reasonable basis for allocation
- at least one home expense category

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.home_office`, `documents.expense_support`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-expense-categories`, `organizing-t2125-routine-operating-expenses`.

## Workflow

### 1. Confirm business-use-of-home review is relevant

Check whether available facts suggest the user has a dedicated or regular workspace at home used for earning business income.

Typical indicators: user mentions home office, describes workspace used exclusively or regularly for business, or has home expenses that appear on the expense list.

If the file does not support a business-use-of-home review, preserve that uncertainty and do not force a mapping.

### 2. Gather workspace facts

Identify:

- whether the workspace is dedicated or shared
- approximate area of workspace
- approximate total home area
- basis for any percentage the user provides

Do not accept a percentage without a stated basis.

### 3. Identify eligible home expenses

Build a list of home expenses that may be eligible:

- rent or mortgage interest
- property taxes
- home insurance
- utilities
- maintenance and repairs relating to the home
- internet where allocated to home office use

Do not include personal portions of expenses without allocation support.

### 4. Assess support strength

For each expense category, mark support as `sufficient`, `partial`, `weak`, or `none`.

If the percentage basis is not documented, mark the allocation support accordingly.

### 5. Build the provisional business-use-of-home mapping

Map home expenses into provisional allocations:

- likely include with stated allocation
- include with caution pending clarification
- exclude_or_clarify
- needs_manual_review
- not_applicable

Note the allocation method used (area-based, room count, or other).

### 6. Flag issues that affect readiness

Flag issues such as:

- allocation percentage not supported by area facts
- workspace may not qualify if shared or occasional
- expense documentation missing
- home expense may have a personal component
- mortgage principal included where only interest is eligible
- repair or renovation may be a capital item

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

- `facts_accepted`: usable home expense facts and workspace description the skill relied on
- `mappings_proposed`: use entries such as likely include with stated allocation, include with caution, exclude_or_clarify, needs_manual_review, not_applicable
- `flags`: use `missing_support`, `mapping_uncertain`, `possible_personal_component`, `possible_capital_item`, `unclear_classification` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: What is the size of your workspace? What is the total home area? Do you have a dedicated room? Do you have receipts for the home expenses?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a business-use-of-home mapping grouped into:

- likely eligible home expenses (show category, amount if known, allocation percentage if stated, support strength)
- excluded or separately reviewed items
- unclear items needing clarification

## Status Guidance

- `ready_for_entry`: workspace allocation and eligible expenses are sufficiently organized for downstream summary use
- `clarification_required`: home office facts are partly available but allocation or support is incomplete
- `cpa_review_recommended`: file includes material allocation uncertainty, mixed-use workspace, or missing documentation
- `incomplete`: major home expense or workspace facts are still missing
- `not_applicable`: business-use-of-home review does not appear relevant from the facts provided

Do not use `ready_for_entry` if the allocation percentage lacks a stated basis.

## Validation

- Workspace description is recorded or flagged as missing.
- Allocation method is stated or flagged as unresolved.
- Every candidate home expense is mapped or explicitly excluded.
- Each included item has a support strength.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
