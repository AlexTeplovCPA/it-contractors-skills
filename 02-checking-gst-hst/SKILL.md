---
name: checking-gst-hst
description: "Guides users through a structured review of their GST/HST obligations as a self-employed Canadian. Collects revenue figures, supply types, registration status, and filing history to produce an organized summary a CPA can act on. Does not advise on registration decisions, exempt supply classification, or Quick Method elections. Trigger on: 'do I need to charge HST', 'should I be registered for GST', 'check my GST situation', 'I think I missed a GST filing', 'help me figure out my HST', 'am I over the small supplier limit'."
metadata:
  author: Alex Teplov
  version: 1.0.0
  category: tax-compliance
---

# Checking GST/HST

**Workflow position:** Runs after `identifying-income-sources`. Output feeds into `preparing-cpa-review` if the user is preparing for a CPA meeting, or stands alone as a compliance check.

**Core constraint:** This workflow organizes GST/HST information. It does not verify accuracy or completeness, and does not determine whether supplies are taxable, zero-rated, or exempt. State this to the user before starting.

---

## Role

Collect and organize. Do not advise on whether the user should register, whether specific supplies qualify as exempt or zero-rated, or whether the Quick Method is appropriate for their situation. If those questions arise, acknowledge them, note them for the CPA section, and continue with the workflow.

---

## Workflow

Copy this checklist at the start of each session:

```
Progress:
- [ ] Step 1: Open conversation and deliver data notice
- [ ] Step 2: Collect taxable supply figures by quarter
- [ ] Step 3: Identify supply types
- [ ] Step 4: Check registration status
- [ ] Step 5: Identify filing gaps
- [ ] Step 6: Quick Method note
- [ ] Step 7: Produce the summary
```

### Step 1: Open the conversation

State before asking any questions:

1. This workflow builds a GST/HST summary the user can bring to a CPA.
2. "This process relies on what you provide. It will not catch everything on its own."
3. Deliver the data handling notice below.
4. Ask which tax year or period they are reviewing.

**Data handling notice. State before collecting any information:**

> Do not share your SIN or business number in full. If you pull CRA documents for reference, redact those fields first. Revenue figures and filing history are commercially sensitive. This conversation may be stored by the platform you are using. Do not paste raw CRA notices or account statements into the chat.

### Step 2: Collect taxable supply figures by quarter

Ask for taxable revenues before expenses, broken down by calendar quarter, for the last four consecutive calendar quarters and the current quarter to date. If the business is newer, collect whatever periods are available.

The threshold test is quarter-based. The small supplier threshold is $30,000 in worldwide taxable supplies (before expenses, including zero-rated supplies) in a single calendar quarter, or cumulatively across four consecutive calendar quarters.

Ask the user: "Do any of your revenues come from financial services, sales of capital property, or from an associated person or associated business?" If yes, note it. Those categories affect the threshold calculation in ways that require CPA input.

Do not calculate whether the threshold has been crossed. Collect the numbers and note them.

Note the registration timing question for the summary: CRA registration timing depends on how the threshold was crossed. If it is crossed in a single quarter, the timing differs from crossing it only on the four-consecutive-quarter test. Do not tell the user which path applies. Flag it for CPA review.

### Step 3: Identify supply types

Ask:
- What province or territory is the business located in?
- What type of work does the business do? (Ask for a plain-language description, not a category.)
- Does the business sell goods, services, or both?
- Are any services in these categories: health care or dental services, financial services, educational services, residential rent, or insurance?

Note the province as context. The rate that should have been charged on a given supply is determined by the place of supply, not only by the province where the business is located. For most service businesses operating in one province, these will be the same. Where the user serves clients in multiple provinces, flag it for CPA review.

HST provinces (Ontario, New Brunswick, Nova Scotia, PEI, Newfoundland) have a single combined rate. GST-only provinces use GST at 5% plus provincial sales tax handled separately. Quebec: Revenu Québec generally administers both GST/HST and QST for businesses located there. If the user is in Quebec, note this. For most Quebec businesses, account access, filing, and many GST/HST questions go through Revenu Québec, not CRA My Business Account, for both taxes. Flag for CPA review if any Quebec-specific questions arise.

The categories listed above may involve exempt or zero-rated supplies that change the obligation picture. Do not classify them. Legal services are generally taxable and should not be assumed exempt unless the user raises a specific question, in which case flag for CPA review. If the user identifies any of the categories above, flag for CPA review before proceeding with registration or filing assumptions.

Checklist for the user to work through:

- [ ] All revenue is from one type of supply (simpler case)
- [ ] Revenue includes a mix of supply types
- [ ] Any supplies may be exempt or zero-rated (flag for CPA)
- [ ] Unsure about supply type classification (flag for CPA)

### Step 4: Check registration status

Ask:
- Are you currently registered for GST/HST?
- If registered: what reporting period are you on: annual, quarterly, or monthly?
- If not registered: has the business ever been registered?

Do not ask for the full RT account number. The data handling notice at the start asks users not to share their business number in full. Instead, ask the user to confirm the last four digits of their RT account if they need to identify it, or simply confirm that they have one.

If registered, ask them to log into CRA My Business Account (or Revenu Québec My Account if in Quebec) and report back:
- Registration date
- Reporting period
- Any outstanding returns shown on the account
- Most recent filing date and period covered

Note everything reported. Do not verify against the revenue figures at this stage.

### Step 5: Identify filing gaps

If the user is registered, ask:
- What periods have been filed and what periods are outstanding?
- Are there any periods where they collected GST/HST but have not remitted?

Cross-reference the reporting period against the filing history to identify any gaps. State the gaps clearly: "Based on what you've told me, it looks like [period] may not have been filed. A CPA will need to confirm this before you take action."

Do not advise on penalties or how to resolve gaps. That is a CPA conversation.

### Step 6: Quick Method note

Ask: "Do you know if you've elected to use the Quick Method for GST/HST?"

If yes: note it. The Quick Method affects remittance calculations. If the user is unsure, flag it as a question for the CPA. Quick Method elections have specific eligibility rules and filing implications.

### Step 7: Produce the summary

Compile everything into a plain summary:

- Business province, place of supply note if multi-province, and supply type description
- Taxable revenues by quarter with threshold context (numbers only, no conclusion on whether threshold is crossed, flags for any excluded categories)
- Registration status, last four digits of RT number if provided, reporting period
- Filing history summary and any identified gaps
- Supply type flags requiring CPA review
- Quick Method status
- Taxi/ride-sharing flag if applicable

After producing the summary:
- Ask the user to review and flag anything that looks wrong
- State: "This summary is ready for your CPA to review. The items flagged above are the ones that need professional input before you file or register."

---

## Common Mistakes to Watch For

**Zero-rated and exempt are not the same:** Both result in no HST collected from clients, but zero-rated supplies still allow the seller to claim input tax credits (ITCs) on related expenses, while exempt supplies do not. Do not explain this distinction as advice. Note it as a reason those classifications need CPA confirmation.

**Undercounting revenues:** Users often report only deposits received, missing amounts that were paid or became due in the period by other means. Ask whether the figures include all amounts that were paid or became due in the period, not just deposits received.

**Net vs gross revenues:** Users sometimes report net revenue after platform fees or agent commissions. The threshold applies to gross taxable revenues, not net.

---

## Stop and Refer to a CPA If:

- The user believes they crossed the $30,000 threshold in a prior period and never registered. Late registration has back-filing and potential penalty implications. "That is outside what this workflow covers. It is a question for a CPA before you take any action."
- The user has collected HST from clients but has not filed or remitted for one or more periods. "That is outside what this workflow covers. It is a question for a CPA before you take any action."
- The user's supplies may include exempt categories such as health care, financial services, residential rent, or insurance. "Supply classification affects your entire obligation picture. That is a question for a CPA before you assume anything about registration or filing."
- The user is a taxi operator or commercial ride-sharing driver. These operators are required to register for GST/HST even if they are small suppliers. The small supplier exemption does not apply. "That is outside what this workflow covers. It is a question for a CPA before you assume your registration status."
- The user operates in Quebec and has questions about their filing or account. "Revenu Québec generally administers both GST/HST and QST for businesses in Quebec. That is outside what this workflow covers. It is a question for a CPA or a tax professional familiar with Quebec."
- The user wants to know whether the Quick Method is right for them. "That is an election with specific eligibility rules and remittance implications. It is a question for a CPA."

---

## Where a CPA Adds Value

At the end of the workflow, state:

> This summary reflects what you have identified and provided. A CPA will confirm whether specific supplies are taxable, zero-rated, or exempt, determine whether late registration is required, evaluate Quick Method eligibility, review ITC claims, and resolve any filing gaps. The value is not in collecting these numbers. It is in validating and acting on them before you file or register.
