---
name: generating-cpa-handoff-summary
description: Generate a structured CPA handoff summary for a Canadian IT contractor after income, expenses, and supporting facts have been organized by earlier skills. Use when the user wants to hand their file to a CPA for review and filing, needs a practitioner-facing summary of organized facts and open issues, or wants a clear list of what is ready, what is uncertain, and what requires professional judgment. Reads prior skill outputs and produces a fact-organized handoff package with flags, questions, and reviewer guidance.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Generate CPA Handoff Summary

Generate a structured CPA handoff summary after the file has been organized by earlier skills.

## Core Rules

- Work only from organized prior results, not from raw guesswork.
- Organize facts, documents, and open issues for a practitioner audience.
- Preserve all uncertainty, flags, and unresolved questions from prior skills.
- Do not resolve open questions on behalf of the CPA.
- Do not determine final filing positions.
- Do not verify completeness or accuracy.
- Do not hide flags, missing items, or review concerns.
- Do not produce a document that implies the return is ready to file.
- Do not tell the user what the CPA will or should conclude.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- outputs from earlier skills in the repository
- a partially aggregated case output object
- organized income mappings
- organized expense mappings
- GST/HST review output if relevant
- foreign income review output if relevant
- instalment review output if relevant
- PSB risk review output if relevant
- reasonableness review output if relevant

Minimum useful input:

- at least one organized result from a prior skill
- at least one status or mapping that can be structured for CPA review

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `form_context`, `review_state`, `output_preferences`.

Read from prior skill outputs where available, especially: `collecting-tax-documents`, `identifying-income-sources`, `identifying-expense-categories`, `organizing-t2125-gross-business-income`, `organizing-t2125-routine-operating-expenses`, `organizing-t2125-8523-meals-and-entertainment`, `organizing-t2125-business-use-of-home`, `organizing-t2125-capital-assets-and-cca`, `organizing-t2125-other-expenses`, `checking-gst-hst`, `reviewing-foreign-platform-and-us-income`, `reviewing-instalments-and-tax-payments`, `reviewing-psb-risk-facts`, `checking-shareholder-or-corporate-leakage`, `reviewing-reasonableness-of-net-income`.

## Workflow

### 1. Confirm CPA handoff mode is appropriate

Use this skill when the user is preparing to hand their file to a CPA. If the user wants a self-entry summary for tax software instead, route to `generating-self-entry-summary`.

### 2. Gather prior organized results

Collect relevant prior outputs and organize them for a practitioner audience.

Typical areas: income, expenses by category, GST/HST, foreign income, instalments, PSB risk, corporate leakage, reasonableness review.

Use prior `facts_accepted`, `mappings_proposed`, `flags`, `open_questions`, `decisions_deferred`, and `status` values.

Do not invent facts or mappings not supported by earlier skills.

### 3. Organize by review area

Build the handoff package organized by review area:

- Income: gross business income, T4 and T4A income, other income sources, foreign income
- Expenses: routine operating expenses, meals and entertainment, business-use-of-home, capital assets and CCA, other expenses
- GST/HST: registration status, collection summary, ITC candidates
- Tax payments: instalments, prior-year balance
- Risk areas: PSB risk facts, corporate leakage if applicable
- Reasonableness: overall income and expense picture
- Documents: what has been provided, what is missing

For each area, note: facts organized, amounts if known, open questions, flags, and CPA judgment required.

### 4. Aggregate flags and open questions

Compile all unresolved flags and open questions from prior skills.

Separate into:

- questions for the client to answer before CPA review
- questions for the CPA to resolve during review
- decisions deferred to the CPA

Do not attempt to answer CPA-level questions.

### 5. Organize missing documents

List all document gaps identified by prior skills.

Group by: missing income documents, missing expense support, missing GST/HST records, missing payment records, other missing items.

### 6. Assess handoff readiness

Determine:

- whether the file is sufficiently organized to hand off
- whether material client questions remain that should be answered first
- whether any area is too incomplete to include meaningfully

Do not assess filing readiness. This skill only assesses handoff readiness.

### 7. Write the handoff package

Produce a practitioner-facing summary that:

- organizes facts by review area
- highlights gaps and unresolved items
- preserves uncertainty without resolving it
- gives the CPA a clear picture of what has been organized and what remains open

## Resource Map

- `references/cpa-handoff-template.md`: use for the visible output structure
- `../../references/cpa-handoff-template.md`: use as the master template
- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: organized facts from all prior skills that were usable
- `mappings_proposed`: aggregated prior mappings, preserved at the level of confidence produced by each skill
- `flags`: all flags from prior skills that remain unresolved at handoff time
- `open_questions`: all questions still open, separated by audience (client vs CPA)
- `decisions_deferred`: all decisions intentionally left for the CPA
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`
- `client_safe_summary`: plain language, short and practical, confirming what has been organized and what still needs attention

Also produce a visible CPA handoff package using the template, including:

- File Overview (client profile, tax year, engagement mode, overall handoff status)
- Income Summary (organized by source, with amounts, documents, flags)
- Expense Summary (organized by T2125 category, with amounts, support strength, flags)
- GST/HST Summary (registration, collection, ITC candidates, open issues)
- Tax Payments (instalment facts, prior-year balance, open issues)
- Risk Areas (PSB risk, corporate leakage, open issues)
- Reasonableness Notes
- Missing Documents
- Open Questions for Client
- Open Questions for CPA
- Decisions Deferred to CPA
- Next Steps

## Status Guidance

- `ready_for_entry`: handoff package can be generated and the file is sufficiently organized for CPA intake
- `clarification_required`: handoff package can be generated but material client questions remain open
- `cpa_review_recommended`: file contains significant complexity or risk areas warranting thorough CPA review
- `incomplete`: too little organized information to generate a useful handoff package

Do not use `ready_for_entry` to imply that the return is ready to file or that no CPA judgment is needed.

## Validation

- All prior skill outputs are represented or explicitly noted as not available.
- Every open flag from a prior skill is preserved in the handoff package.
- Missing documents section is present even if empty.
- Open questions are separated by audience.
- Decisions deferred to CPA section is present and non-empty.
- Overall handoff status is one of the four standard values.
- `client_safe_summary` is present and contains no tax advice.
- No CPA-level judgment is made or implied in the summary.
