---
name: reviewing-reasonableness-of-net-income
description: Review the overall reasonableness of reported net business income for a Canadian IT contractor before final summary or CPA handoff. Use after income and expense skills have run to identify obvious gaps, unusual ratios, or totals that appear inconsistent with the facts provided. Accepts prior skill outputs and income or expense summaries. Produces a reasonableness assessment with flags and downstream routing. This skill flags concerns only and does not verify amounts.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Reviewing Reasonableness of Net Income

Review the overall reasonableness of reported net business income for a Canadian IT contractor after prior skills have run.

## Core Rules

- Flag concerns about overall reasonableness, do not verify amounts.
- Do not recalculate totals.
- Do not advise on what the correct net income should be.
- Do not compare the user's income to industry benchmarks with specificity.
- Preserve uncertainty where inputs are incomplete.
- Do not state that the user's income is correct or incorrect.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- output from `organizing-t2125-gross-business-income`
- output from `organizing-t2125-routine-operating-expenses`
- output from `organizing-t2125-8523-meals-and-entertainment`
- output from `organizing-t2125-business-use-of-home`
- output from `organizing-t2125-capital-assets-and-cca`
- output from `organizing-t2125-other-expenses`
- user summary of total income and expenses
- prior year return summary

Minimum useful input:

- approximate gross business income
- approximate total expenses claimed

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `form_context`, `review_state`.

Read from prior skill outputs where available: all T2125 organizing skills.

## Workflow

### 1. Confirm reasonableness review is relevant

Check whether sufficient income and expense facts are available. If income or expense totals are missing entirely, return incomplete.

### 2. Summarize income and expense totals from prior skills

Identify approximate totals for:

- gross business income
- total expenses (by category where available)
- net income before CCA
- CCA deduction if applicable
- net income after CCA

Note which totals are confirmed, provisional, or estimated.

### 3. Check for obvious gaps or inconsistencies

Review the assembled totals for:

- gross income appears very low relative to the number of clients or contract rates described
- expenses appear very high relative to the type of business activity
- a single expense category appears disproportionately large
- net income is negative and the facts do not explain a loss year
- totals do not add up from the parts provided

Do not flag minor rounding or estimation differences.

### 4. Check prior year comparison if available

If the user has provided prior year figures, note:

- significant changes in gross income without a stated explanation
- significant changes in expense ratios without a stated explanation

Do not conclude that a change is incorrect.

### 5. Assess overall reasonableness

Form a general view of whether the assembled picture appears consistent with the facts provided:

- consistent: totals appear reasonable given the described activity
- minor concerns: some items are unusual but not material
- material concerns: one or more items appear inconsistent with the facts and warrant review
- cannot assess: insufficient information

Do not use scoring or numerical benchmarks.

### 6. Flag issues that affect readiness

Flag issues such as:

- net income appears unusually low or negative without explanation
- expense ratio appears unusually high for the business type
- gross income total appears inconsistent with contracts or rates described
- significant change from prior year without explanation
- totals could not be confirmed from the available inputs

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

- `facts_accepted`: income and expense totals the skill relied on
- `mappings_proposed`: use entries such as consistent, minor_concern, material_concern, cannot_assess for each major area reviewed
- `flags`: use `reasonableness_concern`, `missing_support`, `mapping_uncertain` where applicable
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: Can you confirm your approximate total gross income for the year? Is there a reason net income is lower than last year?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a reasonableness summary grouped into:

- income totals reviewed (gross, net before CCA, net after CCA)
- expense totals reviewed (by category)
- prior year comparison if available
- reasonableness assessment (consistent, minor concerns, material concerns, cannot assess)
- flags requiring follow-up

## Status Guidance

- `ready_for_entry`: totals appear reasonably consistent with the facts provided and no material concerns are present
- `clarification_required`: totals are mostly available but some inconsistency needs explanation
- `cpa_review_recommended`: material reasonableness concerns are present that warrant CPA review before filing
- `incomplete`: insufficient income or expense totals to assess reasonableness
- `not_applicable`: not applicable

Do not use `ready_for_entry` if material reasonableness concerns are present.

## Validation

- Gross income total is noted or flagged as unavailable.
- Total expenses are noted or flagged as unavailable.
- Net income is noted or flagged as unavailable.
- A reasonableness assessment is stated.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
