# CLAUDE.md — it-contractors-skills

Client-facing AI workflow skills for Canadian IT contractors.

This repository contains structured preparation workflows for users who want to:

- organize their tax information
- prepare for CPA review
- or enter their return into tax software themselves

These workflows organize, map, and flag information. They do not:

- provide tax advice
- verify completeness or accuracy
- determine final filing positions
- replace CPA judgment

Built by Alex Teplov, CPA.

---

## Repository Purpose

This repository helps a Canadian IT contractor move from messy inputs to a structured result.

End outputs may include:

- grouped-by-form self-entry summary
- CPA handoff summary
- missing items and open questions summary

This is a client-facing system, even if the internal design is modular and form-aware.

---

## Repository Scope

Use this repository for:

- collecting and organizing tax documents
- identifying income sources
- identifying expense categories
- mapping likely amounts to T1 and T2125 fields
- gathering GST/HST facts
- organizing instalments and tax payments
- organizing foreign and platform income
- preparing summaries for self-entry or CPA handoff

Do not use this repository for:

- generic self-employed workflows
- e-commerce workflows
- accountant internal review workflows
- bookkeeping sign-off workflows
- legal or technical tax analysis
- final filing decisions

---

## Core Strategy

This repository uses a layered skill design.

### Broad intake skills

Organize the overall file.

Examples:

- collecting-tax-documents
- identifying-income-sources
- identifying-expense-categories

### Narrow field skills

Map specific fields or expense buckets.

Examples:

- t2125-gross-business-income
- t2125-8523-meals-and-entertainment
- t2125-business-use-of-home
- t2125-capital-assets-and-cca

### Cross-cutting risk skills

Handle issues affecting multiple areas.

Examples:

- checking-gst-hst
- reviewing-foreign-platform-and-us-income
- reviewing-instalments-and-tax-payments
- reviewing-psb-risk-facts

### Final output skills

Assemble user-facing outputs.

Examples:

- generate-self-entry-summary
- generate-cpa-handoff-summary
- generate-missing-items-summary

---

## Output Modes

### Self-entry mode

User receives grouped-by-form summary for tax software.

Must:

- organize by form and field
- show ready vs unresolved
- highlight missing items

### CPA handoff mode

User receives structured summary for CPA.

Must:

- organize facts and documents
- highlight gaps
- preserve uncertainty

### Missing-items mode

User receives:

- missing documents
- unanswered questions
- blocking issues

---

## Repository Structure

```text
skills/
  collecting-tax-documents/
    SKILL.md
    references/
      checklist-t1.md
      checklist-t2125.md

  identifying-income-sources/
    SKILL.md

  identifying-expense-categories/
    SKILL.md
    references/
      vendor-categories.md

  t2125-gross-business-income/
    SKILL.md

  t2125-routine-operating-expenses/
    SKILL.md

  t2125-8523-meals-and-entertainment/
    SKILL.md

  t2125-business-use-of-home/
    SKILL.md

  t2125-capital-assets-and-cca/
    SKILL.md

  t2125-other-expenses-review/
    SKILL.md

  checking-gst-hst/
    SKILL.md

  reviewing-foreign-platform-and-us-income/
    SKILL.md

  reviewing-instalments-and-tax-payments/
    SKILL.md

  reviewing-psb-risk-facts/
    SKILL.md

  checking-shareholder-or-corporate-leakage/
    SKILL.md

  reviewing-reasonableness-of-net-income/
    SKILL.md

  generate-self-entry-summary/
    SKILL.md
    references/
      grouped-by-form-template.md

  generate-cpa-handoff-summary/
    SKILL.md
    references/
      cpa-handoff-template.md

  generate-missing-items-summary/
    SKILL.md
    references/
      missing-items-template.md

references/
  shared-input-schema.md
  shared-output-schema.md
  self-entry-summary-template.md
  cpa-handoff-template.md

docs/
  repo-scope.md
  writing-rules.md

examples/
  income-summary.csv
  expense-log.csv
  gst-hst-records.csv
```

---

## Platform-Specific Files

Files like `agents/openai.yaml` are optional. Add them only when packaging for a specific platform. They are not part of the default repository structure.

---

## Skill Naming Rules

Use:

- kebab-case
- lowercase only
- clear functional naming

Examples:

- collecting-tax-documents
- identifying-income-sources
- t2125-gross-business-income
- t2125-8523-meals-and-entertainment
- checking-gst-hst
- generate-self-entry-summary

Avoid:

- underscores
- camelCase
- vendor-specific names
- audience suffixes

---

## Frontmatter Rules

Each `SKILL.md` must include:

```yaml
---
name: identifying-income-sources
description: organize income sources for a canadian it contractor and prepare them for tax entry or cpa review.
---
```

Description must:

- explain what the skill does
- explain when to use it
- be specific and practical
- stay under 1024 characters

---

## Skill Structure

Keep `SKILL.md` concise. Recommended structure:

```markdown
# Skill Name

## Purpose

## Core Rules

## Inputs

## Workflow

## Output Requirements

## Status Guidance

## Boundaries

## Related Uses
```

---

## Shared Schema

Use shared schemas across all skills.

### Input schema

Defines:

- user profile
- income
- expenses
- documents
- flags

Stored in: `references/shared-input-schema.md`

### Output schema

Defines:

- mappings
- flags
- questions
- status
- summary

Stored in: `references/shared-output-schema.md`

This is what makes skills interoperate.

---

## Required Rules

### Data handling

Include when needed:

> Do not type your SIN, business number, account numbers, or client names. Redact sensitive data before uploading.

### Accuracy boundary

State clearly:

- information is organized, not verified

### No tax advice

Always:

- organize
- flag
- question

Never:

- conclude filing positions

### Stop condition

Use:

> That is outside what this workflow covers. It is a question for a CPA before you file.

---

## Writing Rules

Use:

- short sections
- direct instructions
- consistent wording
- american spelling
- no em dashes

Prefer:

- organize
- map
- flag
- review
- collect

Avoid:

- long explanations
- legal language
- marketing tone

---

## Progressive Disclosure

Keep `SKILL.md` small. Move large content to `references/`.

Do not:

- duplicate schemas
- create deep folder nesting

---

## Build Priority

Start with this chain:

1. collecting-tax-documents
2. identifying-income-sources
3. identifying-expense-categories
4. t2125-gross-business-income
5. t2125-routine-operating-expenses
6. t2125-8523-meals-and-entertainment
7. generate-self-entry-summary
8. generate-missing-items-summary

Only expand after this works.

---

## Quality Checklist

Before committing:

- names match folder and frontmatter
- description is clear
- no em dashes
- outputs are defined
- boundaries are clear
- schema is respected
- file is concise

---

## Git Conventions

Use clear commit messages:

- `Add identifying-income-sources skill`
- `Refine gst hst logic`
- `Add shared schema`

Avoid vague messages.

---

## Related Repositories

- `cpa-skills` — practitioner workflows
- `ecommerce-skills` — e-commerce workflows

This repository remains client-facing and IT-contractor-specific.