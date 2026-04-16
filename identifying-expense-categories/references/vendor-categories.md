# Vendor Categories Reference

Use this file with `identifying-expense-categories`.

The purpose of this reference is to help group common expense vendors into practical working categories before downstream field review begins.

This file is for **initial categorization only**. It does not determine final deductibility, final T2125 treatment, GST/HST treatment, or filing position.

If a vendor clearly matches a category below, use the category as a strong working assumption.  
If the transaction description conflicts with the usual vendor pattern, prefer the transaction description and the user’s explanation over the vendor name alone.

---

## How to Use This Reference

For each transaction:

1. Check whether the vendor appears in this reference.
2. Apply the listed `working_category` as a starting point.
3. Apply the listed `review_note` if relevant.
4. If the vendor is known but the transaction is unusual, keep the category provisional.
5. If the vendor is not listed, classify by transaction description and user explanation.

Do not use this file to:
- finalize deductibility
- decide capital vs current treatment without review
- determine business vs personal use without support
- determine GST/HST treatment

---

## Working Categories

Use only these working categories in early expense review unless a later repository standard expands them:

- `software_and_cloud`
- `office_and_admin`
- `internet_and_phone`
- `meals_and_entertainment`
- `travel`
- `professional_fees`
- `subcontractors_and_outside_services`
- `workspace_and_rent`
- `home_office_related`
- `vehicle_related`
- `possible_capital_item`
- `other_or_unclear`

---

## Vendor Mapping Table

| Vendor | Working Category | Review Note |
|---|---|---|
| Amazon Web Services | software_and_cloud | Usually recurring cloud hosting or infrastructure cost. Keep routine unless the description suggests hardware or resale items. |
| AWS | software_and_cloud | Same treatment as Amazon Web Services. |
| Microsoft Azure | software_and_cloud | Usually cloud hosting, compute, storage, or software services. |
| Google Cloud | software_and_cloud | Usually cloud hosting or platform services. |
| DigitalOcean | software_and_cloud | Usually routine cloud infrastructure or hosting. |
| Heroku | software_and_cloud | Usually routine hosting or platform service. |
| Vercel | software_and_cloud | Usually hosting or deployment service. |
| Netlify | software_and_cloud | Usually hosting or deployment service. |
| GitHub | software_and_cloud | Usually software subscription or developer tooling. |
| GitLab | software_and_cloud | Usually software subscription or developer tooling. |
| Atlassian | software_and_cloud | Usually software subscription. Review whether charge is Jira, Confluence, or another business tool. |
| Jira | software_and_cloud | Usually project management software. |
| Confluence | software_and_cloud | Usually software subscription. |
| Notion | software_and_cloud | Usually software subscription. |
| Slack | software_and_cloud | Usually software subscription. |
| Zoom | software_and_cloud | Usually software subscription. |
| Figma | software_and_cloud | Usually software subscription. |
| Adobe | software_and_cloud | Usually software subscription. Review if the user also uses it partly personally. |
| QuickBooks | software_and_cloud | Usually bookkeeping software. |
| Xero | software_and_cloud | Usually bookkeeping software. |
| FreshBooks | software_and_cloud | Usually bookkeeping or invoicing software. |
| Dropbox | software_and_cloud | Usually software subscription or cloud storage. |
| Google Workspace | software_and_cloud | Usually software subscription or business email/service bundle. |
| Microsoft 365 | software_and_cloud | Usually software subscription or business productivity suite. |
| OpenAI | software_and_cloud | Usually software or AI tool subscription. Review whether any personal use may be mixed in. |
| Anthropic | software_and_cloud | Usually software or AI tool subscription. Review whether any personal use may be mixed in. |
| Cursor | software_and_cloud | Usually developer software subscription. |
| Replit | software_and_cloud | Usually developer software subscription. |
| Namecheap | software_and_cloud | Usually domain or hosting-related service. Review whether domain use is business-related. |
| GoDaddy | software_and_cloud | Usually hosting, domain, or web services. Review details if unclear. |
| Cloudflare | software_and_cloud | Usually web infrastructure or security service. |
| Shopify | software_and_cloud | Usually software or platform cost. For this repo, review whether it relates to side activity outside the IT contractor scope. |
| Apple App Store | software_and_cloud | Often software, but may be mixed-use. Review transaction description carefully. |
| Google Play | software_and_cloud | Often software, but may be mixed-use. Review transaction description carefully. |
| Staples | office_and_admin | Usually office supplies or small office purchases. Review for larger equipment items. |
| Bureau en Gros | office_and_admin | Usually office supplies or small office purchases. Review for larger equipment items. |
| Costco | office_and_admin | Mixed vendor. Do not rely on vendor name alone. Review item details carefully. |
| Amazon | other_or_unclear | Mixed vendor. Use transaction description before assigning category. |
| Walmart | other_or_unclear | Mixed vendor. Use transaction description before assigning category. |
| Best Buy | possible_capital_item | Often electronics or equipment. Review for laptop, monitor, phone, or accessory purchases. |
| Apple | possible_capital_item | Often hardware or software. Review whether the charge is device purchase, subscription, or mixed-use item. |
| Dell | possible_capital_item | Often computer or equipment purchase. |
| Lenovo | possible_capital_item | Often computer or equipment purchase. |
| HP | possible_capital_item | Often computer or equipment purchase. |
| Canon | possible_capital_item | Often equipment purchase. |
| Logitech | possible_capital_item | Often hardware or peripherals. May still be routine if low-value accessory. |
| IKEA | possible_capital_item | Often furniture or workspace items. Review whether the item is equipment or low-value office supply. |
| Rogers | internet_and_phone | Usually internet or phone service. Review for mixed personal and business use. |
| Bell | internet_and_phone | Usually internet or phone service. Review for mixed personal and business use. |
| Telus | internet_and_phone | Usually internet or phone service. Review for mixed personal and business use. |
| Fido | internet_and_phone | Usually phone service. Review for mixed personal and business use. |
| Freedom Mobile | internet_and_phone | Usually phone service. Review for mixed personal and business use. |
| Videotron | internet_and_phone | Usually internet or phone service. Review for mixed personal and business use. |
| Shaw | internet_and_phone | Usually internet or phone service. Review for mixed personal and business use. |
| Restaurant | meals_and_entertainment | Generic category for restaurant-type vendors. Review business purpose, attendees, and receipt support. |
| Starbucks | meals_and_entertainment | Often meal or meeting cost. May also be personal. Review carefully. |
| Tim Hortons | meals_and_entertainment | Often meal or meeting cost. May also be personal. Review carefully. |
| Second Cup | meals_and_entertainment | Often meal or meeting cost. May also be personal. Review carefully. |
| Cafe | meals_and_entertainment | Generic category. Review business purpose and receipt support. |
| Uber Eats | meals_and_entertainment | Usually meal cost. Review whether business purpose exists. |
| DoorDash | meals_and_entertainment | Usually meal cost. Review whether business purpose exists. |
| SkipTheDishes | meals_and_entertainment | Usually meal cost. Review whether business purpose exists. |
| Air Canada | travel | Usually business travel cost if linked to work purpose. Review personal component. |
| WestJet | travel | Usually business travel cost if linked to work purpose. Review personal component. |
| Porter | travel | Usually business travel cost if linked to work purpose. Review personal component. |
| Via Rail | travel | Usually travel cost if linked to work purpose. |
| Uber | travel | May be business travel or personal transport. Review context carefully. |
| Lyft | travel | May be business travel or personal transport. Review context carefully. |
| Airbnb | travel | May be travel accommodation or personal. Review business purpose. |
| Marriott | travel | Usually accommodation if linked to business travel. |
| Hilton | travel | Usually accommodation if linked to business travel. |
| Expedia | travel | May include flights, hotels, or mixed travel bookings. Review item details. |
| WeWork | workspace_and_rent | Usually coworking or temporary workspace cost. |
| Regus | workspace_and_rent | Usually coworking or temporary workspace cost. |
| Spaces | workspace_and_rent | Usually coworking or temporary workspace cost. |
| CPA Firm | professional_fees | Usually accounting or tax preparation fee. |
| Accountant | professional_fees | Usually accounting or tax preparation fee. |
| Lawyer | professional_fees | Usually legal fee. Review whether clearly business-related. |
| LegalZoom | professional_fees | Usually legal or entity-related support. Review relevance to the business. |
| H&R Block | professional_fees | Often tax preparation fee. Review whether it relates to the business or personal return. |
| Upwork | subcontractors_and_outside_services | Often payments to contractors or freelance services. Review whether this is expense-side use or income-side use. |
| Fiverr | subcontractors_and_outside_services | Often payments for outside services. |
| Freelancer | subcontractors_and_outside_services | Often payments for outside services. |
| Toptal | subcontractors_and_outside_services | Often payments for outside services. |
| Deel | subcontractors_and_outside_services | Often payments to contractors, but context may also relate to income. Review direction of payment. |
| Wise | other_or_unclear | Payment platform only. Do not assign category from vendor name alone. Review source and direction of payment. |
| PayPal | other_or_unclear | Payment platform only. Do not assign category from vendor name alone. |
| Stripe | other_or_unclear | Payment platform only. Do not assign category from vendor name alone. |
| Square | other_or_unclear | Payment platform only. Do not assign category from vendor name alone. |
| RBC | other_or_unclear | Financial institution. Review whether the item is bank fee, loan interest, transfer, or personal. |
| TD | other_or_unclear | Financial institution. Review whether the item is bank fee, loan interest, transfer, or personal. |
| Scotiabank | other_or_unclear | Financial institution. Review whether the item is bank fee, loan interest, transfer, or personal. |
| BMO | other_or_unclear | Financial institution. Review whether the item is bank fee, loan interest, transfer, or personal. |
| Desjardins | other_or_unclear | Financial institution. Review whether the item is bank fee, loan interest, transfer, or personal. |
| Shell | vehicle_related | Usually fuel or vehicle-related cost. Review whether vehicle claims are in scope and supported. |
| Esso | vehicle_related | Usually fuel or vehicle-related cost. Review whether vehicle claims are in scope and supported. |
| Petro-Canada | vehicle_related | Usually fuel or vehicle-related cost. Review whether vehicle claims are in scope and supported. |
| Canadian Tire Gas | vehicle_related | Usually fuel or vehicle-related cost. Review whether vehicle claims are in scope and supported. |
| Canadian Tire | other_or_unclear | Mixed vendor. Review whether charge is fuel, supplies, tools, or personal purchase. |

---

## Review Rules by Category

### software_and_cloud
Use for recurring software, hosting, subscriptions, cloud tools, and business service platforms.

Common risk areas:
- mixed personal and business use
- annual prepaid subscriptions
- software bundled with hardware purchase
- side-business or non-IT-contractor use

### office_and_admin
Use for routine office supplies and low-risk office purchases.

Common risk areas:
- vendor sells equipment as well as supplies
- large one-time purchases may be capital-like

### internet_and_phone
Use for internet and phone-related service providers.

Common risk areas:
- mixed personal and business use
- home office overlap
- multiple lines or family plans

### meals_and_entertainment
Use for restaurants, cafes, food delivery, and entertainment-type charges if business purpose is plausible.

Common risk areas:
- missing business purpose
- no attendee information
- personal component
- weak receipt support

### travel
Use for flights, trains, accommodation, and travel-related transport when linked to business purpose.

Common risk areas:
- personal travel mixed with business travel
- weak link to business purpose
- meals embedded inside travel booking

### professional_fees
Use for accounting, legal, and similar professional services.

Common risk areas:
- charge may relate to personal rather than business matters
- business relevance unclear

### subcontractors_and_outside_services
Use for payments to freelancers, agencies, or outside providers.

Common risk areas:
- vendor may also be an income platform
- business purpose unclear
- mixed contractor and software charges

### workspace_and_rent
Use for coworking, temporary office rental, or workspace fees.

Common risk areas:
- overlap with home office
- mixed business and personal use unlikely but still possible

### home_office_related
Use when the description clearly relates to home office support rather than general rent or internet alone.

Common risk areas:
- percentage allocation required
- incomplete cost detail
- overlap with internet and utilities

### vehicle_related
Use for fuel, parking, insurance, repairs, and similar vehicle costs when vehicle use is in scope.

Common risk areas:
- personal and business use mixed
- no logbook or mileage support
- gas station charges may include non-fuel items

### possible_capital_item
Use when the charge appears to involve equipment, furniture, hardware, or a larger one-time purchase.

Common risk areas:
- current vs capital treatment unclear
- partial personal use
- accessory vs equipment distinction

### other_or_unclear
Use only when the vendor alone is not enough to categorize confidently.

Common risk areas:
- payment platform only
- mixed retail vendor
- bank transfer or financial institution charge with unclear purpose
- unclear transaction description

---

## Default Rule for Unknown Vendors

If the vendor is not listed:

1. classify using the transaction description and user explanation
2. assign the best working category available
3. preserve uncertainty where needed
4. use `other_or_unclear` only when no practical category is supportable

Do not overuse `other_or_unclear`.

---

## Important Boundaries

This reference helps with early categorization only.

Do not use it to:

- determine final deductibility
- determine final T2125 line placement in all cases
- determine GST/HST treatment
- determine capital cost allowance treatment on its own
- determine whether a mixed-use item is fully business
- conclude that a charge is personal only from vendor name

When a category remains materially unclear, flag it for later review.