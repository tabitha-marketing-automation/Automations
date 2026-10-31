# Weekly Lead Report

A free way to get a lead summary in your inbox every Monday, with no dashboard to open.

## Who it is for
Small SaaS teams that already collect scored leads in a Google Sheet (for example with the [Lead Management System](../lead-management-system/)) and want a regular pulse check.

## What it does
Every Monday at 08:00 it emails you:
- new leads in the last 7 days and total leads
- how many are Lead, MQL and SQL, and the SQL share
- the average lead score
- how many used a free email address and how many are interested in automation

## How it works
1. A **Report** tab in the Google Sheet calculates the numbers with formulas (COUNTIFS, AVERAGE) from the Leads tab.
2. One cell on that tab builds the email text.
3. A Make scenario (Google Sheets, then Email) runs weekly, reads that cell and sends it.

## Cost and limits
Free. The scenario uses 2 operations per week on Make Free. Dates in the Leads tab must be real dates.

## Status
Run once on test data and the run succeeded. Not yet used for a live team.

## Build your own copy
1. In your Lead sheet, add a tab called `Report` and put the formulas in `report-tab-formulas.md` in column B (rows 3-11), and the summary formula in B13.
2. In Make, create a scenario: Google Sheets "Get a Cell" (Report, B13), then Email "Send an Email" with the cell value as HTML.
3. Schedule it weekly (Monday 08:00) and turn it on.
