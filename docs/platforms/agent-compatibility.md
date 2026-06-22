# Agent compatibility

This repository is designed to be usable by multiple AI agents. The canonical content is the set of folders under `skills/`.

Each skill is a plain Markdown workflow with YAML frontmatter. The workflow should remain useful even if the agent does not have native skill discovery.

## Canonical files

- `skills/*/SKILL.md`: platform-neutral workflow instructions
- `skills/*/references/`: skill-specific reference files
- `references/`: shared schemas and templates
- `examples/`: sample inputs and outputs for testing or illustration
- `docs/`: repository-level policy, scope, and platform guidance

## Minimum agent capabilities

An agent can use this repository if it can:

- read Markdown files
- follow procedural instructions
- ask follow-up questions
- preserve uncertainty when facts are incomplete
- produce structured Markdown or schema-like output
- read referenced files when a skill tells it to

## Optional capabilities

The experience is better when an agent can:

- automatically discover skills from YAML frontmatter
- accept uploaded files or pasted tables
- inspect CSV, PDF, spreadsheet, or image text
- maintain context across a multi-step workflow
- save or export the final summary

These optional capabilities should improve the user experience, but the canonical skill content should not depend on them.

## Platform adapters

Platform-specific files explain how to expose the same workflows in a given agent.

Current adapters:

- `AGENTS.md` for Codex
- `CLAUDE.md` for Claude
- `GEMINI.md` for Gemini
- `docs/platforms/codex.md`
- `docs/platforms/claude.md`
- `docs/platforms/gemini.md`

Adapters may explain installation paths, activation behavior, or prompting patterns. They should not change the tax workflow boundaries.

## Compatibility rule

When adding or editing a skill, write the `SKILL.md` file for a capable AI agent, not for a specific provider.

Use provider names only in platform adapter docs, examples about installation, or privacy wording that explains the user's chosen AI platform.
