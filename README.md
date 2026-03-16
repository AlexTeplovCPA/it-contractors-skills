# selfemployed-skills

AI workflow skills for Canadian self-employed professionals and the accountants who serve them.

This repository contains structured AI instruction workflows for the tax and bookkeeping work specific to self-employed Canadians. The skills are built from real practice: not generic accounting scenarios, but the actual patterns that appear when working with IT contractors, mortgage agents, trades, and real estate professionals in Canada.

These skills are a domain-specific extension of [cpa-skills](https://github.com/alexteplovcpa/cpa-skills).

---

## Who This Is For

**Practitioners** working with self-employed clients who want consistent, repeatable workflows for common tasks.

**Self-employed professionals** working with their own accountant who want to understand how their books and returns are structured.

The domains this repository covers:

- IT contractors and consultants
- Mortgage agents and brokers
- Trades contractors
- Real estate professionals

---

## Skill Areas

### Income Classification
Identifying revenue sources, separating employment income from self-employment income, and handling situations where the classification is not straightforward.

### Expense Treatment
Applying the correct tax treatment to common self-employed expense categories. Home office, vehicle, meals, professional development, and profession-specific deductions.

### GST/HST
Registration thresholds, collection obligations, input tax credits, and filing requirements for self-employed Canadians across different revenue levels.

### CRA Research
Structured workflows for interpreting CRA guidance, identifying relevant interpretation bulletins, and applying current administrative positions to client-specific scenarios.

### T1
Supporting preparation of T1 personal tax returns for self-employed professionals. Income reporting, allowable deductions, and treatment of business income alongside other income sources.

### T2
Supporting preparation of T2 corporate tax returns for incorporated self-employed professionals. Applicable where clients have moved from sole proprietorship to a professional corporation.

---

## How to Use a Skill

Once installed, the agent discovers and loads the relevant skill automatically based on your request. You do not need to invoke it manually.

Example:

```text
request → "prepare T1 for self-employed client"
agent loads → t1
input → client income and expense summary
output → flagged items and preparation notes
```

For explicit invocation in Claude Code or Codex CLI, reference the skill by name in your prompt.

These skills follow the open [Agent Skills standard](https://agentskills.io) and work across Claude, OpenAI Codex, and Google Gemini CLI without modification.

---

## Installation

**Claude (claude.ai):**
1. Download or clone this repository
2. Zip the skill folder you want to install
3. Go to Settings > Capabilities > Skills > Upload skill

**Claude Code:**
Place the skill folder in `~/.claude/skills/`

**OpenAI Codex:**
Place the skill folder in `~/.agents/skills/`

**Google Gemini CLI:**
Place the skill folder in `~/.gemini/skills/` or `~/.agents/skills/`

---

## Example Data

The `examples/` directory contains sample datasets for testing skills without using real client data.

Example files may include:

```text
examples/
   income-summary.csv
   expense-log.csv
   gst-hst-records.csv
   cra-correspondence/
      sample-notice.pdf
   t1-package/
      t1-sample-documents/
   t2-package/
      t2-sample-documents/
```

These files simulate typical inputs for self-employed professional engagements.

---

## Skill Roadmap

| Area | Skill | Status |
|---|---|---|
| Income | `income-classification` | Roadmap |
| Expenses | `expense-treatment` | Roadmap |
| CRA | `cra-research` | Roadmap |
| Tax | `gsthst` | Roadmap |
| Tax | `t1` | Roadmap |
| Tax | `t2` | Roadmap |

---

## Repository Structure

Each skill is a self-contained folder with a `SKILL.md` file. Optional `scripts/`, `references/`, and `assets/` subdirectories can be added inside a skill folder as needed.

```text
income/
   income-classification/
      SKILL.md

expenses/
   expense-treatment/
      SKILL.md

cra/
   cra-research/
      SKILL.md

tax/
   gsthst/
      SKILL.md
   t1/
      SKILL.md
   t2/
      SKILL.md

examples/
   income-summary.csv
   expense-log.csv
   gst-hst-records.csv
   cra-correspondence/
      sample-notice.pdf
   t1-package/
      t1-sample-documents/
   t2-package/
      t2-sample-documents/
```

---

## Related Repositories

**[cpa-skills](https://github.com/alexteplovcpa/cpa-skills)**
The main repository. Full accounting workflow pipeline from document ingestion through CPA-level review and tax preparation.

**[ecommerce-skills](https://github.com/alexteplovcpa/ecommerce-skills)**
Specialized workflows for Canadian e-commerce sellers.

---

## About

Built by [Alex Teplov, CPA](https://www.linkedin.com/in/alex-teplov/).

I run two specialized accounting practices in Canada and build these workflows to solve operational bottlenecks encountered in real accounting work.
