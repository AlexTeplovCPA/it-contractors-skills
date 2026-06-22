# Codex usage

Codex can use this repository in two practical ways.

## 1. Repo-read mode

Open this repository in Codex and ask Codex to use a specific skill file.

Example:

```text
Use skills/collecting-tax-documents/SKILL.md to organize my 2025 Canadian IT contractor tax documents.
```

Another example:

```text
Use skills/checking-gst-hst/SKILL.md on this GST/HST records file and tell me what is missing.
```

In this mode, Codex reads the selected `SKILL.md`, follows the workflow, and reads referenced files only when needed.

## 2. Installed-skill mode

Install individual folders from `skills/` into the Codex skills directory used by your environment.

Common locations are:

```text
$CODEX_HOME/skills/
~/.codex/skills/
```

Copy the individual skill folders, not the whole repository, unless your Codex setup supports repository-level skill bundles.

Example:

```text
~/.codex/skills/collecting-tax-documents/SKILL.md
~/.codex/skills/checking-gst-hst/SKILL.md
~/.codex/skills/generating-cpa-handoff-summary/SKILL.md
```

Once installed, the user should be able to ask naturally:

```text
I am a Canadian IT contractor. Help me prepare my 2025 tax package for my CPA.
```

Codex should match the request to the relevant skill based on the `name` and `description` fields.

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

Codex should use these workflows to organize information, flag missing support, and prepare summaries.

Codex should not use this repository to provide final tax advice, determine filing positions, conclude PSB status, conclude employment status, or replace CPA review.
