# Purchase Frequency and Basket Size Analysis on Grocery Data

This project looks at the grocery file from a shopping-visit perspective rather than a row-by-row perspective. Each basket is rebuilt from a member and shopping date, then I use those baskets to compare visit frequency, basket depth, product demand, weekday traffic and product combinations.

## What I wanted to answer?

The main questions were practical ones:

- how many items are usually purchased in one visit?
- how often does each customer come back?
- which products create the most demand?
- which weekday brings the most shopping visits?
- do basket sizes change across the week?
- which products repeatedly appear together?
- are total visits concentrated among a few very active customers?

## How I handled the basket logic?

A basket is one unique `Member_number + Date` combination.

The source file has item-level rows, so repeated product lines are kept when calculating basket size and product purchase counts. For product-pair analysis, I use unique products within each basket before generating pairs. This avoids inflating a pair simply because the same item appears more than once in one visit.

Purchase frequency is based on unique shopping dates per member.

The original task lists `6–10 visits` and `10+ visits`, which overlap at 10. I used `11+ visits` for the final segment so the groups remain mutually exclusive.

## What is inside the project?

```text
grocery_basket_analysis/
├── data/
│   └── Groceries_dataset.csv
├── visuals/
│   ├── basket_size_distribution.png
│   ├── customer_frequency_segments.png
│   ├── top_20_products.png
│   ├── weekday_transaction_volume.png
│   ├── avg_basket_size_by_weekday.png
│   ├── top_product_pairs.png
│   └── top10_customers_monthly_frequency.png
├── grocery_basket_analysis.ipynb
├── note.md
└── README.md
```

## Results I would keep in mind

The uploaded file contains 38,765 item rows, 3,898 customers and 167 products. Rebuilding baskets from member and date gives 14,963 shopping visits.

Average basket size is 2.59 items and the median is 2. Two-item baskets alone represent about 67.37% of all visits, so the dataset is dominated by short shopping missions rather than large stock-up baskets.

`whole milk` is the most purchased product with 2,502 recorded purchases, followed by `other vegetables` with 1,898 and `rolls/buns` with 1,716.

Thursday has the highest basket traffic with 2,188 visits. Wednesday has the largest average basket, but the weekday averages are very close to one another, so the difference is not operationally dramatic.

The most common product pair is `other vegetables + whole milk`, appearing together in 222 baskets.

Customer activity is spread across the base rather than being dominated by a small VIP group. The ten most active customers account for only about 0.70% of all baskets.

## Running the notebook again

Open `grocery_basket_analysis.ipynb` from the project folder and run the cells from top to bottom. The notebook expects the source data at:

```text
data/Groceries_dataset.csv
```

The figures are recreated inside `visuals/`.
