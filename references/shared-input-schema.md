# Shared Input Schema

Use this schema to normalize case information before skill-specific logic begins.

The purpose of this schema is consistency. Different input modes may be used:

- chat answers
- uploaded slips
- screenshots
- CSV files
- bookkeeping exports
- transaction logs
- summaries prepared by the user

Regardless of source, normalize information into the same structure.

This schema is internal. The end user does not need to see it.

---

## Top-Level Structure

```yaml
case_id:
tax_year:
engagement_mode:
user_profile:
facts:
documents:
transactions:
form_context:
review_state:
output_preferences:
```

---

## Field Definitions

### case_id

Unique identifier for the case.

```yaml
case_id: "itc-2025-001"
```

### tax_year

The tax year being organized.

```yaml
tax_year: 2025
```

### engagement_mode

The intended outcome for the case.

Allowed values:

- `self_entry`
- `cpa_handoff`
- `mixed`
- `unknown`

```yaml
engagement_mode: "self_entry"
```

### user_profile

Basic context about the user and business structure.

```yaml
user_profile:
  residency_country: "Canada"
  province_or_territory: "Ontario"
  profession: "IT contractor"
  business_structure: "sole_proprietor"
```

Suggested fields:

- `residency_country`
- `province_or_territory`
- `profession`
- `business_structure`

### facts

Normalized facts gathered from the user or extracted from documents.

```yaml
facts:
  business_activity:
    description: "software development consulting"
    active_all_year: true

  income_channels:
    - channel_type: "direct_client"
      label: "Client A"
      country: "Canada"
      currency: "CAD"
    - channel_type: "platform"
      label: "Upwork"
      country: "United States"
      currency: "USD"

  slips_received:
    t4: false
    t4a: true
    rrsp: true

  gst_hst:
    registered: true
    filing_frequency: "quarterly"

  home_office:
    claimed_or_expected: true

  vehicle_use:
    claimed_or_expected: false
```

Suggested fact areas:

- `business_activity`
- `income_channels`
- `slips_received`
- `gst_hst`
- `home_office`
- `vehicle_use`
- `instalments`
- `foreign_income`
- `corporate_overlap`

### documents

Tracks uploaded or referenced support.

```yaml
documents:
  slips:
    - doc_id: "doc-001"
      doc_type: "T4A"
      status: "received"

  summaries:
    - doc_id: "doc-010"
      doc_type: "platform_income_summary"
      source_name: "Upwork"
      status: "received"

  expense_support:
    - doc_id: "doc-020"
      doc_type: "expense_log"
      status: "received"
```

Allowed document status values:

- `received`
- `mentioned_not_provided`
- `missing`
- `not_applicable`
- `unclear`

### transactions

Normalized structured financial records.

```yaml
transactions:
  income_items:
    - txn_id: "inc-001"
      date: "2025-03-14"
      payer: "Client A"
      amount: 5000
      currency: "CAD"
      source_type: "invoice"

  expense_items:
    - txn_id: "exp-001"
      date: "2025-05-18"
      vendor: "Restaurant X"
      amount: 126.40
      currency: "CAD"
      source_type: "card_transaction"
```

Suggested fields:

- `txn_id`
- `date`
- `payer` or `vendor`
- `description`
- `amount`
- `currency`
- `source_type`
- `linked_document_ids`
- `preliminary_form_mapping`
- `confidence`

### form_context

Tracks which forms or sections appear relevant.

```yaml
form_context:
  T2125:
    relevant: true
    candidate_fields:
      - "gross_business_income"
      - "8523"
      - "business_use_of_home"

  T1:
    relevant: true
    candidate_fields:
      - "rrsp_deduction"
      - "t4_income"
      - "t4a_income"
```

### review_state

Tracks completeness, flags, and unresolved questions.

```yaml
review_state:
  completeness:
    income: "partial"
    expenses: "partial"
    slips: "complete"

  flags:
    - type: "missing_support"
      topic: "foreign_income"
      detail: "Platform summary mentioned but not provided"

  open_questions:
    - topic: "income"
      prompt: "Do you have a full invoice summary for direct client work?"

  status:
    overall: "clarification_required"
```

Suggested completeness values:

- `complete`
- `partial`
- `missing`
- `not_applicable`
- `unclear`

Suggested overall status values:

- `ready_for_entry`
- `clarification_required`
- `cpa_review_recommended`
- `incomplete`
- `out_of_scope`

### output_preferences

Controls final presentation style.

```yaml
output_preferences:
  final_format: "grouped_by_form"
  include_caution_notes: true
  include_missing_items: true
```

---

## Minimum Viable Input Schema

If a skill only needs a lighter version, use at minimum:

```yaml
case_id:
tax_year:
engagement_mode:
user_profile:
facts:
documents:
review_state:
```

---

## Skill Use Rule

Skills should:

- read from this structure where possible
- add normalized facts rather than invent new ad hoc categories
- preserve uncertainty
- avoid duplicating the same fact in different formats