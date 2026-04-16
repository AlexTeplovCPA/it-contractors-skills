---
name: generate-missing-items-summary
description: generate a focused missing-items and open-questions summary for a canadian it contractor after income, expenses, documents, and review issues have been organized. use when the user needs a short list of missing records, unanswered questions, and blocking issues before self-entry or cpa handoff.
---

# Generate Missing Items Summary

## Purpose

Generate a focused missing-items and open-questions summary after the file has already been organized by earlier skills.

This skill reads prior skill outputs, identifies the documents, facts, and unresolved issues that still matter, removes low-value noise, and produces a short plain-language summary the user can act on.

This skill organizes prior results into a user-facing output. It does not verify completeness or accuracy.

> Do not type your SIN, business number, account numbers, or client names into this conversation. Use general descriptions and rounded amounts where possible. If uploading tax slips, screenshots, or transaction exports, redact sensitive identifiers first. Avoid sharing sensitive information you would not be comfortable storing in a third-party system.

## Core Rules

- work only from organized prior results, not from raw guesswork
- include only missing items and unresolved questions that materially affect the next step
- remove duplicate or low-value issues
- group missing items by practical category
- preserve uncertainty where support is incomplete
- use plain language suitable for a non-practitioner
- organize and summarize, do not advise
- do not verify completeness or accuracy
- do not determine final filing positions
- do not hide major blocking issues

## Inputs This Skill Can Accept

Prefer any of the following:

- outputs from earlier skills in the repository
- a partially aggregated case output object
- organized document inventory
- organized income mappings
- organized expense mappings
- GST/HST review output if relevant
- instalment review output if relevant

Minimum useful input:

- at least one prior skill output containing missing support, open questions, or flags

## Internal Input Fields to Read

Read from the shared input schema where available:

- `case_id`
- `tax_year`
- `engagement_mode`
- `user_profile`
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
- `generate-self-entry-summary`
- `generate-cpa-handoff-summary`

See:
- `../../references/shared-input-schema.md`
- `../../references/shared-output-schema.md`
- `references/missing-items-template.md`

## Workflow

### 1. Confirm missing-items mode is appropriate

Use this skill when the user needs:

- a list of missing documents
- a list of unresolved questions
- a short explanation of what still blocks progress
- a practical checklist before self-entry or CPA handoff

If the user actually needs a grouped-by-form entry summary, route to `generate-self-entry-summary`.

### 2. Gather unresolved items from prior results

Collect missing or unresolved items from prior skill outputs, especially:

- `open_questions`
- `flags`
- support gaps
- mentioned-but-not-provided documents
- blocking issues affecting readiness

Do not pull in resolved items.

### 3. Remove duplicates and low-value noise

Merge overlapping issues.

Examples:

- if three prior skills all indicate missing GST/HST records, show one grouped GST/HST item
- if both a field skill and a broad skill ask the same business-purpose question, show it once

Exclude issues that do not materially affect the next step.

### 4. Group missing items into practical sections

Use sections such as:

- income support
- expense support
- home office support
- GST/HST records
- instalment and tax payment records
- open questions
- blocking issues

Do not force every issue into a form-based structure.

### 5. Separate missing documents from unanswered questions

Keep these distinct:

- missing documents or records
- unanswered factual questions
- blocking issues that prevent confident entry or handoff

This makes the output easier for the user to act on.

### 6. Identify the true blockers

Mark the issues that still prevent useful next steps.

Common blockers:

- no income support for a material source
- no expense log or transaction support
- home office claim with no supporting details
- GST/HST status mentioned but unsupported
- instalments mentioned but no payment support
- possible capital item with no documentation
- unclear business purpose for a material expense

Do not overstate blockers where the file is still usable for a later step.

### 7. Write a short practical summary

Produce a plain-language summary that tells the user:

- what is still missing
- what questions still need answers
- whether the file is close to usable or still materially incomplete
- what to do next

## Output Requirements

Return the result using the shared internal output schema where applicable.

Also generate a user-facing missing-items and open-questions summary.

At minimum, include:

- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

And produce the visible final output using the missing-items template.

## Status Guidance

Use:

- `ready_for_entry` only when there are no material missing items left for the intended next step
- `clarification_required` when the file is mostly organized but still has unresolved items
- `cpa_review_recommended` when missing items or unresolved issues create material uncertainty
- `incomplete` when key records or facts are still missing

Do not use `ready_for_entry` if major records or clarifications are still outstanding.

## Important Boundaries

Do not:

- treat the missing-items list as a filing decision
- confirm that unresolved items are unimportant
- hide major uncertainty
- turn this into a long general tax checklist unrelated to the actual file
- generate vague follow-up items that the user cannot act on

Use this standard phrase where relevant:

> That is outside what this workflow covers. It is a question for a CPA before you file.

## Required Final Output Shape

Use the missing-items template.

The visible output should include, where relevant:

### Overall Status

- overall result
- short explanation of what still blocks progress

### Missing Documents

Group missing records by practical category.

Examples:
- income support
- expense support
- GST/HST records
- home office support
- instalment payment records

### Open Questions

List only the factual questions that still matter.

### Blocking Issues

List the items that still prevent confident self-entry or CPA handoff.

### Caution Notes

List only the warnings that still matter for the next step.

### Recommended Next Actions

State practical next steps in plain language.

## Output Pattern

Use this structure by default.

### flags

Carry forward only the flags that still matter at summary level.

### open_questions

Carry forward only the unresolved questions that still need answers.

### status

End with one of the repository standard result values.

### client_safe_summary

Use this as the visible summary basis. It should be plain-language, short, and practical.

## Example

### Example Input

- one direct client income source still lacks invoice support
- one meal expense lacks business purpose explanation
- home office claim has no workspace details
- GST/HST registration was mentioned but filing records were not provided
- instalment payment was mentioned but no payment proof was uploaded

### Example Output Shape

- missing invoice summary listed under income support
- missing meal explanation listed under open questions
- missing workspace size and home cost details listed under home office support
- GST/HST filing records listed under GST/HST records
- missing instalment payment proof listed under instalment records
- overall status set to clarification required or incomplete depending on materiality

## Related Downstream Uses

This skill may feed:

- user-facing next-step guidance
- readiness communication before self-entry
- readiness communication before CPA handoff