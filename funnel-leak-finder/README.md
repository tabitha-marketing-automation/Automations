# Funnel Leak Finder

A one-page calculator that shows an early-stage SaaS founder how much monthly revenue is tied up in leads nobody followed up, and which fix to start with.

![Funnel Leak Finder, example numbers](screenshots/leak-finder-final-frame.png)

**Live tool:** https://149661254.hs-sites-eu1.com/funnel-leak-finder (example numbers shown by default)

## Who it is for

Founders and first marketing hires who get a trickle of leads, reply when they can and have no idea what that costs.

## What it does

The founder answers a few questions with simple counts from a typical month, so there is no percentage maths:

- how many people visit the website, how many get in touch, how many are a good fit, how many book a call, demo or trial, and how many become paying customers
- what one new customer is worth each month
- out of those who get in touch, how many get no personal reply within 24 hours, and out of the good-fit ones, how many never get a second follow-up
- how fast they reply, whether a follow-up sequence exists and whether they get a weekly report

The tool works out every percentage itself. A later step can never be larger than the one before it, so a miscounted entry is capped, not rejected.

It returns:

- new MRR per month today
- MRR tied up in leads nobody followed up
- MRR they could add by winning back a share they choose (default 25%, their own assumption)
- the weakest conversion step after the lead stage
- a short list of fixes, each linking to a build guide in this repo

## How it calculates

```
leads            = visitors x visitor-to-lead
lead-to-paid     = lead-to-qualified x qualified-to-trial x trial-to-paid
MRR tied up      = leads without a reply in 24h x lead-to-paid x revenue per customer
                 + qualified leads without a second touch x trial-to-paid path x revenue per customer
MRR to win back  = MRR tied up x recovery share
```

The two groups can overlap, so the total is an upper bound. The tool uses no industry benchmarks. Every number comes from the person using it.

## Use it

Open `index.html` in a browser. It has no build step and sends no data anywhere. To host it, upload the single file to any static host.

## Known limits

- It is a model, not a measurement. Garbage in, garbage out.
- It does not know your sales cycle length or churn.
- The default values are examples, not benchmarks.
