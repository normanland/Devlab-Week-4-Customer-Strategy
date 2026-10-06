# Telco Customer Churn Dashboard

## Project Overview

This dashboard analyzes customer churn patterns in a telecommunications dataset and identifies the customer groups with the highest churn risk.

The project was initially planned in Power BI, but the final interactive dashboard was developed in Tableau after approval to migrate the visualization layer. The analytical objective and business requirements remained unchanged.

The dashboard focuses on contract type, internet service, tenure, payment method, customer distribution, monthly charges, and revenue exposure.

---

## Data Preparation Decisions

Several data preparation steps were performed before building the dashboard.

### Total Charges

The `TotalCharges` field required cleaning because some values were not initially interpreted correctly as numeric values.

The field was converted to a numeric data type so that it could be used reliably in calculations and visualizations.

### Churn Indicator

The original `Churn` field contains categorical values:

- Yes
- No

A numeric churn indicator was created to simplify aggregation:

- Yes = 1
- No = 0

This makes it possible to calculate churn rate using an average or ratio-based calculation.

### Tenure Bands

Customer tenure was grouped into business-friendly segments to make lifecycle patterns easier to analyze.

The tenure groups used in the dashboard are:

- 0–12 months
- 13–24 months
- 25–48 months
- 49+ months

This allows the dashboard to compare churn risk across different stages of the customer lifecycle.

### Monthly Charges Quartiles

Monthly Charges quartiles were calculated during the data-preparation stage:

- Q1 = 35.50
- Q2 = 70.35
- Q3 = 89.85

These thresholds can be used to distinguish lower-, medium-, and higher-charge customer groups.

---

## Tableau Calculated Measures

### Total Customers

The number of unique customers in the dataset.

Conceptually:

COUNTD(Customer ID)

### Churned Customers

Counts customers whose churn status is `Yes`.

Conceptually:

COUNTD(
    IF [Churn] = "Yes"
    THEN [Customer ID]
    END
)

### Churn Rate

The percentage of customers who churned.

Conceptually:

Churned Customers / Total Customers

The overall churn rate in the full dataset is approximately 26.5%.

### Average Monthly Charges

Average monthly charge across customers.

Conceptually:

AVG(Monthly Charges)

The overall value is approximately $64.8.

### Monthly Revenue at Risk

Monthly revenue associated with customers who have churned.

Conceptually:

SUM(
    IF [Churn] = "Yes"
    THEN [Monthly Charges]
    END
)

The full-dataset dashboard shows approximately $139K in monthly revenue associated with churned customers.

---

## Dashboard Design

The final dashboard contains four KPI cards:

- Total Customers
- Churn Rate
- Monthly Revenue at Risk
- Average Monthly Charges

The analytical sections include:

- Churn Rate by Contract Type
- Contract × Internet Service Churn Rate
- Churn Rate by Internet Service
- Churn Rate by Tenure Band
- Churn Rate by Payment Method
- Customer Distribution
- Monthly Charges by Churn Status
- Top Risk Segment

Interactive filters allow users to explore the dashboard by:

- Contract
- Internet Service
- Tenure Band

A second dashboard screenshot is included with the Contract filter set to `Month-to-month` to demonstrate dashboard interactivity.

---

## Key Findings

The analysis shows that churn is not evenly distributed across the customer base.

Month-to-month contracts have substantially higher churn than longer-term contracts.

Fiber optic customers show elevated churn compared with other internet service groups, particularly when combined with month-to-month contracts.

Customers in the earliest tenure group also show higher churn, indicating that the beginning of the customer lifecycle is an important retention period.

Electronic check users show comparatively high churn within the payment-method analysis.

The combination of Fiber optic service and Month-to-month contracts appears as the primary high-risk customer segment in the dashboard.

---

## Three Recommendations

### 1. Strengthen Early-Customer Retention

Prioritize onboarding and retention initiatives during the first 12 months of the customer lifecycle.

Customers with shorter tenure show higher churn, so early engagement, service follow-up, and targeted retention offers should be tested.

### 2. Encourage Longer-Term Contracts

Develop incentives that encourage suitable month-to-month customers to move to one-year or two-year contracts.

The dashboard shows a strong association between short-term contracts and higher churn.

### 3. Investigate High-Risk Service and Payment Segments

Prioritize customers using Fiber optic service together with Month-to-month contracts and investigate the high churn observed among Electronic check users.

Targeted retention campaigns and additional analysis of service experience, pricing, and payment behavior may help identify opportunities to reduce churn.

---

## Tools

- Tableau
- Data preparation and calculated fields
- Interactive filters
- KPI design
- Customer segmentation
- Churn analysis