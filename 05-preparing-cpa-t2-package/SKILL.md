---
name: preparing-cpa-t2-package
description: "Assembles a corporate tax handoff package for an incorporated Canadian business owner to hand off to a CPA before T2 filing. Guides the user through collecting bookkeeping status, owner compensation records, GST/HST standing, prior year context, and supporting corporate documents, then produces a cover summary the CPA can act on directly. Does not give tax advice, prepare financial statements, or advise on compensation structure. Trigger on: 'prepare for my corporate tax filing', 'what does my accountant need for my T2', 'get my company documents ready for my CPA', 'organize my corporate books before filing', 'what should I send my accountant for the corporation', 'I have a meeting with my CPA about the corporate return'."
metadata:
  author: Alex Teplov
  version: 1.0.0
  category: tax-preparation
---

# Preparing CPA T2 Package

**Workflow position:** Stands alone in the incorporated owner-manager sequence within selfemployed-skills. Complements `04-preparing-cpa-t1-package`, which covers the owner's personal T1 return. Run both skills when the owner files a T2 and a T1 in the same CPA engagement. The two cover summaries together help the CPA understand the personal and corporate sides of the owner-manager file.

**Core constraint:** This workflow organizes information the user provides. It does not guarantee completeness and may not detect items the user has omitted or described inaccurately. It does not verify bookkeeping accuracy or prepare financial statements. State this to the user before starting.

---

## Role

Do not give tax advice. When the user asks about deductibility, compensation structure, dividend versus salary decisions, or what they should claim, redirect the advisory part and continue the workflow. The goal is a well-organized package, not a filing position.

## Workflow

Copy this checklist at the start of each session:

```
Progress:
- [ ] Step 1: Open conversation and deliver data notice
- [ ] Step 2: Collect corporate profile
- [ ] Step 3: Collect bookkeeping and financial statement status
- [ ] Step 4: Collect owner compensation details
- [ ] Step 5: Confirm GST/HST status
- [ ] Step 6: Collect prior year context
- [ ] Step 7: Collect other corporate items
- [ ] Step 8: Identify gaps and flag questions
- [ ] Step 9: Produce cover summary
```

### Step 1: Open the Conversation

State before asking any questions:

1. This workflow assembles a CPA-ready T2 package from the corporation's financial information.
2. "This process organizes what you provide and prompts for common items, but it may still miss information you have omitted or described inaccurately."
3. Deliver the data handling notice below.
4. Ask what the corporation's fiscal year-end date is. This frames everything that follows. If they do not know, ask them to check their prior year T2 return or CRA My Business Account.
5. Ask which fiscal year the package is for.

**Data handling notice. State before collecting any information:**

> Do not type your corporation's business number, SIN, or any client or supplier names into this conversation. Amounts, document types, and general descriptions are all that are needed. If uploading financial documents, remove or cover any business numbers or SINs before uploading. Avoid sharing sensitive business or legal information you would not be comfortable storing in a third-party system. Your inputs and uploaded documents may be stored by this AI tool according to its policies. Review those policies before proceeding if you have concerns.

---

### Step 2: Collect Corporate Profile

Collect before moving to financial detail. This information helps the CPA scope the engagement and review the file correctly.

Ask one question at a time:

- What province is the corporation incorporated in, and what province does it primarily operate in? Note both for the CPA.
- Is this a Canadian-controlled private corporation (CCPC)? If unsure, flag for CPA and continue.
- Is the corporation actively carrying on business, or is it primarily holding assets such as investments or real estate? Note the answer for the CPA and flag if unclear.
- How many shareholders does the corporation have, and are any shareholders other than the owner?

---

### Step 3: Collect Bookkeeping and Financial Statement Status

The T2 requires financial statements. The CPA needs to know what the bookkeeping looks like before scoping the engagement.

Ask one question at a time:

- What bookkeeping software or method does the corporation use? Common options: QuickBooks Online, QuickBooks Desktop, Xero, Wave, spreadsheet, or no formal system.
- Is the bookkeeping current to the fiscal year-end date, or are there entries still to be made?
- Are the bank accounts reconciled to the fiscal year-end date?
- Are the credit card statements reconciled?
- Are there outstanding invoices (accounts receivable) or unpaid bills (accounts payable) the bookkeeping may not reflect?
- Does the corporation own any depreciable assets: equipment, vehicles, computers, leasehold improvements? If yes, ask whether a CCA schedule is in the bookkeeping records, and whether any assets were purchased or disposed of during the year.
- Are the financial statements already prepared, or does the CPA need to prepare them from the bookkeeping records?

If financial statements are already prepared, ask who prepared them and whether they are draft or final.

Ask one question at a time for year-end support documents:

- Are year-end bank statements available for all accounts?
- Are year-end credit card statements available?
- Are loan or financing statements available?
- Is a payroll summary available if salary was paid?
- Are GST/HST filing summaries available for the year?
- Are purchase documents available for major assets acquired during the year?

Did the corporation hold any inventory at fiscal year-end? If yes, ask whether count sheets or valuation records are available.

---

### Step 4: Collect Owner Compensation Details

Owner compensation is one of the most common areas requiring CPA attention before a T2 is filed.

Ask one question at a time:

- Did the owner receive a salary from the corporation during the fiscal year? If yes, confirm total salary paid and whether T4 slips were issued and filed with CRA.
- Were any dividends declared by the corporation during the fiscal year? If yes, confirm the total amount declared.
- Were those dividends paid during the fiscal year, or are any amounts still outstanding?
- Were board resolutions or minute book entries prepared for those dividends?
- Were T5 slips issued and filed with CRA for dividends paid?
- Did the owner receive any other payments from the corporation: management fees, rent for use of personal property, loan repayments?
- Does the owner have a shareholder loan account with the corporation? A shareholder loan exists if money was borrowed from the corporation or if the owner advanced money to the corporation. If yes, ask for the balance at fiscal year-end: does the corporation owe money to the owner, or does the owner owe money to the corporation?

If the owner owes money to the corporation at fiscal year-end, flag for CPA immediately. Do not assess the tax treatment or repayment timeline in this workflow. "That is outside what this workflow covers. It is a question for a CPA before you file."

---

### Step 5: Confirm GST/HST Status

Ask one question at a time:

- Is the corporation registered for GST/HST?
- What is the reporting period: annual, quarterly, or monthly?
- Are all GST/HST returns filed and remittances current to the fiscal year-end date?
- Were there any outstanding balances, penalties, or CRA correspondence related to GST/HST during the year?

If there are filing gaps or unremitted amounts, flag for CPA. Do not advise on what to file.

---

### Step 6: Collect Prior Year Context

Ask one question at a time:

- Does the owner have the prior year corporate T2 return? If yes, confirm it is available to provide to the CPA. If not, note as missing.
- Does the owner have the prior year corporate Notice of Assessment from CRA? Note whether it is on hand.
- Were there any losses carried forward from prior years, either non-capital losses or net capital losses? If yes, note the amount and year if known, and flag for CPA.
- Did the corporation make any tax instalment payments to CRA during the fiscal year? CRA My Business Account shows instalment history. Confirm total if applicable.
- Were there any CRA audit notices, proposal letters, or reassessments for prior years that are still open or unresolved?

---

### Step 7: Collect Other Corporate Items

Ask one question at a time. Skip any the user confirms do not apply.

- Were there any significant transactions during the year: sale of assets, purchase of a business, sale of shares, amalgamation, wind-up activity?
- Were there any share issuances, share redemptions, changes in ownership percentages, or director changes during the year? If yes, flag for CPA. Corporate records may need to be updated.
- Did the corporation have any related corporations, associated corporations, or affiliated entities? If yes, flag for CPA.
- Does the corporation have any foreign income, foreign subsidiaries, or transactions with non-residents?
- Were there any intercompany loans or transactions with related parties, including the owner's other corporations or family members?
- Is the corporate minute book current? The minute book should reflect any dividends declared, director resolutions, and share transactions during the year. If it is not current, flag for CPA.

---

### Step 8: Identify Gaps and Flag Questions

Before producing the summary, review collected information and identify:

**Missing items:** List anything noted as missing or not confirmed: prior year T2, prior year corporate NOA, T4 or T5 slips not yet filed, bookkeeping not current, CCA schedule missing, minute book not current.

**Flagged items:** List anything requiring CPA attention before filing. State each as: "Item: [description]. Flag reason: [what is unclear or requires professional judgment]."

Ask the user to confirm the gap and flag list before producing the cover summary.

---

### Step 9: Produce Cover Summary

Produce a structured summary the user can send to their CPA. Format as a plain document, not a table. Use the structure below.

---

**CPA Package Cover Summary**
Corporation: [name if provided, otherwise "corporation"]
Fiscal year-end: [date]
Prepared: [today's date]

**Corporate Profile**
Province of incorporation: [province]
Province of operation: [province]
CCPC status: [confirmed / not confirmed, flag if unclear]
Nature of business: [active / holding / unclear]
Number of shareholders: [number]

**Bookkeeping and Financial Statements**
Bookkeeping software: [name]
Books current to fiscal year-end: [yes / no / partially]
Bank accounts reconciled: [yes / no / partially]
Credit cards reconciled: [yes / no / partially]
Outstanding AR or AP not in books: [yes, described / no]
Depreciable assets: [yes, list asset types / no]
CCA schedule: [current / missing / not applicable]
Financial statements: [prepared by [who], draft or final / not yet prepared]

**Owner Compensation**
Salary paid: $[amount] / [none]
T4 filed: [yes / no / not applicable]
Dividends declared: $[amount] / [none]
Dividends paid: $[amount] / [none] / [unclear]
Dividend resolutions recorded: [yes / no / unclear]
T5 filed: [yes / no / not applicable]
Other payments: [describe or none]
Shareholder loan balance at year-end: [corporation owes owner $[amount] / owner owes corporation $[amount] / nil / unclear, flag]

**GST/HST**
Registered: [yes / no]
Reporting period: [annual / quarterly / monthly]
Returns filed to year-end: [yes / no / gap, flag]
Outstanding balances or CRA correspondence: [yes, flag / no]

**Prior Year**
Prior year T2 return: [on hand / missing]
Prior year corporate NOA: [on hand / missing]
Loss carryforwards: [amounts and years / none / unclear, flag]
Instalments paid this year: $[amount] / [none]
Open CRA audit or reassessment: [yes, flag / no]

**Ownership and Structural Changes**
Share issuances, redemptions, or ownership changes: [describe or none]
Director changes: [describe or none]
Significant transactions: [describe or none]

**Related and Foreign Matters**
Associated or related corporations: [yes, flag / no]
Foreign income or non-resident transactions: [yes, flag / no]
Intercompany transactions: [describe or none]

**Corporate Records**
Minute book current: [yes / no, flag]
Year-end support documents available: [yes / no / partial, describe gaps]
Inventory at year-end: [yes, valuation records available / yes, no valuation records / no]

**Missing Items**
[List each missing item, one per line]

**Questions for CPA**
[List each flagged item and flag reason, one per line]

---

If the owner does not have a CPA, state that a CPA can use this summary to scope the corporate engagement. Do not recommend a specific CPA.

Ask whether the owner also needs to file a personal T1 return. If yes, ask whether they have prepared or started `04-preparing-cpa-t1-package`. If not, note in the cover summary that a personal T1 package may also be needed before the CPA meeting.

---

## Common Mistakes to Watch For

**Fiscal year-end assumed to be December 31:** Many small business owners assume their corporate year-end matches the calendar year. Confirm the actual fiscal year-end in Step 1 before collecting any other information. An incorrect year-end produces an incorrect package.

**T4 and T5 slips not filed:** If salary was paid, ask whether T4 slips were prepared and filed. If dividends were declared or paid, ask whether the relevant slips were prepared and filed. If either is missing, flag for the CPA. These are late-filing items, not items to omit from the package.

**Shareholder loan not tracked:** If the owner draws money from the corporation without a formal dividend or salary record, those draws may sit in the shareholder loan account. A year-end debit balance in the shareholder loan (owner owes the corporation) is a flag item. Refer to CPA without advising on treatment.

**Bookkeeping treated as complete when it is not:** If the owner says the books are "mostly done," ask specifically about the last month of the fiscal year and any entries made after year-end. Unrecorded items at year-end affect the financial statements and the T2 calculations.

**Associated corporations not disclosed:** An owner who has two or more corporations may not think to mention related entities. Ask specifically. The shared small business deduction limit is a CPA-level issue that affects both T2 returns.

**Minute book treated as optional:** Dividends without board resolutions can create legal and tax issues. If dividends were paid and the minute book is not current, flag it. Do not treat it as administrative backlog.

---

## Stop and Refer to a CPA If:

- The shareholder loan shows the owner owes money to the corporation at fiscal year-end. "That is outside what this workflow covers. It is a question for a CPA before you file."
- The corporation has associated corporations that may share the small business deduction limit. "That is outside what this workflow covers. It is a question for a CPA before you file."
- The corporation has foreign income, a foreign subsidiary, or transactions with non-residents. "That is outside what this workflow covers. It is a question for a CPA before you file."
- There was a sale of shares, purchase of a business, amalgamation, wind-up, significant ownership change, or other major structural transaction during the year. "That is outside what this workflow covers. It is a question for a CPA before you file."
- There is an open CRA audit, proposal letter, or unresolved reassessment. "That is outside what this workflow covers. It is a question for a CPA before you file."
- The corporation's CCPC status is unclear. "That is outside what this workflow covers. It is a question for a CPA before you file."

---

## Where a CPA Adds Value

At the end of the workflow, state:

> This package organizes what you have gathered. A CPA will review the bookkeeping for accuracy, prepare or review the financial statements, calculate the correct CCA claims, apply the small business deduction, assess owner compensation treatment in the context of the corporate and personal filings, and file the return. The value is not in having organized documents. It is in the technical work the CPA does with them once they have them.
