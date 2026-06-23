---
name: organizing-intake-folder
description: Rename and organize raw files in a client intake folder before tax review begins. Use when a client has uploaded documents with inconsistent or generic file names and the folder needs to be structured before skills like collecting-tax-documents or identifying-income-sources can run effectively. Reads file names and any available content, proposes a standardized naming scheme, and outputs a rename plan with a folder structure. Does not open or interpret document contents for tax purposes.
metadata:
    author: Teplov CPA
    version: 1.0
    updated: 2026-06-23
---

# Organizing Intake Folder

Rename and organize raw client files before tax review begins.

## Core Rules

- Rename files only. Do not interpret contents for tax purposes.
- Do not open files to extract financial data. Read file names and visible metadata only.
- Do not determine whether a document is relevant, deductible, or complete.
- Preserve all original files. Output a rename plan, not a destructive operation.
- Do not delete, archive, or move files without explicit instruction.
- Flag files that cannot be identified from name alone.
- Use this phrase where relevant: "That is outside what this workflow covers. It is a question for a CPA before you file."

## Inputs

Accept any of:

- a list of file names pasted into chat
- a directory listing
- a folder shared via OneDrive or SharePoint sync

Minimum useful input:

- a list of file names in the intake folder
- the tax year if known
- the client's business structure if known (sole proprietor, incorporated, or mixed)

Do not ask for SIN, business number, account numbers, or client names.

## Naming Convention

Use this format for all renamed files:

```
[document-type]-[tax-year].[extension]
```

Examples:

```
t4-2024.pdf
t4a-2024.pdf
rrsp-slip-2024.pdf
invoice-log-2024.xlsx
expense-log-2024.csv
gst-hst-return-q4-2024.pdf
instalment-payment-2024.pdf
noa-2023.pdf
platform-summary-upwork-2024.pdf
platform-summary-stripe-2024.pdf
bank-statement-jan-2024.pdf
engagement-letter-2024.pdf
prior-year-summary-2023.pdf
```

Rules:

- lowercase only
- hyphens between words, no underscores or spaces
- include tax year in every name
- include platform or source name when it disambiguates (e.g. `platform-summary-upwork-2024.pdf`)
- include month or quarter for periodic documents (e.g. `bank-statement-jan-2024.pdf`, `gst-hst-return-q4-2024.pdf`)
- preserve the original file extension

## Document Type Labels

Use these standard labels in file names:

| Document | Label |
|---|---|
| T4 slip | `t4` |
| T4A slip | `t4a` |
| T5 slip | `t5` |
| RRSP contribution slip | `rrsp-slip` |
| FHSA contribution slip | `fhsa-slip` |
| Notice of assessment | `noa` |
| Invoice log or summary | `invoice-log` |
| Expense log or summary | `expense-log` |
| Bank statement | `bank-statement` |
| Credit card statement | `card-statement` |
| Platform income summary | `platform-summary-[platform]` |
| GST/HST return | `gst-hst-return-[period]` |
| GST/HST remittance confirmation | `gst-hst-remittance-[period]` |
| Instalment payment confirmation | `instalment-payment` |
| Prior-year return summary | `prior-year-summary` |
| Engagement letter | `engagement-letter` |
| Other identified document | use a descriptive kebab-case label |
| Unidentified document | `unidentified-[sequence]` |

## Workflow

### 1. Read the folder

List all files in the intake folder. Note:

- current file names
- file extensions
- any patterns in existing naming (date prefixes, scan numbers, client codes)

### 2. Identify each file

For each file, determine the most likely document type based on:

- file name keywords (e.g. "T4", "NOA", "Upwork", "invoice", "GST")
- file extension (e.g. `.pdf` for slips, `.csv` or `.xlsx` for exports)
- sequence or date in the name if present

If a file cannot be identified from the name alone, mark it as `unidentified` and flag it for manual review.

Do not open file contents to identify the document type.

### 3. Propose rename plan

For each file, output:

- original name
- proposed name
- confidence: `high`, `medium`, or `low`
- note if confidence is medium or low

### 4. Flag unresolved files

List any files that:

- could not be identified
- have ambiguous names that match more than one document type
- appear to be duplicates

Ask one clarifying question per unresolved file if needed.

### 5. Confirm before renaming

Present the full rename plan to the user before any files are renamed.

Do not rename files without explicit confirmation.

## Output

Return:

- **Rename plan**: table with original name, proposed name, confidence, and notes
- **Unresolved files**: list with reason and clarifying question if needed
- **Folder summary**: count of identified, unresolved, and flagged files
- **Downstream routing**: which skills are ready to run once renaming is confirmed

Example downstream routing after a complete rename:

- `collecting-tax-documents`: run first to inventory the organized folder
- `identifying-income-sources`: if invoice log or platform summaries are present
- `checking-gst-hst`: if GST/HST records are present

## Status Guidance

- `ready_for_entry`: all files identified and rename plan is complete
- `clarification_required`: one or more files could not be identified
- `incomplete`: folder appears to be missing major expected document types

## Validation

- Every file in the folder has a proposed name or is explicitly marked `unidentified`.
- No file is renamed without user confirmation.
- All proposed names follow the naming convention.
- Unresolved files are listed with a reason.
- At least one downstream skill is suggested if the folder contains tax documents.
