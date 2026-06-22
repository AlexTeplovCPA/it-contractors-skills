# Gemini usage

Gemini can use this repository as a set of workflow skills, but the workflows are not Gemini-specific.

The canonical files are the folders under `skills/`. `GEMINI.md` is only a Gemini-facing adapter for repo-level guidance.

## Repo context mode

Open the repository in Gemini CLI or another Gemini environment that can read local files.

Example:

```text
Use skills/collecting-tax-documents/SKILL.md to organize my 2025 Canadian IT contractor tax documents.
```

Another example:

```text
Use skills/checking-gst-hst/SKILL.md on this GST/HST records file and tell me what is missing.
```

Gemini should read the selected `SKILL.md`, follow the workflow, and load referenced files only when needed.

## Gemini CLI context

Gemini CLI can use `GEMINI.md` as a project context file. When this repository is opened in Gemini CLI, `GEMINI.md` should tell Gemini how to treat the skill folders and where the platform-neutral boundaries are.

The expected pattern is:

1. Start Gemini CLI in the repository.
2. Ask naturally or name a specific skill file.
3. Let Gemini read the relevant `SKILL.md`.
4. Provide records through chat, uploads, or pasted tables where the environment supports them.
5. Generate a self-entry summary, CPA handoff summary, or missing-items summary.

## Prompt examples

Broad preparation request:

```text
I am a Canadian IT contractor. Help me prepare my 2025 tax package for my CPA.
```

Specific skill request:

```text
Use skills/identifying-expense-categories/SKILL.md to organize these contractor expenses.
```

Final output request:

```text
Use skills/generating-cpa-handoff-summary/SKILL.md to turn the prior outputs into a CPA handoff summary.
```

## Routing pattern

For a broad request, start with one of:

- `collecting-tax-documents`
- `identifying-income-sources`
- `identifying-expense-categories`

For a focused issue, use the narrowest relevant skill:

- GST/HST records: `checking-gst-hst`
- U.S. clients or platform income: `reviewing-foreign-platform-and-us-income`
- home office: `organizing-t2125-business-use-of-home`
- meals: `organizing-t2125-8523-meals-and-entertainment`
- capital assets: `organizing-t2125-capital-assets-and-cca`
- PSB fact gathering: `reviewing-psb-risk-facts`

For final output, use one of:

- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

## Boundaries

Gemini should use these workflows to organize information, flag missing support, and prepare summaries.

Gemini should not use this repository to provide final tax advice, determine filing positions, conclude PSB status, conclude employment status, or replace CPA review.

## Adapter rule

When updating this repository:

- keep `skills/*/SKILL.md` provider-neutral
- keep Gemini-specific setup notes in `GEMINI.md` or this file
- do not introduce Gemini-only phrasing into canonical skill workflows
