# Nurture emails (as sent by the Make scenario)

The `Lead Nurture Emails` scenario creates and sends one Mailchimp campaign per email, each day, to the people whose signup date matches:

| Email | Sent to people who signed up | Subject |
| --- | --- | --- |
| 1 Welcome | today | Welcome: how this lead scoring setup works |
| 2 Tip | 2 days ago | How scoring decides who to call first |
| 3 Question | 5 days ago | A quick question about your lead process |

Merge tags used: `*|FNAME|*` (first name) and `*|INTEREST|*` (set by the lead scoring scenario from the HubSpot Interest field).

## Email 1: welcome
Hi *|FNAME|*, thanks for signing up. Over the next few days I will send two short emails on how small SaaS teams can score and sort leads using free tools. The full setup, with the Make blueprint and the Google Sheet template, is on GitHub.

## Email 2: tailored by interest
One paragraph is shown depending on `INTEREST`:
- **Automation:** every new lead gets a score from company size, job seniority, interest and email type, and the score decides who gets a sales alert and who gets nurtured.
- **Analytics:** every lead is logged to a Google Sheet with its score and stage, and a Monday email summarises new leads, stage counts and the average score.
- **Content (or anything else):** because every lead is tagged by interest, you can see which topics bring in the highest-scoring leads and write more of those.

Then: you can copy the scoring rules and change them to fit your own product.

## Email 3: a question
One question: which CRM and email tool does your team use today? Reply with your tool stack and a sentence on how you sort leads now, and I will say which parts of this setup you could reuse.

All three end with the list address and an unsubscribe link, which Mailchimp requires.

## Rules before you switch it on
- Only people who agreed to receive emails should be in the audience. The HubSpot form in this build has no consent checkbox. Add one (or a data privacy field) before using it with real people.
- The production scenario has no test filter. It emails every audience member whose signup date matches.
