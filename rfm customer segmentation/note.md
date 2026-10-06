# RFM Methodology and Segment Actions

## Objective

This project converts transaction-level sales data into customer-level RFM profiles. RFM stands for **Recency**, **Frequency**, and **Monetary value**. Together, these measures describe how recently a customer purchased, how often they order, and how much revenue they have generated.

The analysis uses `CUSTOMERNAME` as the customer key and follows the task requirement to count **unique `ORDERNUMBER` values** for Frequency.

## Dataset and preparation

- Source: Kaggle Sample Sales Data (`sales_data_sample.csv`)
- Transaction rows: **2,823**
- Unique customers: **92**
- Date range: **2003-01-06 to 2005-05-31**
- Reference date: **2005-06-01**
- Duplicate full rows: **0**
- Missing values in `CUSTOMERNAME`, `ORDERNUMBER`, `ORDERDATE`, and `SALES`: **0**

The complete file is retained because the task does not request filtering by order status. Status counts are still inspected in the notebook so this assumption remains visible.

## RFM calculation

For every `CUSTOMERNAME`:

- **Recency** = reference date − customer's most recent order date
- **Frequency** = number of unique `ORDERNUMBER` values
- **Monetary** = total `SALES`

Calculated ranges from the uploaded dataset:

| Metric | Min | Max | Mean | Median |
|---|---:|---:|---:|---:|
| Recency (days) | 1 | 509 | 182.83 | 186.00 |
| Frequency (orders) | 1 | 26 | 3.34 | 3.00 |
| Monetary ($) | 9,129.35 | 912,294.11 | 109,050.31 | 86,522.61 |

### Why these figures differ from some values in the assignment note

The supplied task note lists Frequency and Monetary ranges that do not match this specific uploaded file when the stated requirements are followed. In particular, the requirement defines Frequency as **unique orders**, so the notebook does not replace that definition with line-item counts merely to reproduce a benchmark. The reference date and customer count do match the assignment: `2005-06-01` and 92 customers.

## Quantile scoring logic

Each metric receives a score from 1 to 4 using `pd.qcut`.

- **Recency:** low days are better, so the labels are `[4, 3, 2, 1]`.
- **Frequency:** more unique orders are better, so the labels are `[1, 2, 3, 4]`.
- **Monetary:** higher customer revenue is better, so the labels are `[1, 2, 3, 4]`.

Frequency contains many tied values. A direct four-bin `qcut` therefore creates duplicate bin edges. The notebook first applies `rank(method="first")` and then runs `pd.qcut` on the ranks. This keeps four quartiles and still bases the ordering on the original metric.

`RFM_Segment` concatenates the three scores. For example, `444` means the customer is in the best quartile for all three dimensions.

## Segment definitions

The project uses seven mutually exclusive customer profiles. Rules are evaluated from top to bottom.

| Segment | Rule | Reasoning |
|---|---|---|
| Champions | `R=4, F=4, M=4` | Best current customers across every RFM dimension |
| Loyal | `R>=3, F>=3, M>=3`, excluding Champions | Strong repeat and value behavior with healthy recency |
| At Risk | `R<=2, F>=3, M>=3` | Valuable historical customers whose recency has weakened |
| Potential Loyalists | `R>=3, F>=2, M>=2` | Recent customers with a credible path to repeat behavior |
| Needs Attention | `R in {2,3}` and `F>=2 or M>=2` | Mid-strength customers who could drift without engagement |
| Lost | exact `111` | Weakest quartile on all three measures |
| Low Engagement | remaining combinations | No dominant high-value or high-engagement pattern |

This slightly broader **At Risk** recency rule (`R<=2`) produces a commercially useful pool of **7 customers**. Restricting it to `R=1` would miss customers who have already begun to drift but are not yet in the oldest quartile.

## Segment results

| Segment             |   Customer_Count |   Avg_Recency |   Avg_Frequency |   Avg_Monetary |   Revenue_Share_Pct |
|:--------------------|-----------------:|--------------:|----------------:|---------------:|--------------------:|
| Champions           |                9 |         19.44 |            8.11 |       290098   |               26.02 |
| Loyal               |               17 |        110.29 |            3.59 |       132895   |               22.52 |
| Potential Loyalists |               13 |         72.38 |            3    |        82951.3 |               10.75 |
| At Risk             |                7 |        239    |            3.29 |       125490   |                8.76 |
| Needs Attention     |               20 |        189.15 |            2.9  |        77039.8 |               15.36 |
| Lost                |               11 |        360.45 |            1.91 |        52367   |                5.74 |
| Low Engagement      |               15 |        293.87 |            2.13 |        72593.8 |               10.85 |

Notable results:

- **Champions:** 9 customers and **26.0%** of total customer revenue.
- **At Risk:** 7 customers. These customers have historically strong frequency/value but weaker recency.
- **Lost (`111`):** 11 customers, matching the exact weakest-score definition.

## Marketing actions

| Segment             | Business_Goal             | Recommended_Action                                                                                                                                    |
|:--------------------|:--------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| Champions           | Protect and amplify       | Offer VIP early access, premium bundles and referral rewards; avoid blanket discounts that erode margin.                                              |
| Loyal               | Deepen the relationship   | Use loyalty milestones, personalized cross-sell recommendations and replenishment reminders to move strong repeat buyers upward.                      |
| Potential Loyalists | Build the next habit      | Trigger a second/third-order incentive within 30–45 days and recommend products adjacent to the customer’s recent categories.                         |
| At Risk             | Win back before churn     | Launch a time-limited win-back campaign based on prior spend, surface previously purchased categories, and ask for a short reason-for-leaving signal. |
| Needs Attention     | Re-engage selectively     | Use product-interest reminders and moderate incentives; prioritize customers with above-median monetary value rather than mass messaging.             |
| Lost                | Reactivate cheaply        | Test one low-cost reactivation touch. If there is no response, reduce contact frequency to avoid wasting campaign budget.                             |
| Low Engagement      | Nurture with low friction | Use educational or discovery content, low-commitment offers and category recommendations to create another purchase occasion.                         |

## Visualization logic

The notebook contains:

1. **Segment size bar chart** — shows how the 92 customers are distributed.
2. **Recency vs Monetary scatter plot** — separates recent/high-value customers from older or lower-value customers; marker size carries Frequency.
3. **Average RFM heatmap** — compares the behavioral signature of each segment.
4. **3D Recency–Frequency–Monetary plot** — bonus view using raw customer metrics.
5. **Revenue-share bar chart** — added business view to reveal where customer revenue is concentrated.

## Files exported for marketing

- `outputs/rfm_customer_report.csv` — customer-level RFM metrics, scores, RFM code and segment.
- `outputs/rfm_segment_summary.csv` — segment counts, average metrics and revenue contribution.
- `outputs/rfm_marketing_actions.csv` — segment-specific campaign actions.

## Final interpretation

RFM should be used as a prioritization framework rather than as a permanent customer label. Recency changes with time, and customer behavior can move quickly after a new purchase or a campaign. A practical production workflow would refresh these scores on a regular schedule and then measure conversion, incremental revenue and retention by segment.
