---
name: reviewing-psb-risk-facts
description: Review personal services business risk facts for a Canadian IT contractor operating through a corporation. Use when the user earns contract income through a corporation and there is a risk the arrangement may be characterized as a personal services business by CRA. Accepts engagement descriptions, client relationships, and incorporation facts. Produces a provisional PSB risk fact summary with flags and downstream routing. This skill organizes facts only and does not determine PSB status.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-04-18
---

# Reviewing PSB Risk Facts

Review personal services business risk facts for a Canadian IT contractor operating through a corporation.

## Core Rules

- Organize PSB-relevant facts, do not determine PSB status.
- Do not conclude that the user is or is not a personal services business.
- Do not advise on restructuring arrangements.
- Do not determine tax consequences of a PSB finding.
- Preserve uncertainty where client relationship or incorporation facts are incomplete.
- Flag significant risk indicators for CPA review.
- Do not state that the user's arrangement is compliant.
- Do not state that the user is ready to file.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Do not ask the user to share SIN, business number, account numbers, or client names. Use general descriptions and rounded amounts.

Accept any of:

- description of the user's corporate structure
- description of client relationships and contract terms
- prior year T2 return summary
- user explanation in chat

Minimum useful input:

- description of how business income is earned
- whether income flows through a corporation
- description of the primary client relationship

Read from the shared input schema where available: `case_id`, `tax_year`, `engagement_mode`, `user_profile`, `facts.business_activity`, `facts.corporate_structure`, `form_context`, `review_state`.

Read from prior skill outputs where available: `identifying-income-sources`.

## Workflow

### 1. Confirm PSB review is relevant

Check whether the user earns income through a corporation. If the user is self-employed as an individual with no corporation, PSB does not apply to their T1 filing directly. Note this and return not_applicable unless the user has indicated a corporation is involved.

### 2. Organize incorporation and structure facts

Identify:

- whether the user operates through a corporation
- the nature of the business activity
- whether the corporation has employees other than the user
- whether the user is the sole or primary worker

### 3. Organize client relationship facts

Identify:

- number of active clients during the year
- whether income is concentrated with one primary client
- whether the client controls the manner of work
- whether the user provides services at the client's premises
- whether the user uses the client's tools or equipment
- whether the user bears financial risk
- whether the user could subcontract the work

Do not draw conclusions. Collect facts only.

### 4. Assess the concentration of income

Note whether one client accounts for the majority of revenue. High concentration with a single client is a common PSB risk indicator.

### 5. Identify PSB risk indicators present

Review collected facts against common PSB indicators:

- single dominant client
- client controls manner of work
- user works exclusively at client site
- user uses client tools
- user cannot subcontract
- user has no other employees
- relationship resembles employment

Note how many indicators are present. Do not score or conclude.

### 6. Flag issues that affect readiness

Flag issues such as:

- high client concentration
- relationship facts suggest possible PSB
- insufficient facts to assess risk
- user has not confirmed whether a corporation is involved
- prior T2 filing may be affected

Only flag issues that materially affect readiness.

### 7. Prepare downstream routing

Indicate likely downstream uses:

- `generating-cpa-handoff-summary`
- `generating-missing-items-summary`

Do not run those workflows inside this skill.

## Resource Map

- `../../references/shared-input-schema.md`: read to populate input fields
- `../../references/shared-output-schema.md`: read to format output fields

## Output

Return using the shared output schema. Include:

- `facts_accepted`: usable PSB-relevant facts the skill relied on
- `mappings_proposed`: use entries such as risk indicator present, risk indicator absent, unclear, needs_manual_review, not_applicable
- `flags`: use `missing_support`, `mapping_uncertain`, `unclear_classification` where applicable; use a specific PSB risk flag where indicators are present
- `open_questions`: only questions needed to resolve meaningful uncertainty; typical useful questions include: Do you operate through a corporation? How many clients did you have this year? Does one client account for most of your revenue? Does the client control how you do your work?
- `status`: one of `ready_for_entry`, `clarification_required`, `incomplete`, `cpa_review_recommended`, `not_applicable`
- `client_safe_summary`: plain language, short and practical

Also include a PSB risk fact summary grouped into:

- structure facts (corporation, employees, activity)
- client relationship facts (number of clients, concentration, control, tools, subcontracting)
- risk indicators present
- risk indicators absent or unclear
- open issues requiring CPA review

## Status Guidance

- `ready_for_entry`: PSB risk facts are organized and no significant risk indicators are present
- `clarification_required`: some relevant facts are available but client relationship or structure details are incomplete
- `cpa_review_recommended`: one or more material PSB risk indicators are present
- `incomplete`: insufficient facts to assess PSB risk meaningfully
- `not_applicable`: no corporation involved, PSB not applicable to this filing

Do not use `ready_for_entry` if material risk indicators are present. Route to cpa_review_recommended in that case.

## Validation

- Corporate structure is confirmed or flagged as unresolved.
- Client relationship facts are listed or flagged as missing.
- Each PSB risk indicator is noted as present, absent, or unclear.
- At least one downstream skill is identified in routing.
- `status` is one of the five standard values.
- `client_safe_summary` is present and contains no tax advice.
