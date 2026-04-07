# it-contractors-skills

Client-facing AI workflow skills for Canadian IT contractors preparing for CPA review.

This repository is designed for the preparation layer before professional review. The skills guide users through structured workflows: collecting documents, organizing income and expenses, identifying missing items, surfacing higher-risk areas, and preparing a clean handoff package for a CPA.

These workflows are built from real accounting work with Canadian IT contractors. They do not replace CPA judgment, tax advice, or filing.

## Repository Purpose

This repository is public and client-facing.

Its role is to help Canadian IT contractors prepare their records before working with a CPA. The focus is on structured intake, document organization, issue spotting, and handoff preparation.

This is separate from [**cpa-skills**](https://github.com/alexteplovcpa/cpa-skills), which is practitioner-facing and designed for accountants and bookkeepers.

## Who This Is For

This repository is for:

- Canadian IT contractors who want to organize tax and bookkeeping information before CPA review
- sole proprietor and incorporated IT contractors preparing for T1 and T2 filings
- practitioners who want a consistent intake workflow for IT contractor clients

These skills organize what the user provides. A CPA reviews the file, confirms tax treatment, identifies gaps, and completes the return.

## Disclosure

These workflows organize information provided by the user. They do not verify completeness or accuracy, provide tax advice, determine final tax treatment, or create a professional relationship of any kind. Use of these skills does not replace review by a qualified CPA before filing.

## How the Skills Work Together

The skills follow a structured preparation sequence. They can be run in order or individually depending on the situation.

The workflow moves from document collection to income and expense organization, then to compliance checks and CPA-ready package preparation.

## Current Skill Map

### Intake

- `collecting-tax-documents`
- `normalizing-uploads`

### Income and Compliance

- `identifying-income-sources`
- `checking-gst-hst`
- `collecting-foreign-income-support`
- `reconciling-income-to-deposits`

### Expense and Support

- `classifying-expenses`
- `collecting-home-office-support`
- `collecting-vehicle-support`

### Incorporated Contractor Risk Areas

- `screening-psb-risk`
- `reviewing-shareholder-transactions`
- `collecting-owner-compensation-records`

### Handoff

- `preparing-cpa-t1-package`
- `preparing-cpa-t2-package`
- `validating-readiness`

## Planned Repository Structure

```text
skills/
  collecting-tax-documents/
    SKILL.md
    agents/
      openai.yaml
    references/
      checklist-t1.md
      checklist-t2.md

  normalizing-uploads/
    SKILL.md
    agents/
      openai.yaml

  identifying-income-sources/
    SKILL.md
    agents/
      openai.yaml

  checking-gst-hst/
    SKILL.md
    agents/
      openai.yaml

  collecting-foreign-income-support/
    SKILL.md
    agents/
      openai.yaml

  reconciling-income-to-deposits/
    SKILL.md
    agents/
      openai.yaml

  classifying-expenses/
    SKILL.md
    agents/
      openai.yaml
    references/
      vendor-categories.md

  collecting-home-office-support/
    SKILL.md
    agents/
      openai.yaml

  collecting-vehicle-support/
    SKILL.md
    agents/
      openai.yaml

  screening-psb-risk/
    SKILL.md
    agents/
      openai.yaml

  reviewing-shareholder-transactions/
    SKILL.md
    agents/
      openai.yaml

  collecting-owner-compensation-records/
    SKILL.md
    agents/
      openai.yaml

  preparing-cpa-t1-package/
    SKILL.md
    agents/
      openai.yaml

  preparing-cpa-t2-package/
    SKILL.md
    agents/
      openai.yaml

  validating-readiness/
    SKILL.md
    agents/
      openai.yaml

docs/
  repo-scope.md
  writing-rules.md

examples/
  income-summary.csv
  expense-log.csv
  gst-hst-records.csv
  t1-package/
  t2-package/
```

## Examples

The `examples/` folder contains sample inputs and outputs used during development and testing:

- income summaries
- expense logs
- GST/HST records
- sample T1 and T2 support packages

These are not templates for filing. They illustrate how structured outputs should look before CPA review.

## Installation

### Claude (claude.ai)
1. Download or clone this repository
2. Zip the individual skill folder you want to install
3. Go to Settings → Capabilities → Skills
4. Upload the skill ZIP

### Claude Code
Place the skill folder in:

```text
~/.claude/skills/
```

### OpenAI Codex
Place the skill folder in:

```text
~/.agents/skills/
```

### Google Gemini CLI
Place the skill folder in one of:

```text
~/.gemini/skills/
~/.agents/skills/
```

These skills follow a shared agent-skill style structure and are being developed primarily around Claude-style workflows. Behavior may vary across tools.

## How to Use the Repository

A user does not need to run every skill.

A typical path might look like this:

1. collect tax documents
2. normalize uploads
3. identify income sources
4. check GST/HST context if relevant
5. classify expenses
6. collect additional support for home office, vehicle, or foreign income if needed
7. review incorporated contractor risk areas where relevant
8. prepare the T1 package, T2 package, or both
9. validate readiness before CPA intake

## Example Workflow

```text
request: I need to get my IT contractor tax information ready for my CPA
skills used:
- collecting-tax-documents
- identifying-income-sources
- classifying-expenses
- preparing-cpa-t1-package

output:
- organized summaries
- missing item list
- CPA question list
- handoff package for review
```

## Related Repositories

[**cpa-skills**](https://github.com/alexteplovcpa/cpa-skills)  
Practice-tested AI workflow skills for CPAs and bookkeepers. Practitioner-facing workflows for bookkeeping review, T1, T2, client communication, and CRA research.

[**ecommerce-skills**](https://github.com/alexteplovcpa/ecommerce-skills)  
Accounting workflows for Canadian e-commerce sellers, including reconciliation, inventory, cost of goods sold, and GST/HST handling.

## About

Built by [Alex Teplov, CPA](https://www.linkedin.com/in/alex-teplov/).

These workflows come from real work with Canadian IT contractors. The goal is to make the preparation stage more structured, reduce back-and-forth with clients, and allow CPAs to spend more time on judgment rather than reconstruction.
