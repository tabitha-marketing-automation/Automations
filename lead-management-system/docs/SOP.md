# SOP: Lead scoring and routing

**Owner:** marketing operations. **Last updated:** 31 Oct 2026.

## Purpose
Score every new HubSpot contact, set its lifecycle stage, tag it in Mailchimp and alert sales when a lead is sales-ready.

## Fields
| Field | Where it comes from | Allowed values |
| --- | --- | --- |
| First name, email, company, job title | HubSpot contact | free text |
| Company size | HubSpot `company_size` | 1-9, 10-49, 50+ |
| Interest | HubSpot `interest` | Automation, Analytics, Content |
| Lead score | Calculated by Make, saved to HubSpot `lead_score` | number |
| Lifecycle stage | Calculated by Make, saved to HubSpot | lead, marketingqualifiedlead, salesqualifiedlead |

## Scoring rules
Company size 50+ = +20, 10-49 = +10, 1-9 = 0. Seniority Senior or Manager = +20, Specialist = 0. Interest Automation = +15. Company email = +10, free email = -10.

## Stage thresholds
Under 30 = Lead. 30 to 59 = MQL. 60 or more = SQL.

## Alerts and who gets them
SQL leads trigger an email to the Make account owner with the contact details and the score breakdown. Lead and MQL contacts get Mailchimp tags only.

## Mailchimp tags
Every contact gets its interest tag (or `no-interest`) plus `stage-lead`, `stage-mql` (and `nurture`) or `stage-sql`.

## Weekly check
- Errors tab is empty, or every row has been looked at and marked fixed.
- Make run history shows no failed runs.
- Mailchimp shows no bounces from the last week.
- Spot-check 3 contacts in HubSpot: score and stage match the rules above.
- Operations used this month are below the free plan limit.

## Fixing an error
1. Open the Errors tab and read the email and what failed.
2. Fix the contact in HubSpot or Mailchimp (for example, correct a fake or mistyped email).
3. Mark the row `yes` in the "fixed?" column.

## Known limits
- The keyword `lead` also matches "Lead Generation Specialist", which scores as Manager.
- Only new contacts are scored. Changes to an existing contact are not re-scored.
- HubSpot may refuse to move a stage backwards.
- Mailchimp rejects fake-looking email addresses.
