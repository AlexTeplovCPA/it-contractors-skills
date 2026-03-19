---
name: identifying-income-sources
description: "Identifies and documents all income sources for a self-employed Canadian for the current tax year. Use when a self-employed Canadian needs to organize income before tax filing or CPA review. Trigger on: T4A, T4, invoices, self-employment income, income summary, prepare for CPA, organize my income, what income do I need to report, I don't know if I have everything, I need to pull together my income."
metadata:
  author: Alex Teplov
  version: 1.0.0
  category: tax-preparation
---

# Identifying Income Sources

**Workflow position:** First skill in the selfemployed-skills sequence. Run before `checking-gst-hst`, `classifying-expenses`, and `preparing-cpa-review`. Those skills assume this step is complete or in progress.

**Core constraint:** This workflow organizes information. It does not verify completeness or accuracy. State this to the user before starting.

---

## Role

Do not give tax advice. When the user asks what is taxable, how to treat an unusual payment, or whether they need to file a specific form, redirect the advisory part and continue the workflow.

---

## Workflow

Copy this checklist at the start of each session:

```
Progress:
- [ ] Step 1: Open conversation and deliver data notice
- [ ] Step 2: Review uploaded documents
- [ ] Step 3: Fill gaps
- [ ] Step 4: Produce income summary
```

### Step 1: Open the Conversation

State before asking any questions:

1. This workflow builds a complete income summary for the tax year.
2. "This process relies on what you provide. It will not catch everything on its own."
3. Deliver the data handling notice below.
4. Ask which tax year they are filing for.
5. Ask them to upload income documents: T4A slips, T4 slips, invoices, foreign payment confirmations, platform earnings summaries, or bank statements.

**Data handling notice. State before they upload anything:**

> Do not type your SIN, business number, or client names into this conversation. Amounts and income types are all we need. If uploading photos of tax slips, cover or black out your SIN before photographing. Avoid sharing sensitive business details you would not be comfortable storing in a third-party system. Your inputs and uploaded documents may be stored by this AI tool according to its policies. Review those policies before proceeding if you have concerns.

### Step 2: Review Uploaded Documents

Assume documents are incomplete unless the user clearly states otherwise. Do not assume totals from a single document represent all income for that source.

When documents are uploaded:

- Extract from each: income source type, amount in CAD, payer type (not name), date (if visible), notes on unclear or missing information
- If unreadable: ask the user to retake the photo. If retaking is not possible, ask them to enter the amount and type manually and flag as "manually entered, verify against original"
- Complete document review before asking any questions

After reviewing, state:
1. What income sources were confirmed
2. What was unclear or unreadable
3. What common income sources may be missing based on what was uploaded

### Step 3: Fill the Gaps

Ask one question at a time. Wait for the answer before asking the next. Skip areas already confirmed from documents. Cover in order:

**Employment income:** Any T4 employment income in addition to self-employment? Includes part-time, casual, or any work where an employer deducted CPP and EI.

**Self-employment income without a slip:** Any invoiced Canadian clients who did not issue a T4A? All invoiced income is taxable whether or not a slip was issued.

**Cash, e-transfer, or informal payments:** Any cash, e-transfer, or informal payments not reflected in invoices or slips?

**Platform income:** Any income through Upwork, Fiverr, Toptal, PayPal, or similar platforms not captured in uploaded documents?

**Foreign income:** Any payment from clients outside Canada? If yes, ask for original currency and amount. Flag for CAD conversion using a reasonable method, often the Bank of Canada annual average exchange rate for the tax year. Do not convert. Flag in Notes column.

**Other income:** Any amounts that do not clearly relate to regular business or employment activity. Do not default informal payments here unless clearly not business-related.

**Bank deposit cross-check:** Ask the user to scan bank statements for deposits not already captured. Treat as a final completeness check. If unmatched deposits are identified, keep in the table as "Not yet confirmed" rather than excluding them.

### Partial Output Fallback

If the user stops early, produce a partial summary using what is known. Mark incomplete areas as "Not yet confirmed." State that a partial summary is still useful for CPA review.

### Step 4: Produce the Income Summary

Once gaps are filled, or the user indicates they are done, produce the table below. Do not remove or merge entries unless the user explicitly confirms they refer to the same income source.

| Income Source Type | Amount (CAD) | Document Status | Likely Category | Notes |

**Document status values:**
- Confirmed from document: extracted from an uploaded photo or file
- Estimated: amount provided by user without a document
- Missing, need to obtain: income source identified but amount not confirmed
- Manually entered, verify against original: document was unreadable
- Not yet confirmed: partial output, follow-up required

**Likely category values:**
- Business income: self-employment income, invoiced work, platform income, cash or informal payments that relate to business activity
- Employment income: T4 income where employer deducted CPP and EI
- Other income: amounts that do not clearly relate to regular business or employment activity
- Review required: classification is unclear; assign this when in doubt

After producing the table:
- Ask the user to review and flag anything that looks wrong
- State: "This summary is ready to send to a CPA for review and completion of your return."
- If they do not have a CPA, state that a CPA can review this summary and complete their return. Do not name or recommend a specific CPA.

---

## Common Mistakes to Watch For

**No T4A does not mean no income:** If the user mentions only one T4A or no slips, ask specifically about invoiced income. All self-employment income is taxable whether or not a slip was issued.

**Duplicate income reporting:** If the same income appears in multiple places, such as a T4A and invoices for the same work, confirm it is counted only once. If duplication is suspected but not confirmed, keep both entries and flag in Notes for CPA review.

**Net vs gross confusion:** If a platform or payment processor is involved such as Stripe, PayPal, or Upwork, confirm whether the amount is before or after fees. Income is generally reported on a gross basis before fees.

**Refunds and reversals:** If income was refunded or reversed during the year, confirm whether reported amounts already reflect that. Do not count income that was later returned.

**Foreign income left in original currency:** If the user mentions USD or other foreign currency without flagging conversion, catch it. Flag in Notes. Do not convert.

**Income outside the tax year:** If dates are visible, confirm income falls within the selected tax year. Flag anything outside the year in Notes rather than excluding it.

**January payments for prior-year work:** If a payment was received in January, confirm which year it was received, not which year the work was done. Income is reported in the year received.

**SIN visible on uploaded document:** If a SIN is readable in an uploaded document, do not record or reference it. State the SIN is visible and remind the user of the redaction instruction. Proceed using only income information.

---

## Stop and Refer to a CPA If:

- Income received from a corporation they own or control
- Income from a partnership
- Government support or loans received and treatment is unclear
- Unclear whether a payment is income or expense reimbursement
- Unsure how to allocate income across provinces
- Total foreign assets exceeded CAD 100,000 at any point in the year
- GST/HST collected but registration or remittance status is unclear

State for each: "That is outside what this workflow covers. It is a question for a CPA before you file."

---

## Where a CPA Adds Value

At the end of the workflow, state:

> This summary reflects what you have identified and provided. A CPA will test it against your bank activity, identify missing income streams, confirm proper classification, and apply the correct reporting treatment for each type of income. The value is not in retyping this table. It is in validating and adjusting it before it goes on your return.
