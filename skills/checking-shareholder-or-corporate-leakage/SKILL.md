---
name: checking-shareholder-or-corporate-leakage
description: Review shareholder loan and corporate expense leakage facts for a Canadian IT contractor who operates through a corporation. Use when personal expenses may have been paid by the corporation, or corporate funds may have been used for non-business purposes, creating shareholder benefit or loan account issues. Accepts prior skill output and expense or payment descriptions. Produces a provisional leakage fact summary with flags and downstream routing.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Checking Shareholder or Corporate Leakage

Review shareholder loan and corporate expense leakage facts for a Canadian IT contractor who operates through a corporation.

## Core Rules

- Organize and flag leakage facts, do not advise on corporate tax treatment.
- Do not determine the shareholder benefit amount.
- Do not determine the shareholder loan balance.
- Do not advise on how to correct leakage.
- Preserve uncertainty where the nature of payments is unclear.
- Do not state that any arrangement is compliant or non-compliant.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `identifying-expense-categories`
- description of corporate expense payments
- description of shareholder loan activity
- corporate bank or credit card records
- user explanation in chat

Minimum useful input:

- indication that a corporation exists
- at least one expense or payment that may involve a personal component paid by the corporation

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.corporate_structure`, `documents.expense_support`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-expense-categories`, `organizing-t2125-routine-operating-expenses`.

## Workflow

### 1. Confirm leakage review is relevant

Check whether the user operates through a corporation. If no corporation is involved, return not_applicable.

### 2. Identify potential leakage items

Look for items where personal expenses may have been paid by the corporation or where the business purpose is unclear:

- personal travel claimed as business
- personal meals or entertainment with no business purpose
- personal vehicle costs charged to the corporation
- home expenses charged to the corporation without a clear business basis
- personal purchases on corporate accounts
- transfers from the corporation to the user without clear salary or dividend treatment

### 3. Organize shareholder loan facts

Identify:

- whether the user has drawn funds from the corporation beyond salary or declared dividends
- whether amounts were recorded as shareholder loans
- whether those loans were repaid within the required period
- whether the prior-year shareholder loan balance is known

Do not calculate the shareholder loan balance. Note facts and flag for CPA review.

### 4. Assess support strength

For each potential leakage item, mark support as `sufficient`, `partial`, `weak`, or `none`.

### 5. Build the provisional leakage summary

Group items into:

- likely legitimate business expenses with adequate support
- items that may have a personal component
- items that may have been misrouted through the corporation
- shareholder loan activity requiring CPA review
- unclear items

### 6. Flag issues that affect readiness

Flag issues such as:

- expense appears personal but was paid by the corporation
- business purpose not documented for a corporate expense
- shareholder loan balance unknown
- loan repayment within required period not confirmed
- salary vs dividend treatment not clear

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Indicate likely downstream uses:

- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

Do not run those workflows inside this skill.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable leakage-related facts the skill relied on
- `mappings_proposed`: use entries such as likely legitimate business expense, possible personal component, possible misrouted expense, shareholder loan item, needs_manual_review, not_applicable
- `flags`: use `missing_support`, `possible_personal_component`, `mapping_uncertain`, `unclear_classification` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: Were any personal expenses paid through the corporation? Do you have a shareholder loan balance from this year or prior years? Were corporate distributions treated as salary or dividends?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a leakage summary grouped into:

- likely legitimate corporate expenses
- items with possible personal component (show description, amount if known, flag)
- shareholder loan activity notes
- open issues requiring CPA review

## Status Guidance

- `ready_for_entry`: no material leakage indicators found and corporate expenses appear well-supported
- `clarification_required`: some items may have a personal component but facts are incomplete
- `cpa_review_recommended`: material personal or leakage items are present, or shareholder loan activity requires review
- `incomplete`: insufficient facts to assess leakage risk
- `not_applicable`: no corporation involved

Do not use `ready_for_entry` if any material leakage items are unresolved.

## Validation

- Corporate structure is confirmed or flagged as unresolved.
- Each potential leakage item is mapped or explicitly excluded.
- Shareholder loan status is noted or flagged as not applicable.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
