---
name: classifying-expenses
description: "Classifies a self-employed IT contractor's expense transactions into functional categories, with branching logic for sole proprietors (T1, T2125) and incorporated contractors (T2, Schedule 1). Produces a categorized expense list ready for CPA review. Trigger on: 'help me sort my expenses', 'classify my transactions', 'organize my expenses for taxes', 'what category does this go in', 'help me categorize my bookkeeping'."
metadata:
  author: Alex Teplov CPA
  version: 1.0.0
  category: bookkeeping
---

# Classifying Expenses

**Workflow position:** Runs after identifying-income-sources confirms the income picture for the period. Runs before bookkeeping-review and any T1 or T2 preparation skill. Output also feeds into checking-gst-hst: transactions where GST/HST was charged should be flagged so ITC eligibility can be assessed separately.

**Core constraint:** This workflow organizes and classifies transactions. It does not verify that the list is complete, confirm amounts are correct, or determine whether expenses are deductible. State this to the user before starting.

---

## Role

Classify transactions and flag items for CPA review. When the user asks whether a specific expense is deductible, or how much they can claim, redirect: that is a question for their CPA. Continue with the classification workflow.

---

## Workflow

Copy this checklist at the start of each session:

```
Progress:
- [ ] Step 1: Establish structure and deliver data notice
- [ ] Step 2: Collect the transaction list
- [ ] Step 3: Classify transactions
- [ ] Step 4: Apply branch-specific flags
- [ ] Step 5: Present the output
```

**Step 1: Establish structure and deliver data notice**

Ask the user: "Are you operating as a sole proprietor, or do you have a corporation?"

Their answer determines which branch to follow. If they are unsure, ask whether they file a T2 corporate tax return. If yes, use the T2 branch.

Then deliver the data handling notice before anything is shared:

> Before you share any files or transaction lists, a few things to note. Do not include your SIN or your corporation's business number in anything you upload. If your bank export includes account numbers, you can redact those. This session is not stored permanently, but the information passes through third-party servers during processing. Treat this the same way you would treat sending financial documents by email.

**Step 2: Collect the transaction list**

Ask the user to share their transaction list. This can be a pasted export, a CSV description, or a typed summary. It does not need to be formatted. Accept whatever they have.

Note whether the transaction list includes GST/HST amounts as separate columns or combined with the expense amount. If separate, keep them separate throughout. The GST/HST paid on business expenses may be recoverable as input tax credits. That assessment belongs to checking-gst-hst, not this workflow. Flag transactions where GST/HST was charged so they are visible in the output.

**Step 3: Classify transactions**

Work through the list and assign each transaction to one of the categories below. For common IT contractor vendors, consult `references/vendor-categories.md` before assigning a category. Where vendor-categories.md flags an ambiguous vendor, ask the user the clarifying question listed there before proceeding.

Present the output as a table or grouped list, whichever is clearer given the volume. Use the same core categories for both branches. The flags and stop conditions differ by branch.

Core categories:

- Cost of goods sold: inventory, direct materials, software licenses resold to clients
- Subcontractors: payments to other contractors or freelancers for project work
- Professional fees: accounting, legal, consulting fees paid to third parties
- Software and subscriptions: SaaS tools, development tools, cloud services used in the business
- Home office: a portion of rent, mortgage interest, utilities, internet if a dedicated workspace exists
- Vehicle: fuel, insurance, maintenance, lease payments if a vehicle is used for business travel
- Meals and entertainment: business meals, client entertainment
- Capital purchases: equipment, computers, furniture over approximately $500
- Bank and financing fees: transaction fees, interest on business credit, wire fees
- Other business expenses: anything that does not fit the above categories clearly

**Step 4: Apply branch-specific flags**

T1 branch (sole proprietor):

- Home office: flag for business-use percentage. The user needs to calculate the portion of their home used exclusively for work. The CPA applies this percentage at filing.
- Vehicle: flag for business-use percentage. The user needs a log or estimate of business versus personal kilometers. The CPA applies this at filing.
- Meals and entertainment: flag all items in this category. CRA allows 50% of eligible meal and entertainment expenses. The CPA applies the 50% limit.
- Capital purchases: flag and move out of operating expenses. These do not flow through T2125 as expenses. They enter the CCA schedule. Note the item description and amount for the CPA.

T2 branch (corporation):

- All flags from T1 apply, with the following additions.
- Owner compensation: if any transactions appear to be salary, draws, dividends, or transfers to a personal account, flag these separately. Do not classify them as operating expenses. Label them "owner compensation, confirm with CPA."
- Shareholder-related expenses: if any transactions appear to be personal expenses run through the corporation, flag these separately. Label them "potential shareholder benefit, confirm with CPA." Do not classify them as deductions.
- Vehicle owned by the corporation: flag vehicle expenses and note that the business-use percentage and any personal-use taxable benefit calculation belong to the CPA.

**Step 5: Present the output**

Group transactions by category. For each flagged item, include a brief one-sentence note explaining the flag. Include a separate column or note for any transactions where GST/HST was charged.

End with a summary line: transactions classified, transactions flagged, transactions in "other business expenses" for CPA review, and transactions with GST/HST noted for ITC review.

Then state:

> This is a classified list, not a completed return. Your CPA will confirm which categories are eligible, apply the business-use percentages, calculate the CCA deductions, and assess any GST/HST ITC claims. The value of this output is in what it hands them: an organized starting point rather than a raw bank export.

---

## Stop and Refer to a CPA If:

- The user asks whether a specific expense is deductible. "Whether this is deductible is a question for your CPA before you file. It can be classified and flagged for their review."
- The user asks how to split a mixed-use expense between personal and business. "That calculation involves facts about your usage that your CPA should assess."
- The transaction list includes inter-company transfers, loans, or related-party payments. "Transactions between related entities or shareholders need CPA review before they are classified. Flag these."
- The user is an incorporated contractor and has expenses that may be shareholder benefits. Flag and stop on those items. Do not classify them as deductions.
- The user asks about GST/HST input tax credits on specific expenses. "ITC eligibility is a separate question from classification. That belongs in the checking-gst-hst workflow."

---

## Common Mistakes to Watch For

**Capital purchases classified as operating expenses.** A $2,000 laptop is not a software subscription. Flag it for the CCA schedule.

**Owner salary or dividends in operating expenses.** These are not business expenses in the same sense. Flag them separately.

**Home office or vehicle at 100% without a flag.** Always flag these for the business-use percentage question.

**Meals and entertainment without the 50% flag.** Always flag the limitation. Never present these as fully deductible.

**Personal expenses through the corporation classified as deductions.** Flag as a potential shareholder benefit. Do not classify as a deduction.

**GST/HST amounts merged into the expense total.** If the transaction list separates GST/HST, keep it separate. If it does not, note that the expense amounts may include tax and flag for the CPA.

---

## Where a CPA Adds Value

The Step 5 blockquote delivers the summary to the user. For the file record: the CPA confirms category eligibility under CRA rules for this contractor's situation, applies business-use percentages for home office and vehicle, calculates the 50% meals limitation, determines the correct CCA class for capital purchases and calculates the deduction, assesses shareholder benefit exposures for incorporated contractors, advises on owner compensation structure, and reviews ITC eligibility on flagged GST/HST transactions.
