# Test results

Run on 31 Oct 2026 with dummy contacts. Expected values come from the `Test leads` tab of the workbook.

| # | Test lead | Expected | Result in HubSpot and Sheet | Pass |
| --- | --- | --- | --- | --- |
| 1 | Director of Marketing, 50+, Automation, company email | 65 SQL | 65 SQL | Yes |
| 2 | Marketing Manager, 50+, Automation, company email | 65 SQL | 65 SQL | Yes |
| 3 | Growth Manager, 10-49, Analytics, company email | 40 MQL | 40 MQL | Yes |
| 4 | Marketing Specialist, 10-49, Automation, company email | 35 MQL | 35 MQL | Yes |
| 5 | Student, 1-9, Content, gmail | -10 Lead | -10 Lead | Yes |
| 6 | Specialist, 1-9, Analytics, outlook | -10 Lead | -10 Lead | Yes |
| 7 | Duplicate of #1 | rejected | HubSpot: "Entry must be unique" | Yes |
| 8 | Blank job title, 10-49, Content, company email | 20 Lead | 20 Lead | Yes |

Also checked:
- The lifecycle stage in HubSpot matched the stage in the Sheet.
- SQL leads sent an email alert with the score breakdown.
- Leads with real-looking addresses were added to Mailchimp with their interest tag and `stage-lead`.

## What broke and how I fixed it
1. **`or()` does not exist in Make.** The seniority formula failed. I used the `|` operator instead.
2. **Blank interest.** A contact with no interest gave Mailchimp a blank tag name and an error. I added `ifempty(interest; "no-interest")`.
3. **Fake emails.** Mailchimp rejects example.com addresses and stopped the whole run. I added error handlers that log the lead to the Errors tab and continue.
4. **Repeated rows.** Failed runs re-processed the same contacts and wrote duplicate rows in the Sheet. I cleaned the rows by hand and added the error handlers so a failed step no longer aborts the run.
