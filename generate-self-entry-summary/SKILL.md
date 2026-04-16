---
name: generate-self-entry-summary
description: generate a grouped-by-form self-entry summary for a canadian it contractor after income, expenses, and supporting facts have been organized. use when the user wants a plain-language summary for tax software entry, needs amounts grouped by t1 and t2125 areas, or wants to see which items are ready, unclear, or still require review before entering them.
---

# Generate Self-Entry Summary

## Purpose

Generate a grouped-by-form self-entry summary after the file has already been organized by earlier skills.

This skill reads prior skill outputs, combines the relevant mappings, unresolved questions, and caution flags, and produces a plain-language summary the user can use for tax software entry.

This skill organizes prior results into a user-facing output. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips, screenshots, or transaction exports, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- work only from organized prior results, not from raw guesswork
- group amounts by form and field where possible
- distinguish clearly between ready items, unresolved items, and review items
- preserve uncertainty where support is incomplete
- use plain language suitable for a non-practitioner
- organize and summarize, do not advise
- do not verify completeness or accuracy
- do not determine final filing positions
- do not state that an unresolved amount is safe to enter
- do not hide review flags or missing items

## Inputs This Skill Can Accept

Prefer any of the following:

- outputs from earlier skills in the repository
- a partially aggregated case output object
- organized income mappings
- organized expense mappings
- missing-items output
- GST/HST review output if relevant
- instalment review output if relevant

Minimum useful input:

- at least one organized form-relevant result from a prior skill
- at least one status or mapping that can be shown to the user

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
- `form_context`
- `review_state`
- `output_preferences`

Read from prior skill outputs where available, especially:

- `collecting-tax-documents`
- `identifying-income-sources`
- `identifying-expense-categories`
- `t2125-gross-business-income`
- `t2125-routine-operating-expenses`
- `t2125-8523-meals-and-entertainment`
- `t2125-business-use-of-home`
- `t2125-capital-assets-and-cca`
- `t2125-other-expenses-review`
- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`
- `references/grouped-by-form-template.md`
- `../../references/self-entry-summary-template.md`

## Workflow

### 1. Confirm self-entry mode is appropriate

Check whether the requested or implied output is a self-entry summary.

Use this skill when the user wants:

- a grouped-by-form summary
- help entering information into tax software
- a plain-language view of what appears ready and what does not
- a combined view of mapped fields and unresolved items

If the user actually needs a practitioner-facing handoff package instead, route to `generate-cpa-handoff-summary`.

### 2. Gather prior mapped results

Collect relevant prior outputs and organize them by form.

Typical forms or sections include:

- T2125
- T1
- GST/HST review status if relevant

Use prior `mappings_proposed`, `flags`, `open_questions`, and `status` values.

Do not invent field mappings that were not supported by earlier skills.

### 3. Group items by form and field

Build a grouped summary using broad field labels that a user can understand.

Examples:

- T2125 gross business income
- T2125 routine operating expenses
- T2125 meals and entertainment
- T2125 business-use-of-home expenses
- T1 T4 income
- T1 T4A income
- T1 RRSP deduction
- T1 instalment payments

For each item, show:

- label
- amount if known
- status
- short basis
- caution note if needed
- missing items if needed

### 4. Determine field readiness

For each grouped field or bucket, assign one of these readiness labels:

- ready for entry
- clarification required
- CPA review recommended
- not applicable

Use the strongest unresolved issue that still affects the field.

Examples:

- missing business purpose for a meal charge → clarification required
- likely capital item not yet reviewed → CPA review recommended
- well-supported recurring software expenses → ready for entry

Do not downgrade caution just to make the summary look cleaner.

### 5. Aggregate missing items and review warnings

Create a short section for:

- missing items
- review warnings
- unresolved questions that still matter for entry

Only include issues that materially affect the user’s next step.

Do not duplicate the same issue in multiple sections unless the duplication improves clarity.

### 6. Generate entry readiness summary

Summarize the file at a high level.

Include:

- count of fields or sections ready for entry
- count needing clarification
- count with CPA review recommended
- overall readiness

Allowed overall readiness values:

- complete
- partial
- not ready

### 7. Write a client-safe final summary

Produce a plain-language final output that:

- groups items by form
- highlights what appears ready
- highlights what still needs clarification
- reminds the user that the summary does not confirm correctness or deductibility

Keep it practical, concise, and understandable.

## Output Requirements

Return the result using the shared internal output schema where applicable.

Also generate a user-facing grouped-by-form self-entry summary.

At minimum, include:

- `mappings_proposed`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

And produce the visible final output using the grouped-by-form self-entry template.

## Status Guidance

Use:

- `ready_for_entry` when the summary can be generated and the file has at least some fields clearly ready for entry
- `clarification_required` when the summary can be generated but unresolved items materially remain
- `cpa_review_recommended` when major parts of the file are too uncertain for confident self-entry
- `incomplete` when there is too little organized information to generate a useful summary

Do not use `ready_for_entry` to imply that the whole return is ready to file.

## Important Boundaries

Do not:

- confirm that every amount is correct
- confirm that every mapped amount is deductible
- tell the user that no CPA review is needed
- hide major unresolved items in the summary
- output a false sense of certainty where support is incomplete
- generate a vague summary with no field-level structure

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

Use the grouped-by-form self-entry template.

The visible output should include, where relevant:

### Completion Status

- overall result
- short explanation of file readiness

### T2125

Group organized T2125 items by major section, such as:

- business income
- business expenses
- business-use-of-home
- capital and asset-related items

For each field or bucket, show:

- field label
- amount if known
- status
- short basis
- caution note if needed
- missing items if needed

### T1

Group organized T1 items by major section, such as:

- slips and income
- deductions
- tax-related items

For each field or bucket, show:

- field label
- amount if known
- status
- short basis
- caution note if needed
- missing items if needed

### Missing Items

List only the missing items that materially affect confident entry.

### Review Warnings

List the most important caution notes that still affect entry.

### Entry Readiness

Summarize:

- ready fields
- clarification-required fields
- CPA-review-recommended fields
- overall readiness

### Next Steps

State practical next steps in plain language.

## Output Pattern

Use this structure by default.

### mappings_proposed

Use aggregated prior mappings only where earlier skills already produced them.

### flags

Carry forward only the flags that still matter at summary level.

### open_questions

Carry forward only the unresolved questions that still block or affect entry.

### status

End with one of the repository standard result values.

### client_safe_summary

Use this as the visible summary basis. It should be plain-language and grouped by form.

## Example

### Example Input

- T2125 gross business income already organized
- routine operating expenses already grouped
- meals and entertainment partially organized
- one laptop purchase flagged for capital review
- one home office claim missing support
- RRSP deduction organized from slip
- instalment payment records partly organized

### Example Output Shape

- T2125 gross business income shown as ready for entry
- routine operating expenses shown as ready for entry
- meals and entertainment shown as clarification required
- business-use-of-home shown as clarification required
- capital item shown as CPA review recommended
- T1 RRSP deduction shown as ready for entry
- instalment payments shown as ready or clarification required depending on support
- missing items and review warnings listed at the end
- overall readiness shown as partial

## Related Downstream Uses

This skill may feed:

- user-facing self-entry workflow completion
- final readiness communication
- later CPA handoff decision if self-entry is not appropriate