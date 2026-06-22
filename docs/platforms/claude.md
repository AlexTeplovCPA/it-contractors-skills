# Claude usage

Claude can use this repository as a set of workflow skills, but the workflows are not Claude-specific.

The canonical files are still the folders under `skills/`. `CLAUDE.md` is only a Claude-facing adapter for repo-level guidance.

## Repo context mode

Open the repository in Claude or provide the relevant skill folder as project context.

Example:

```text
Use skills/identifying-expense-categories/SKILL.md to organize these contractor expenses.
```

Claude should read the selected `SKILL.md`, follow the workflow, and load referenced files only when needed.

## Skill-install mode

If using a Claude environment that supports reusable skills, package or install individual folders from `skills/` according to that environment's current instructions.

Install the skill folders themselves, not a rewritten Claude-only version of the workflow.

## Adapter rule

When updating this repository:

- keep `skills/*/SKILL.md` provider-neutral
- keep Claude-specific setup notes in `CLAUDE.md` or this file
- do not introduce Claude-only phrasing into canonical skill workflows

## Boundaries

Claude should use these workflows to organize information, flag missing support, and prepare summaries.

Claude should not use this repository to provide final tax advice, determine filing positions, conclude PSB status, conclude employment status, or replace CPA review.
