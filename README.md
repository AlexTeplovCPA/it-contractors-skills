# it-contractors-skills

Client-facing AI workflow skills for Canadian IT contractors.

This repository contains structured preparation workflows for Canadian IT contractors who want to:

- organize their tax information
- prepare for CPA review
- or enter their return into tax software themselves

These workflows are built from real accounting practice. They are designed to help users move from messy inputs to structured outputs through repeatable, profession-grounded workflows.

The internal design is modular and form-aware. The user experience should still feel simple.

---

## Repository Purpose

This repository helps a Canadian IT contractor organize tax information into one of three main outcomes:

- a grouped-by-form self-entry summary
- a CPA handoff summary
- a missing-items and open-questions summary

These workflows are for preparation and organization. They are not a substitute for CPA judgment.

---

## Who This Is For

This repository is for:

- Canadian IT contractors preparing their own tax information
- sole proprietors with T1 and T2125 reporting needs
- incorporated or mixed-structure contractors who need cleaner records before CPA review
- users who want a more structured path before entering amounts into tax software
- practitioners who want a client-facing intake structure for IT contractor files

This repository is not for:

- general self-employed workflows outside the IT contractor niche
- e-commerce seller workflows
- accountant-facing internal review workflows
- bookkeeping sign-off workflows
- deep technical tax analysis for practitioner use only

---

## What These Skills Do

These workflows can help users:

- collect and organize tax documents
- identify income sources
- identify expense categories
- map likely amounts to T1 and T2125 areas
- organize GST/HST facts
- organize foreign and platform income support
- organize instalments and tax payment information
- generate a self-entry summary
- generate a CPA handoff summary
- identify missing items before filing or handoff

They do not:

- provide tax advice
- verify completeness or accuracy
- determine final filing positions
- replace CPA review
- make legal conclusions on matters such as employment status or PSB status

---

## How the Repository Is Structured

The repository follows a layered skill strategy.

### 1. Broad intake skills

These organize the overall file and normalize what the user has.

Examples:

- `collecting-tax-documents`
- `identifying-income-sources`
- `identifying-expense-categories`

### 2. Narrow field skills

These review one field or one tightly related bucket at a time.

Examples:

- `organizing-t2125-gross-business-income`
- `organizing-t2125-8523-meals-and-entertainment`
- `organizing-t2125-business-use-of-home`
- `organizing-t2125-capital-assets-and-cca`

### 3. Cross-cutting risk skills

These handle issues that affect more than one field or form.

Examples:

- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `reviewing-psb-risk-facts`

### 4. Final output skills

These assemble prior results into a user-facing deliverable.

Examples:

- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

---

## Output Modes

### Self-entry mode

The user receives a grouped-by-form summary to help with tax software entry.

This output should:

- organize likely amounts by form and field
- distinguish ready items from unresolved items
- show missing support and caution notes
- avoid sounding like tax advice

### CPA handoff mode

The user receives a structured summary for handoff to a CPA.

This output should:

- organize documents, facts, gaps, and open questions
- highlight unresolved areas
- preserve uncertainty where support is incomplete

### Missing-items mode

The user receives a focused list of:

- missing documents
- unanswered questions
- blocking issues
- caution items preventing confident entry or handoff

---

## Current Build Priority

The first working chain is:

1. `collecting-tax-documents`
2. `identifying-income-sources`
3. `identifying-expense-categories`
4. `organizing-t2125-gross-business-income`
5. `organizing-t2125-routine-operating-expenses`
6. `organizing-t2125-8523-meals-and-entertainment`
7. `generating-self-entry-summary`
8. `generating-missing-items-summary`

This is the first end-to-end path the repository is designed to support.

After that, the next build set includes:

- `checking-gst-hst`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `organizing-t2125-business-use-of-home`
- `organizing-t2125-capital-assets-and-cca`
- `organizing-t2125-other-expenses`
- `generating-cpa-handoff-summary`

Later expansion may include:

- `t2125-travel`
- `t2125-motor-vehicle-expenses`
- `t2125-legal-accounting-and-professional-fees`
- `t2125-subcontractors-and-fees`
- `reviewing-other-income-and-reimbursements`
- `reviewing-psb-risk-facts`
- `checking-shareholder-or-corporate-leakage`
- `reviewing-reasonableness-of-net-income`

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

  organizing-t2125-gross-business-income/
    SKILL.md

  organizing-t2125-routine-operating-expenses/
    SKILL.md

  organizing-t2125-8523-meals-and-entertainment/
    SKILL.md

  organizing-t2125-business-use-of-home/
    SKILL.md

  organizing-t2125-capital-assets-and-cca/
    SKILL.md

  organizing-t2125-other-expenses/
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

  generating-self-entry-summary/
    SKILL.md
    references/
      grouped-by-form-template.md

  generating-cpa-handoff-summary/
    SKILL.md
    references/
      cpa-handoff-template.md

  generating-missing-items-summary/
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

Platform-specific files such as `agents/openai.yaml` are optional and may be added later for distribution needs. They are not part of the default repository structure.

---

## How to Use

Once installed in a compatible AI agent, the relevant workflow should load automatically when the user's request matches the skill.

Example:

```
request → "I need to organize my tax documents and figure out what I'm missing"
agent loads → collecting-tax-documents
output → document inventory, missing items, and next-step summary
```

Another example:

```
request → "I had client meals and need to know where they belong"
agent loads → organizing-t2125-8523-meals-and-entertainment
output → field mapping, open questions, and caution notes
```

The user should not need to manually orchestrate the internal skill structure.

---

## Design Principles

These workflows are built around a few practical principles.

**Organize before deciding.** The system should collect and normalize facts before trying to map them to form fields.

**Narrow where it helps.** Line-specific or bucket-specific skills should be used where they improve clarity, testing, and maintenance.

**Keep cross-cutting risks separate.** GST/HST, foreign and platform income, instalments, PSB-related facts, and corporate overlap should not be hidden inside one field skill.

**Final outputs must be understandable.** Even if the internal logic is modular, the visible result should be clear to a non-practitioner.

**Preparation, not professional sign-off.** The point is to reduce friction and improve organization before filing or handoff, not to remove the need for judgment.

---

## Disclosure

These workflows organize information provided by the user. They do not verify completeness or accuracy, provide tax advice, or create a professional relationship of any kind.

Use of these workflows does not replace review by a qualified CPA before filing.

---

## Related Repositories

- [cpa-skills](https://github.com/AlexTeplovCPA/it-contractors-skills) — practitioner-facing workflows for CPAs and bookkeepers
- [ecommerce-skills](https://github.com/AlexTeplovCPA/ecommerce-skills) — client-facing workflows for Canadian e-commerce sellers

---

## License

This repository is licensed under the MIT License.

These workflows are built from real accounting practice. If you adapt or use them, attribution is appreciated. See the `LICENSE` file for details.

---

## About

Built by [Alex Teplov, CPA](https://teplov.ca).

Specialized accounting practices in Canada focused on IT contractors and e-commerce sellers. These workflows are built from real operational bottlenecks encountered in practice.
