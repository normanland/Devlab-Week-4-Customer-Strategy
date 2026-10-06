# DevLab Week 4 — Customer Strategy Analytics

## Retain. Prioritize. Expand.

Week 4 is built around three recurring business decisions:

```text
Who should we try to retain?
Who should we prioritize?
What behavior can we grow?
```

Three different projects approach those questions from different analytical angles.

---

## Decision Board

| Business Decision | Analytical Lens | Main Signal | Output |
|---|---|---|---|
| **RETAIN** | Customer churn | Risk concentration | Tableau retention dashboard |
| **PRIORITIZE** | RFM segmentation | Customer value & engagement | Actionable customer segments |
| **EXPAND** | Basket behavior | Shopping mission & product combinations | Store and basket-growth insights |

---

# RETAIN

## Telco Customer Churn

**7,043 customers → 1,869 churned → 26.5% churn**

The first project focuses on identifying where customer loss is concentrated rather than treating churn as one company-wide percentage.

The dashboard combines contract type, internet service, tenure, payment method, and monthly charges to isolate commercially important risk.

### Highest-Risk Concentration

```text
Fiber optic
+
Month-to-month
=
54.6% churn
```

This segment contains **2,128 customers** and represents approximately **$100.48K in monthly revenue associated with churned customers**.

Across the full customer base, monthly revenue associated with churn is approximately **$139K**.

### Decision

Retention resources should not be spread equally across every customer.

The dashboard points first toward:

```text
early tenure
short contracts
fiber optic customers
electronic check users
```

**Tool:** Tableau

---

# PRIORITIZE

## RFM Customer Segmentation

**2,823 transactions → 92 customers → 7 behavioral segments**

Not every customer requires the same marketing treatment.

RFM converts transaction history into three signals:

```text
R  → How recently did they buy?
F  → How often do they buy?
M  → How much have they spent?
```

The result is a customer prioritization system rather than a simple sales ranking.

### Portfolio Snapshot

```text
Champions             9
Loyal                17
Potential Loyalists  13
At Risk                7
Needs Attention       20
Lost                  11
Low Engagement        15
```

The **9 Champions generate 26.0% of customer revenue**.

At the opposite end, the At Risk segment contains customers with historically strong value but weakening recency.

### Decision

```text
Champions       → protect
Loyal           → deepen
Potential       → develop
At Risk         → win back
Lost            → reactivate selectively
```

**Tools:** Python · pandas · RFM scoring

---

# EXPAND

## Grocery Basket Behavior

**38,765 item rows → 14,963 shopping visits → 3,898 customers**

The third project changes perspective.

Instead of asking which customer is valuable, it asks:

> What actually happens inside a shopping visit?

A basket is reconstructed from:

```text
Member_number + Date
```

This makes it possible to analyze basket depth, visit frequency, weekday traffic, and product co-occurrence.

### Shopping Mission

Average basket:

```text
2.59 items
```

Median:

```text
2 items
```

And **67.37% of all baskets contain exactly two items**.

That makes basket expansion a more interesting commercial opportunity than designing only for large stock-up trips.

### Product Signal

```text
whole milk         2,502 purchases
other vegetables   1,898
rolls/buns         1,716
```

Most common pair:

```text
other vegetables + whole milk
222 baskets
```

### Customer Concentration

The ten most active customers account for only about:

```text
0.70%
```

of all baskets.

Demand is therefore broad rather than dependent on a tiny VIP customer group.

### Decision

Focus on:

```text
staple availability
complementary placement
small-basket expansion
medium-frequency customer growth
```

**Tools:** Python · pandas · basket analysis

---

# The Customer Strategy Loop

```text
                    ┌───────────────┐
                    │   CUSTOMER    │
                    └───────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
          RETAIN        PRIORITIZE       EXPAND
             │              │              │
             ▼              ▼              ▼
           churn            RFM           basket
             │              │              │
             └──────────────┼──────────────┘
                            │
                            ▼
                     BUSINESS ACTION
```

The three projects solve different problems, but they share one principle:

> Analysis becomes useful when a metric changes what the business should do next.

---

# Repository Map

```text
01-telco-churn-retention-dashboard/
│
├── telco_churn_dashboard.twbx
├── telco_churn_dashboard_overview.png
├── insights.md
└── README.md


02-rfm-customer-segmentation/
│
├── data/
│   └── sales_data_sample.csv
├── outputs/
│   ├── figures/
│   ├── rfm_customer_report.csv
│   ├── rfm_segment_summary.csv
│   └── rfm_marketing_actions.csv
├── rfm_customer_segmentation.ipynb
├── insights.md
└── README.md


03-grocery-basket-behavior-analysis/
│
├── data/
│   └── groceries_dataset.csv
├── visuals/
├── grocery_basket_analysis.ipynb
├── insights.md
└── README.md
```

---

## Stack

`Tableau` · `Python` · `pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `Jupyter`

---

## Week 4 in One Line

```text
Retain the right customers.
Prioritize the right relationships.
Expand the right behavior.
```
