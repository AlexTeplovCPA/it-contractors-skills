---
name: organizing-t2125-other-expenses
description: Organize remaining business expenses that do not fit standard T2125 expense lines for a Canadian IT contractor. Use after routine operating, meals, home office, and capital asset skills have run, to capture leftover or unusual items that may still be legitimate business expenses. Accepts prior skill output and expense lists. Produces a provisional other-expenses mapping with support strength, flags, and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# T2125 Other Expenses

Organize remaining business expenses for T2125 that do not belong in other specific expense lines, after prior field skills have run.

## Core Rules

- Work from prior skill outputs and remaining unclassified expenses.
- Focus on items not already handled by routine operating, meals, home office, or capital asset skills.
- Preserve uncertainty where classification or support is incomplete.
- Organize and flag, do not advise.
- Do not determine final deductibility.
- Do not determine final GST/HST treatment.
- Do not force items into other expenses if they clearly belong elsewhere.
- Do not state that an expense is definitely allowable.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `identifying-expense-categories`
- output from `organizing-t2125-routine-operating-expenses`
- output from `organizing-t2125-8523-meals-and-entertainment`
- output from `organizing-t2125-business-use-of-home`
- output from `organizing-t2125-capital-assets-and-cca`
- expense log or CSV with unclassified items
- user explanation in chat

Minimum useful input:

- at least one expense not already handled by a prior skill
- some explanation of what the expense was for

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `documents.expense_support`, `transactions.expense_items`, `form_context`, `review_state`.

Read from prior skill outputs where available: all preceding T2125 organizing skills.

## Workflow

### 1. Confirm other-expenses review is relevant

Check whether prior skills left any items unclassified or whether the user has described expenses with no obvious standard home.

If there are no remaining unclassified items, return not_applicable.

### 2. Build the candidate other-expenses set

Identify items not mapped by prior skills. Typical candidates:

- professional development costs
- association or membership fees
- bank fees and merchant fees
- licensing and regulatory fees
- shipping or courier costs for business
- small tools or minor equipment not reaching capital threshold
- other unusual but potentially legitimate business costs

Do not include: personal expenses with no business connection, items already mapped by another skill, items with no explanation.

### 3. Extract key facts for each candidate item

For each candidate, identify: vendor or description, date, amount, receipt status, and business purpose explanation.

Do not invent missing details.

### 4. Assess support strength

For each candidate, mark support as `sufficient`, `partial`, `weak`, or `none`.

### 5. Build the provisional other-expenses mapping

Map candidate items into one of:

- likely other business expense
- include with caution
- exclude_or_clarify
- carry_to_other_field
- needs_manual_review
- not_applicable

Note the general nature of each item rather than forcing a specific T2125 line.

### 6. Flag issues that affect readiness

Flag issues such as:

- business purpose unclear
- receipt missing
- item may belong in a more specific field
- item may be partly personal
- item description is too vague to support

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

- `facts_accepted`: usable expense facts the skill relied on
- `mappings_proposed`: use entries such as likely other business expense, include with caution, exclude_or_clarify, carry_to_other_field, needs_manual_review, not_applicable
- `flags`: use `missing_support`, `mapping_uncertain`, `possible_personal_component`, `unclear_classification` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include an other-expenses mapping grouped into:

- likely other business expenses (show description, amount if known, support strength, confidence level)
- excluded or separately reviewed items
- unclear items needing clarification

## Status Guidance

- `ready_for_entry`: remaining expenses are sufficiently organized for downstream summary use
- `clarification_required`: some items are identified but support or classification is incomplete
- `cpa_review_recommended`: file includes unusual items or material uncertainty
- `incomplete`: significant unclassified expenses remain without explanation
- `not_applicable`: no remaining unclassified expenses after prior skills ran

## Validation

- Every remaining candidate item is mapped or explicitly excluded.
- Each included item has a support strength and brief purpose note.
- Items that may belong in another field are flagged with carry_to_other_field.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
