# GEMINI.md - Gemini adapter for it-contractors-skills

This is Gemini-facing repository guidance for `it-contractors-skills`.

The canonical workflows live in `skills/*/SKILL.md`. Treat those files as platform-neutral source material. Do not rewrite them to depend on Gemini, Codex, Claude, ChatGPT, or any other provider unless the change is limited to a platform adapter document.

Gemini-specific setup notes belong in this file or in `docs/platforms/gemini.md`, not inside canonical skill workflows.

## Working rules

- Keep the repository client-facing, IT-contractor-specific, and preparation-oriented.
- Preserve the boundary between organization and advice.
- Do not make final tax, legal, deductibility, PSB, GST/HST, or employment-status conclusions.
- Use the phrase from the relevant skill when a request falls outside scope: "That is outside what this workflow covers. It is a question for a CPA before you file."
- Do not ask users for SINs, business numbers, bank account numbers, account login details, or full client names.
- Use American spelling and avoid em dashes.
- Keep `SKILL.md` instructions operational. Write to the agent, not to the end user.

## Gemini usage

When a user asks to use this repository in Gemini:

1. Match the request to the relevant `skills/*/SKILL.md` frontmatter description.
2. Read the selected `SKILL.md`.
3. Read only the reference files named in that skill's resource map when they are needed.
4. Follow the workflow and output rules in the skill.
5. Route to another skill only when the current skill explicitly identifies that downstream need.

If automatic skill discovery is not available, use repo-read mode. The user can ask Gemini to follow a named file, such as:

```text
Use skills/collecting-tax-documents/SKILL.md to organize my 2025 contractor tax documents.
```

## Routing pattern

For broad preparation requests, start with one of:

- `collecting-tax-documents`
- `identifying-income-sources`
- `identifying-expense-categories`

For focused issues, use the narrowest relevant skill.

For final outputs, use one of:

- `generating-self-entry-summary`
- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

## Platform adapters

Platform-specific guidance belongs in:

- `AGENTS.md` for Codex repo-level guidance
- `CLAUDE.md` for Claude repo-level guidance
- `GEMINI.md` for Gemini repo-level guidance
- `docs/platforms/` for installation and compatibility notes

Do not put provider-specific installation details inside canonical skill instructions unless a skill genuinely requires that provider.
