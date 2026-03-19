# Vendor classification reference

For use with the classifying-expenses skill. When a transaction vendor matches an entry below, apply the listed category and flag note. Where the GST/HST column indicates "likely yes," flag the transaction for ITC review as instructed in Step 2. Where classification depends on context, ask one clarifying question before assigning.

---

## Cloud infrastructure and hosting

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Amazon Web Services (AWS) | Software and subscriptions | No (US supplier, not registered) | If resold to client, may be cost of goods sold. Confirm with user. |
| Google Cloud Platform (GCP) | Software and subscriptions | No (US supplier, not registered) | Same as AWS. |
| Microsoft Azure | Software and subscriptions | Yes | |
| DigitalOcean | Software and subscriptions | No (US supplier) | |
| Cloudflare | Software and subscriptions | No (US supplier) | |
| Hetzner | Software and subscriptions | No (EU supplier) | |
| Vercel | Software and subscriptions | No (US supplier) | |
| Netlify | Software and subscriptions | No (US supplier) | |
| Heroku | Software and subscriptions | No (US supplier) | |
| Linode / Akamai | Software and subscriptions | No (US supplier) | |

---

## Development tools and services

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| GitHub | Software and subscriptions | No (US supplier) | |
| GitLab | Software and subscriptions | No (US supplier) | |
| JetBrains | Software and subscriptions | No (EU supplier) | Annual license. If over $500, flag for CCA review. |
| Atlassian (Jira, Confluence) | Software and subscriptions | No (AU supplier) | |
| Linear | Software and subscriptions | No (US supplier) | |
| Postman | Software and subscriptions | No (US supplier) | |
| Docker | Software and subscriptions | No (US supplier) | |
| CircleCI | Software and subscriptions | No (US supplier) | |
| Sentry | Software and subscriptions | No (US supplier) | |
| Datadog | Software and subscriptions | No (US supplier) | |
| PagerDuty | Software and subscriptions | No (US supplier) | |
| Terraform / HashiCorp | Software and subscriptions | No (US supplier) | |
| Anthropic / OpenAI / Cohere | Software and subscriptions | No (US suppliers) | If API usage is resold or embedded in client deliverables, may be cost of goods sold. Confirm with user. |

---

## Productivity and communication

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Notion | Software and subscriptions | No (US supplier) | |
| Slack | Software and subscriptions | No (US supplier) | |
| Zoom | Software and subscriptions | No (US supplier) | |
| Microsoft 365 / Office | Software and subscriptions | Yes | |
| Google Workspace | Software and subscriptions | No (US supplier) | |
| Loom | Software and subscriptions | No (US supplier) | |
| Calendly | Software and subscriptions | No (US supplier) | |
| 1Password | Software and subscriptions | Yes (Canadian company) | |
| Dropbox | Software and subscriptions | No (US supplier) | |

---

## Hardware and equipment

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Apple Store | Capital purchase or software and subscriptions | Yes | Hardware (MacBook, iPad, monitor) over $500: flag for CCA. Apps and iCloud: software and subscriptions. Confirm which with user. |
| Best Buy | Capital purchase | Yes | Flag for CCA if over $500. |
| Canada Computers | Capital purchase | Yes | Flag for CCA if over $500. |
| Dell | Capital purchase | Yes | Flag for CCA if over $500. |
| Lenovo | Capital purchase | Yes | Flag for CCA if over $500. |
| Amazon (hardware) | Capital purchase or other | Yes (if Canadian seller) | Amount and description determine category. Confirm with user. |
| Staples | Other business expenses or capital purchase | Yes | Small supplies: other. Furniture or equipment over $500: flag for CCA. |
| IKEA | Capital purchase | Yes | Desk, chair, shelving for home office: flag for CCA and note home office context. |

---

## Professional services and finance

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Stripe | Bank and financing fees | No (US supplier) | Payment processing fees only. If Stripe charge is for a subscription product, classify by the product. |
| PayPal | Bank and financing fees | No (US supplier) | Same as Stripe. |
| Wave | Software and subscriptions | Yes (Canadian company) | |
| QuickBooks / Intuit | Software and subscriptions | Yes | |
| FreshBooks | Software and subscriptions | Yes (Canadian company) | |
| Xero | Software and subscriptions | No (NZ supplier) | |
| Wise / TransferWise | Bank and financing fees | No (UK supplier) | Transfer fees only. |
| Shopify | Software and subscriptions or cost of goods sold | Yes (Canadian company) | Monthly platform fee: software and subscriptions. Transaction fees on product sales may relate to cost of goods sold. Confirm with user. |

---

## Learning and professional development

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Udemy | Other business expenses | No (US supplier) | Professional development. Confirm business relevance with user. |
| Coursera | Other business expenses | No (US supplier) | Same as Udemy. |
| LinkedIn Learning | Other business expenses | No (US supplier) | Same as Udemy. |
| O'Reilly / Safari Books | Software and subscriptions | No (US supplier) | Technical reference subscription. |
| Pluralsight | Software and subscriptions | No (US supplier) | |
| A Cloud Guru | Software and subscriptions | No (US supplier) | |

---

## Meals, travel, and entertainment

| Vendor | Default category | GST/HST | Flag or note |
|--------|-----------------|---------|--------------|
| Restaurants (any) | Meals and entertainment | Yes | Flag 50% limitation. Confirm business purpose with user. |
| Uber Eats / DoorDash / SkipTheDishes | Meals and entertainment or personal | Yes | Delivery during work: meals and entertainment, flag 50%. Personal meal: do not classify as business. Confirm with user. |
| Uber / Lyft | Vehicle or meals and entertainment | Yes | Business travel: vehicle. Client entertainment involving transportation: meals and entertainment. Confirm with user. |
| Air Canada / WestJet / other airlines | Other business expenses | Yes (domestic) / No (international) | Business travel only. Confirm trip purpose with user. |
| Hotels / Airbnb | Other business expenses | Yes | Business travel only. Confirm trip purpose with user. |
| Tim Hortons / Starbucks / coffee shops | Meals and entertainment | Yes | Flag 50% limitation. Solo working coffee is borderline: flag for CPA. |

---

## Ambiguous or high-risk vendors

These vendors appear frequently and are misclassified often. Always ask one clarifying question before assigning a category.

| Vendor | Risk | Clarifying question |
|--------|------|-----------------|
| Amazon (general) | Could be anything | What was purchased? |
| Apple (general) | Hardware vs software vs personal | Was this hardware, a software subscription, or a personal purchase? |
| Costco / Walmart / wholesale clubs | Usually personal | What was purchased and was it exclusively for the business? |
| Facebook / Meta Ads | Other business expenses | Was this paid advertising for a business purpose? |
| Google Ads | Other business expenses | Same as Meta Ads. |
| Canada Post / UPS / FedEx | Other business expenses | Was this shipping for a business purpose? |
| Insurance (general) | Depends on type | Was this business liability, vehicle insurance, or home insurance? Each goes to a different category. |

---

## Category to form line mapping

Use this table to orient the CPA when handing off the classified output. Category names in the skill are functional, not form-line labels. This mapping shows where each category lands on T2125 (T1 sole proprietor) and on a corporate income statement feeding into T2 Schedule 1.

| Category | T2125 line (T1) | T2 treatment |
|----------|----------------|--------------|
| Cost of goods sold | 8300 (purchases) / 8320 (direct wages) | Cost of sales on income statement |
| Subcontractors | 8340 | Subcontracts on income statement |
| Professional fees | 8860 | Professional fees on income statement |
| Software and subscriptions | Other expenses, line 9270 (itemized) | Other expenses on income statement |
| Home office | 9220 (rent) / 9281 (business-use-of-home calc) | Reasonable allocation; personal portion not deductible |
| Vehicle | 9281 motor vehicle expenses | Motor vehicle expenses; personal-use taxable benefit applies for T2 |
| Meals and entertainment | 8523 (50% limitation applied by CPA) | Same; 50% limitation applies |
| Capital purchases | Not on T2125; enter CCA schedule (class determined by CPA) | Not expensed; capitalized and depreciated via CCA |
| Bank and financing fees | 8710 | Interest and bank charges on income statement |
| Other business expenses | 9270 (other expenses, itemized) | Other expenses on income statement; CPA reviews each item |

Notes for the CPA:

- Software and subscriptions has no dedicated T2125 line. Each item is listed individually under other expenses at line 9270. For high-volume contractors this section can be long.
- Capital purchases do not appear as expenses anywhere on T2125 or the corporate income statement. They enter the CCA schedule. The CPA determines the correct class: Class 10 (general equipment, 30%), Class 50 (computers, 55%), Class 12 (software, 100% in year of acquisition) are the most common for IT contractors.
- Home office on T2125 flows through the business-use-of-home calculation, which limits the deduction to business income and cannot create a loss. Carry-forward rules apply.
- Vehicle expenses for a T2 corporation require a standby charge and operating benefit calculation if the vehicle is owned by the corporation and available for personal use. This is separate from the business-use percentage applied on T1.
