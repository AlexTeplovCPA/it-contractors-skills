---
name: generating-missing-items-summary
description: Generate a focused missing-items and open-questions summary for a Canadian IT contractor after income, expenses, documents, and review issues have been organized by earlier skills. Use when the user needs a short list of missing records, unanswered questions, and blocking issues before self-entry or CPA handoff. Reads prior skill outputs, removes duplicate and low-value noise, and produces a grouped plain-language summary the user can act on immediately.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-17
---

# Generate Missing Items Summary

Generate a focused missing-items and open-questions summary after the file has been organized by earlier skills.

## Core Rules

- Work only from organized prior results, not from raw guesswork.
- Include only missing items and unresolved questions that materially affect the next step.
- Remove duplicate or low-value issues.
- Group missing items by practical category.
- Preserve uncertainty where support is incomplete.
- Use plain language suitable for a non-practitioner.
- Organize and summarize, do not advise.
- Do not verify completeness or accuracy.
- Do not determine final filing positions.
- Do not hide major blocking issues.
- Do not treat the missing-items list as a filing decision.
- Do not confirm that unresolved items are unimportant.
- Do not generate vague follow-up items the user cannot act on.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- outputs from earlier skills in the repository
- a partially aggregated case output object
- organized document inventory
- organized income mappings
- organized expense mappings
- GST/HST review output if relevant
- instalment review output if relevant

Minimum useful input:

- at least one prior skill output containing missing support, open questions, or flags

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `review_state`, `output_preferences`.

Read from prior skill outputs where available, especially: `collecting-tax-documents`, `identifying-income-sources`, `identifying-expense-categories`, `organizing-t2125-gross-business-income`, `organizing-t2125-routine-operating-expenses`, `organizing-t2125-8523-meals-and-entertainment`, `organizing-t2125-business-use-of-home`, `organizing-t2125-capital-assets-and-cca`, `organizing-t2125-other-expenses`, `checking-gst-hst`, `reviewing-foreign-platform-and-us-income`, `reviewing-instalments-and-tax-payments`, `generating-self-entry-summary`, `generating-cpa-handoff-summary`.

## Workflow

### 1. Confirm missing-items mode is appropriate

Use this skill when the user needs a list of missing documents or unresolved questions, a practical checklist before self-entry or CPA handoff, or a short explanation of what still blocks progress.

If the user needs a grouped-by-form entry summary, route to `generating-self-entry-summary`.

### 2. Gather unresolved items from prior results

Collect missing or unresolved items from prior skill outputs, especially `open_questions`, `flags`, support gaps, mentioned-but-not-provided documents, and blocking issues affecting readiness.

Do not pull in resolved items.

### 3. Remove duplicates and low-value noise

Merge overlapping issues. If three prior skills all flag missing GST/HST records, show one grouped item. Exclude issues that do not materially affect the next step.

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

Keep distinct:

- missing documents or records
- unanswered factual questions
- blocking issues that prevent confident entry or handoff

### 6. Identify the true blockers

Mark issues that still prevent useful next steps.

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

Produce a plain-language summary that tells the user what is still missing, what questions still need answers, whether the file is close to usable or still materially incomplete, and what to do next.

## Resource Map

- `references/missing-items-template.md`: use for the visible output structure
- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `flags`: carry forward only flags that still matter at summary level
- `open_questions`: carry forward only unresolved questions that still need answers
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`
- `client_safe_summary`: plain language, short and practical

Also produce a visible missing-items summary using the template, including:

- Overall Status (result and short explanation of what still blocks progress)
- Missing Documents grouped by: income support, expense support, GST/HST records, home office support, instalment payment records
- Open Questions
- Blocking Issues
- Caution Notes
- Recommended Next Actions

## Status Guidance

- `ready_for_entry`: no material missing items remain for the intended next step
- `clarification_required`: file is mostly organized but unresolved items remain
- `cpa_review_recommended`: missing items or unresolved issues create material uncertainty
- `incomplete`: key records or facts are still missing

Do not use `ready_for_entry` if major records or clarifications are still outstanding.

## Validation

- Missing Documents section is present and grouped by practical category.
- No resolved item from a prior skill appears in the missing list.
- Blocking Issues are identified separately from general open questions.
- Recommended Next Actions are concrete and actionable.
- `status` is one of the four standard values.
- `client_safe_summary` is present and contains no tax advice.
