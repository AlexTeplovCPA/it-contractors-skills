# Repo Scope — it-contractors-skills

## Purpose

This repository contains client-facing AI workflow skills for Canadian IT contractors.

Its purpose is to help users move from messy tax inputs to structured preparation outputs. These outputs may support:

- self-entry into tax software
- CPA handoff
- document and readiness review before either path

The repository is designed around preparation, organization, mapping, and gap detection. It is not designed to replace CPA judgment.

---

## What Belongs in This Repository

Include workflows that help a Canadian IT contractor:

- collect and organize tax documents
- identify income sources
- identify expense categories
- organize GST/HST facts
- organize instalments and tax payment records
- organize foreign and platform income records
- gather support for home office, vehicle, and other common contractor issues
- map likely amounts to T1 and T2125 fields
- generate grouped-by-form self-entry summaries
- generate CPA handoff summaries
- generate missing-items and open-questions summaries

This repository may include:

- broad intake skills
- narrow field skills
- cross-cutting risk skills
- final output skills
- shared schemas
- shared templates
- reference files used by multiple skills
- examples used for testing or illustration

---

## Target User

The primary user is a Canadian IT contractor who wants help preparing their tax information.

This may include:

- sole proprietors with T1 and T2125 reporting
- incorporated or mixed-structure contractors gathering records before CPA review
- users preparing their own software entry
- users cleaning up records before handing the file to a CPA

A secondary user may be a practitioner who wants a structured client-facing intake system for IT contractor files.

---

## Output Modes in Scope

This repository supports three output modes.

### 1. Self-entry summary
A grouped-by-form summary to support user entry into tax software.

### 2. CPA handoff summary
A structured summary of facts, records, gaps, and unresolved items for a CPA.

### 3. Missing-items summary
A focused list of missing records, unanswered questions, and blocking issues.

---

## Internal Skill Strategy

The repository uses a layered design.

### Broad intake skills
These organize the overall file and normalize what the user has.

Examples:
- collecting-tax-documents
- identifying-income-sources
- identifying-expense-categories

### Narrow field skills
These review one field or one tightly related bucket at a time.

Examples:
- t2125-gross-business-income
- t2125-8523-meals-and-entertainment
- t2125-business-use-of-home
- t2125-capital-assets-and-cca

### Cross-cutting risk skills
These handle issues that affect more than one field or form.

Examples:
- checking-gst-hst
- reviewing-foreign-platform-and-us-income
- reviewing-instalments-and-tax-payments
- reviewing-psb-risk-facts

### Final output skills
These assemble prior results into a user-facing deliverable.

Examples:
- generate-self-entry-summary
- generate-cpa-handoff-summary
- generate-missing-items-summary

---

## What Does Not Belong in This Repository

Do not include:

- generic self-employed workflows not specific to IT contractors
- e-commerce seller workflows
- accountant-only internal review workflows
- bookkeeping sign-off workflows
- generic tax education content
- legal analysis
- technical tax memoranda
- definitive filing-position logic
- accountant-facing firm management workflows
- workflows that depend on private connectors or MCP tools unless the repo direction explicitly changes

Do not build skills whose main purpose is to:

- give tax advice
- determine final deductibility
- determine final compliance positions
- conclude PSB status
- conclude employment vs contractor status
- replace professional review

---

## Scope Boundary on Advice and Judgment

This repository is for organization and preparation.

Skills in this repository may:

- organize facts
- group records
- map likely fields
- flag issues
- ask useful follow-up questions
- indicate when CPA review is recommended

Skills in this repository may not:

- give legal or tax advice
- confirm filing positions
- guarantee correctness
- tell the user they are ready to file unless the wording is clearly limited to workflow readiness
- imply that CPA review is unnecessary where judgment is still required

---

## Scope Boundary on Complexity

This repository should prefer:

- modular skills
- clear outputs
- shared schemas
- reusable references
- workflows grounded in realistic contractor files

This repository should avoid:

- very large all-in-one skills
- deep theoretical guidance with no workflow value
- duplicate standards across many files
- placeholder skill folders with no content
- form-line fragmentation where there is no distinct review logic

---

## Shared Standards in Scope

The repository should maintain shared internal standards for:

- input schema
- output schema
- final output templates
- naming
- writing rules
- data-handling boundaries
- stop-and-refer wording

These standards belong at the repo level, not duplicated across every skill.

---

## Examples in Scope

Examples may be included when they materially help with:

- testing
- illustrating input shape
- illustrating output shape
- showing realistic starting points for users

Examples should not be added as filler.

Where useful, examples may include:

- input CSVs
- sample logs
- example grouped-by-form summaries
- example missing-items outputs

---

## Development Policy

A skill folder should exist only when it contains real content.

Show in the repository:

- completed skills
- real in-progress skills
- shared references
- examples used for testing or illustration
- roadmap information in the README

Do not show in the repository:

- empty placeholder folders
- fake finished skills
- speculative structures with no actual implementation value

---

## Related Repositories

This repository is distinct from:

- `cpa-skills` — practitioner-facing workflows for CPAs and bookkeepers
- `ecommerce-skills` — client-facing workflows for Canadian e-commerce sellers

This repository remains:

- client-facing
- IT-contractor-specific
- preparation-oriented
- suitable for self-entry support or CPA handoff support

It does not replace professional review.