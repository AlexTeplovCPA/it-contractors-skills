# it-contractors-skills

CPA-developed, platform-neutral workflows that help Canadian IT contractors use AI more safely to organize their tax information, identify missing facts, and prepare for filing or CPA review.

This repository contains structured preparation workflows for Canadian IT contractors who want to:

- organize their tax information
- prepare for CPA review
- or enter their return into tax software themselves

These workflows are built from real accounting practice and designed for a reality that already exists: many contractors are already using AI to help with tax questions and tax preparation. The goal here is not to replace CPA judgment. It is to give users a more structured way to use AI for preparation, organization, and issue spotting before filing or handoff.

The internal design is modular and form-aware. The user experience should still feel simple.

---

## Repository Purpose

This repository helps Canadian IT contractors use AI in a more structured way when preparing tax information. Instead of relying on one-off prompts or generic tax answers, the workflows guide users toward one of three practical outcomes:

- a grouped-by-form self-entry summary
- a CPA handoff summary
- a missing-items and open-questions summary

These workflows are for preparation, organization, and issue spotting. They are not a substitute for CPA judgment, final filing positions, or legal conclusions.

## Platform Neutrality

The canonical workflows in this repository live in `skills/*/SKILL.md`. They are written for capable AI agents in general, not for one model provider.

The same skill content can be used with Codex, Claude, ChatGPT, Gemini, or another agent when that agent can read the relevant files and follow the workflow.

Platform-specific files are adapters only:

- `AGENTS.md` gives Codex repo-level guidance.
- `CLAUDE.md` gives Claude repo-level guidance.
- `GEMINI.md` gives Gemini repo-level guidance.
- `docs/platforms/codex.md` explains Codex usage.
- `docs/platforms/claude.md` explains Claude usage.
- `docs/platforms/gemini.md` explains Gemini usage.
- `docs/platforms/agent-compatibility.md` defines the agent-neutral compatibility contract.

Automatic skill discovery depends on the platform. If an agent cannot auto-load a skill, point it directly to the relevant `SKILL.md` file and ask it to follow that workflow.

## How This Repository Fits the Broader System

This repository contains CPA-designed AI workflows for one specific client niche: Canadian IT contractors. The goal is clearer boundaries, cleaner preparation, and better handoff quality.

---

## Who This Is For

This repository is for:

- Canadian IT contractors who already use AI and want a safer workflow for tax preparation
- contractors preparing their own tax information before filing or software entry
- sole proprietors with T1 and T2125 reporting needs
- incorporated or mixed-structure contractors who need cleaner records before CPA review
- users who want more structure, clearer boundaries, and fewer missing facts before handoff
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
- preserve uncertainty where facts are incomplete
- flag missing support and open questions that should be resolved before filing
- generate a self-entry summary
- generate a CPA handoff summary
- identify missing items before filing or handoff

They do not:

- provide tax advice
- verify completeness or accuracy
- determine final filing positions
- resolve ambiguous tax treatment
- replace CPA review
- make legal conclusions on matters such as employment status or PSB status

---

## Why Use These Workflows Instead of a Blank AI Prompt

Generic AI tax prompts often fail in predictable ways: they accept incomplete facts too easily, blur preparation with advice, and sound more certain than the input supports.

These workflows are designed to reduce that risk by giving the model a tighter job:

- ask for the facts that matter
- organize those facts into a structured output
- preserve uncertainty where support is incomplete
- flag issues that should be reviewed before filing
- route the result toward self-entry, CPA handoff, or missing-items follow-up

The result should feel less like asking AI for an answer and more like using a CPA-designed preparation process.

## How a Contractor Would Use This Repository

A typical user flow looks like this:

1. Start with broad intake skills to organize documents, income sources, and expense categories.
2. Run narrower skills for the areas that need detail, such as gross income, home office, meals, or capital assets.
3. Use cross-cutting review skills for issues like GST/HST, foreign income, instalments, or PSB risk facts.
4. Generate the final output that best fits the situation: self-entry summary, CPA handoff summary, or missing-items summary.

The goal is not to answer every tax question in one step. The goal is to move from messy inputs to a cleaner, better-scoped file.

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

## Current Build State

All 18 skills are built and included in the repository.

### Broad intake

- `collecting-tax-documents`
- `identifying-income-sources`
- `identifying-expense-categories`

### Narrow field skills

- `organizing-t2125-gross-business-income`
- `organizing-t2125-routine-operating-expenses`
- `organizing-t2125-8523-meals-and-entertainment`
- `organizing-t2125-business-use-of-home`
- `organizing-t2125-capital-assets-and-cca`
- `organizing-t2125-other-expenses`

### Cross-cutting risk skills

- `checking-gst-hst`
- `checking-shareholder-or-corporate-leakage`
- `reviewing-foreign-platform-and-us-income`
- `reviewing-instalments-and-tax-payments`
- `reviewing-psb-risk-facts`
- `reviewing-reasonableness-of-net-income`

### Final output skills

- `generating-self-entry-summary`
- `generating-missing-items-summary`
- `generating-cpa-handoff-summary`

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

AGENTS.md
CLAUDE.md
GEMINI.md
docs/
  repo-scope.md
  writing-rules.md
  platforms/
    agent-compatibility.md
    codex.md
    claude.md
    gemini.md

examples/
  inputs/
    income-summary.csv
    expense-log.csv
    gst-hst-records.csv
  outputs/
    self-entry-summary-example.md
    missing-items-summary-example.md
```

Platform-specific files such as `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, or `agents/openai.yaml` are adapters. They may explain how a platform should load or expose the same canonical workflows, but they should not replace the platform-neutral `skills/*/SKILL.md` files.

---

## How Skills Are Invoked

Once installed in a compatible AI agent, the relevant workflow should load automatically when the user's request matches the skill. Automatic loading depends on the platform.

These workflows are designed so the user does not need to guess which prompt to write or which tax issue to analyze first.

Example:

```
request -> "I need to organize my tax documents and figure out what I'm missing"
agent loads -> collecting-tax-documents
output -> document inventory, missing items, and next-step summary
```

Another example:

```
request -> "I had client meals and need to know where they belong"
agent loads -> organizing-t2125-8523-meals-and-entertainment
output -> field mapping, open questions, and caution notes
```

The user should not need to manually orchestrate the internal skill structure.

If a platform does not support automatic skill loading, the user can still use repo-read mode by naming the relevant skill file.

Example:

```text
request -> "Use skills/collecting-tax-documents/SKILL.md to organize my 2025 contractor tax documents"
agent reads -> skills/collecting-tax-documents/SKILL.md
output -> document inventory, missing items, and next-step summary
```

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

See [PRIVACY.md](PRIVACY.md) for information on how personal data is handled when using these workflows or submitting a package to Alex Teplov CPA.

---

## License

This repository is licensed under the MIT License.

These workflows are built from real accounting practice. If you adapt or use them, attribution is appreciated. See the `LICENSE` file for details.

---

## About

Built by [Alex Teplov, CPA](https://teplov.ca).

These workflows are built from real accounting practice focused on Canadian IT contractors. They are designed around a simple reality: many clients already use AI for tax questions, but they need better structure, clearer boundaries, and a more reliable preparation process before filing or CPA review.

- [teplov.ca](https://teplov.ca/): IT contractor tax practice
- [LinkedIn](https://www.linkedin.com/in/alex-teplov)
