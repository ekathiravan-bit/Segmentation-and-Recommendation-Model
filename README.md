# Churn Risk Score Model

Customer segments and a transparent, rule-based churn-risk score built from contract type, tenure and support tickets. One static page (`index.html`) with no build step.

**Live page:** _add your GitHub Pages link here after you enable Pages (see "Publish" below)_

## Features used

| Feature | Why |
|---|---|
| Contract type | Every Month-to-Month customer churned. No One Year or Two Year customer did. |
| Tenure (months) | Churned customers were all in their first 14 months. |
| Support tickets | Churned customers all had 3 or more tickets. Retained customers had 2 or fewer. |
| Payment method | Not scored. In this sample it is tangled up with contract type, so its effect cannot be separated. |

## Segments (first matching rule wins)

| Segment | Rule | Customers | Churned | Monthly revenue |
|---|---|---|---|---|
| Early and frustrated | tenure ≤ 12 AND tickets ≥ 3 | 6 | 6 | $329.94 |
| Month-to-month, settled | Month-to-Month, not above | 1 | 1 | $79.99 |
| Mid-term committed | One Year | 4 | 0 | $259.96 |
| Long-term loyal | Two Year | 4 | 0 | $599.96 |

## Scoring rubric (0–100 points)

| Signal | Condition | Points |
|---|---|---|
| Contract | Month-to-Month / One Year / Two Year | 40 / 15 / 0 |
| Tenure | 0–6 / 7–12 / 13–24 / 25+ months | 30 / 20 / 10 / 0 |
| Support tickets | 5+ / 3–4 / 1–2 / 0 | 30 / 20 / 10 / 0 |

Tiers: **High** 60 or more, **Medium** 30 to 59, **Low** under 30. Example: Month-to-Month (40) + 8 months (20) + 4 tickets (20) = 80, High.

## Results

| Tier | Customers | Churned |
|---|---|---|
| High | 7 | 7 |
| Medium | 4 | 0 |
| Low | 4 | 0 |

## Edge cases tested

The page runs 23 checks on load: every tenure and ticket band boundary, tier cut-offs at 29/30 and 59/60, maximum and minimum scores, a new Two Year customer with 6 tickets (60, High), a quiet long-term Month-to-Month customer (40, Medium), and invalid input (blank tenure, negative tickets, unknown contract) which returns no score.

## Retention actions

- **Early and frustrated:** proactive outreach after the third ticket in the first year.
- **Month-to-month, settled:** annual-contract discount after month 12.
- **Mid-term committed:** renewal outreach 60 days before term end.
- **Long-term loyal:** named contact and quarterly check-in.

Impact ranges on the page assume outreach keeps 10–30% of would-be churners. That is a planning assumption, not a measured result.

## Limitations

- The data has 15 customers, so one customer shifts a segment by several points.
- The weights were chosen after looking at this same data. The clean split in the results shows the rules describe the sample, not that they predict new customers.
- There is no usage, billing or competitor data, and only one snapshot in time.
- Re-check the weights on a larger held-out set before using the score to decide who gets contacted.

## Data

`data/customer_churn_sample.csv`. Source: https://edvyro.in/datasets/customer_churn_sample.csv

## Publish

1. Push this folder to a new GitHub repository.
2. Open Settings → Pages, set the source to the `main` branch and the root folder, and save.
3. The page goes live at `https://<your-username>.github.io/<repo-name>/`. Paste it above and submit it.
