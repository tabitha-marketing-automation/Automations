# A/B test plan

| Field | Your answer |
| --- | --- |
| Ad being tested | |
| Page A (current) | URL |
| Page B (matched) | URL |
| One change between A and B | e.g. headline repeats the ad promise |
| Hypothesis | If the headline repeats the ad promise, more visitors will sign up because they see what they clicked for |
| Main metric | Visitor to lead conversion rate |
| Traffic split | 50 / 50, same audience, same days |
| Start date / end date | Decide in advance. Do not stop early because one version looks ahead |
| Visitors needed per page | See the rule of thumb below |
| Result | |
| Decision and what I learned | |

## Rule of thumb for sample size
For about 80% power and 95% confidence, per page you need roughly `16 x p x (1 - p) / d^2` visitors, where p is your current conversion rate and d is the lift you want to detect, both as decimals.

Example: p = 5% and you want to detect a rise to 7% (d = 0.02): 16 x 0.05 x 0.95 / 0.0004 = 1,900 visitors per page.

Small sites often cannot reach that. In that case test a big change (the whole message, not a button colour), run it longer, and treat the result as a direction rather than proof.
