# Shared Output Schema

Use this schema for all skill results.

The purpose of this schema is to keep skills modular but interoperable. A broad intake skill, a narrow field skill, and a final summary skill should all be able to work from compatible outputs.

This schema is internal. The end user does not need to see it exactly in this format.

---

## Top-Level Structure

```yaml
skill_result:
  skill_name:
  skill_version:
  case_id:
  tax_year:
  scope:
  inputs_used:
  facts_accepted:
  mappings_proposed:
  support_assessment:
  flags:
  open_questions:
  decisions_deferred:
  downstream_effects:
  status:
  confidence:
  client_safe_summary:
  internal_notes:
```

---

## Field Definitions

### skill_name

The skill identifier.

```yaml
skill_name: "t2125-8523-meals-and-entertainment"
```

### skill_version

Optional but recommended.

```yaml
skill_version: "1.0.0"
```

### case_id

Case reference.

```yaml
case_id: "itc-2025-001"
```

### tax_year

Tax year.

```yaml
tax_year: 2025
```

### scope

Defines what the skill reviewed.

```yaml
scope:
  form: "T2125"
  field_refs:
    - "8523"
  topic: "meals_and_entertainment"
  mode: "field_review"
```

Allowed mode values:

- `intake`
- `field_review`
- `cross_cutting_review`
- `synthesis`

### inputs_used

Tracks what the skill relied on.

```yaml
inputs_used:
  facts:
    - "income_channels"
  documents:
    - "doc-001"
  transactions:
    - "exp-001"
  assumptions_made:
    - "user-provided category treated as provisional"
```

### facts_accepted

Facts this skill treated as usable.

```yaml
facts_accepted:
  - fact: "Restaurant charge appears meal-related"
    source: "transaction_record"
    confidence: "high"
```

### mappings_proposed

The core mapping output.

```yaml
mappings_proposed:
  - mapping_id: "map-001"
    form: "T2125"
    field_ref: "8523"
    item_ref: "exp-001"
    proposed_treatment: "include"
    amount: 126.40
    currency: "CAD"
    rationale_short: "Meal expense appears business-related"
    confidence: "medium"
```

Allowed `proposed_treatment` values:

- `include`
- `exclude`
- `exclude_or_clarify`
- `split_required`
- `carry_to_other_field`
- `needs_manual_review`
- `not_applicable`

### support_assessment

Summarizes evidence strength.

```yaml
support_assessment:
  evidence_status: "partial"
  evidence_items:
    - type: "receipt"
      status: "received"
    - type: "business_purpose_explanation"
      status: "missing"
  support_gap_summary:
    - "Business purpose not documented"
```

Allowed `evidence_status` values:

- `sufficient`
- `partial`
- `weak`
- `none`

### flags

Standardized issues.

```yaml
flags:
  - flag_id: "f-001"
    type: "missing_support"
    severity: "medium"
    topic: "meals_and_entertainment"
    detail: "Receipt missing for one charge"
```

Allowed `severity` values:

- `low`
- `medium`
- `high`

Suggested `type` values:

- `missing_support`
- `unclear_classification`
- `possible_duplication`
- `possible_personal_component`
- `possible_capital_item`
- `cross_border_issue`
- `gst_hst_issue`
- `reasonableness_concern`
- `mapping_uncertain`
- `software_calculated_field`

### open_questions

Questions that still matter.

```yaml
open_questions:
  - question_id: "q-001"
    audience: "client"
    topic: "meals_and_entertainment"
    prompt: "What was the business purpose of this meal?"
    related_item_refs:
      - "exp-001"
    blocking: true
```

Allowed `audience` values:

- `client`
- `practitioner`
- `either`

### decisions_deferred

What the skill intentionally did not conclude.

```yaml
decisions_deferred:
  - "No final conclusion made on deductibility"
```

### downstream_effects

What later skills may need to use.

```yaml
downstream_effects:
  triggers:
    - "generate-self-entry-summary"
    - "generate-missing-items-summary"
  affected_forms:
    - "T2125"
  affected_fields:
    - "8523"
```

### status

Final state of this skill's result.

```yaml
status:
  result: "clarification_required"
  ready_for_form_entry: false
  ready_for_cpa_handoff: true
```

Allowed `result` values:

- `ready_for_entry`
- `clarification_required`
- `cpa_review_recommended`
- `incomplete`
- `out_of_scope`
- `not_applicable`

### confidence

Overall confidence in the result.

```yaml
confidence:
  overall: "medium"
  reason: "Item appears relevant but support is incomplete"
```

Allowed values:

- `high`
- `medium`
- `low`
- `unknown`

### client_safe_summary

Plain-language result that can be shown directly.

```yaml
client_safe_summary:
  summary: "Some meal expenses appear business-related, but more detail is needed before all of them can be entered confidently."
  missing_items:
    - "Business purpose for restaurant charge"
  caution_notes:
    - "Do not rely on unsupported meal charges without clarification."
```

### internal_notes

Optional internal guidance for later synthesis.

```yaml
internal_notes:
  reviewer_style_note: "Weak descriptions on several items"
  synthesis_hint: "Group with travel meals if travel skill also triggers"
```

---

## Minimum Viable Output Schema

If a skill only needs a smaller version, it must still include:

```yaml
skill_result:
  skill_name:
  case_id:
  scope:
  mappings_proposed:
  flags:
  open_questions:
  status:
  confidence:
  client_safe_summary:
```

---

## Required Output Rule

Every skill in this repository should end with at least:

- `mappings_proposed`
- `flags`
- `open_questions`
- `status`
- `client_safe_summary`

Broad intake skills may have fewer field mappings. Narrow field skills should usually have stronger mapping detail. Final synthesis skills may rely more heavily on aggregated prior results.

---

## Skill Use Rule

Skills should:

- use the shared output shape
- preserve uncertainty where support is incomplete
- separate mapping from unresolved questions
- avoid giving filing advice through the output language
- produce client-safe summaries in plain language