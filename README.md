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

## How the Skills Work Together

The skills follow a structured preparation sequence. They can be run in order or individually depending on the situation.

The workflow moves from document collection → income and expense organization → compliance checks → CPA-ready package.

## Current Skill Map

### Intake

- `collecting-tax-documents-it-contractors`
- `normalizing-uploads-it-contractors`

### Income and Compliance

- `identifying-income-sources-it-contractors`
- `checking-gst-hst-it-contractors`
- `collecting-foreign-income-support-it-contractors`
- `reconciling-income-to-deposits-it-contractors`

### Expense and Support

- `classifying-expenses-it-contractors`
- `collecting-home-office-support-it-contractors`
- `collecting-vehicle-support-it-contractors`

### Incorporated Contractor Risk Areas

- `screening-psb-risk-it-contractors`
- `reviewing-shareholder-transactions-it-contractors`
- `collecting-owner-compensation-records-it-contractors`

### Handoff

- `preparing-cpa-t1-package-it-contractors`
- `preparing-cpa-t2-package-it-contractors`
- `validating-readiness-it-contractors`

## Planned Repository Structure

```text
skills/
  collecting-tax-documents-it-contractors/
    SKILL.md
    agents/
      openai.yaml
    references/
      checklist-t1.md
      checklist-t2.md

  normalizing-uploads-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  identifying-income-sources-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  checking-gst-hst-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  collecting-foreign-income-support-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  reconciling-income-to-deposits-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  classifying-expenses-it-contractors/
    SKILL.md
    agents/
      openai.yaml
    references/
      vendor-categories.md

  collecting-home-office-support-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  collecting-vehicle-support-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  screening-psb-risk-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  reviewing-shareholder-transactions-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  collecting-owner-compensation-records-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  preparing-cpa-t1-package-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  preparing-cpa-t2-package-it-contractors/
    SKILL.md
    agents/
      openai.yaml

  validating-readiness-it-contractors/
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

## Related Repositories

[**cpa-skills**](https://github.com/alexteplovcpa/cpa-skills)  
Practice-tested AI workflow skills for CPAs and bookkeepers. Practitioner-facing workflows for bookkeeping review, T1, T2, client communication, and CRA research.

[**ecommerce-skills**](https://github.com/alexteplovcpa/ecommerce-skills)  
Accounting workflows for Canadian e-commerce sellers, including reconciliation, inventory, COGS, and GST/HST handling.

## About

Built by [Alex Teplov, CPA](https://www.linkedin.com/in/alex-teplov/).

These workflows come from real work with Canadian IT contractors. The goal is to make the preparation stage more structured, reduce back-and-forth with clients, and allow CPAs to spend more time on judgment rather than reconstruction.
