# T1 Document Checklist

Use this checklist with `collecting-tax-documents`.

The purpose of this file is to help organize common T1-related records for a Canadian IT contractor.

This checklist is for document collection only. It does not determine whether a slip amount is taxable, deductible, business-related, or ready for filing.

---

## How to Use This Checklist

For each item below, mark one of:

- `received`
- `mentioned_not_provided`
- `missing`
- `not_applicable`
- `unclear`

Do not guess.

If the user is unsure whether a document exists, mark it as `unclear`.

---

## Core T1 Items

### Employment and contract slips

- T4 slips
- T4A slips
- T5 slips if relevant
- other tax slips if mentioned

### Personal deduction and contribution records

- RRSP contribution slips
- FHSA contribution slips if relevant
- union or professional dues slips if relevant
- tuition slips if relevant

### Tax payment records

- instalment reminder or instalment notice from CRA
- proof of instalment payments made during the year
- notice of assessment from the prior year if available

### Other personal return support

- prior-year return summary if available
- prior-year notice of assessment if available
- summary of any carryforward items if the user mentions them

---

## Relevance Notes for This Repository

This repository is focused on Canadian IT contractors.

For most users in this repository, the highest-priority T1 records are:

- T4 slips
- T4A slips
- RRSP slips
- instalment payment records
- prior-year notice of assessment if available

Do not ask for low-relevance T1 documents unless the user’s facts suggest they matter.

---

## Output Guidance

When using this checklist inside a skill, group the result into:

### Confirmed T1 documents
List all items marked `received`.

### Mentioned but not provided
List all items marked `mentioned_not_provided`.

### Missing T1 documents
List only the missing items that matter for the next workflow step.

### Not applicable
List items clearly outside the user’s situation only if doing so improves clarity.

---

## Important Boundary

This checklist helps collect T1-related documents.

It does not:
- verify completeness
- interpret slip treatment
- determine filing positions
- replace CPA review