# RFM Segmentation

A complete rule-based **RFM (Recency, Frequency, Monetary)** customer segmentation project built from `sales_data_sample.csv`.

## What the notebook does

- Parses `ORDERDATE` and validates the fields needed for RFM.
- Uses **2005-06-01** as the reference date (`max(ORDERDATE) + 1 day`).
- Calculates customer-level Recency, unique-order Frequency, and Monetary value.
- Scores R, F and M from 1 to 4 with `pd.qcut`.
- Handles tied Frequency values with a rank-then-qcut method so all four score bands remain available.
- Creates the compact `RFM_Segment` code such as `444` or `111`.
- Assigns seven actionable segments: Champions, Loyal, Potential Loyalists, At Risk, Needs Attention, Lost, and Low Engagement.
- Produces the three required charts, a bonus 3D RFM scatter plot, and an additional segment revenue-share chart.
- Exports customer, segment and marketing-action CSV reports.

## Main results from this dataset

- Customers analyzed: **92**
- Recency: **1–509 days** (mean 182.83)
- Frequency: **1–26 unique orders** (mean 3.34)
- Monetary: **$9,129.35–$912,294.11** (mean $109,050.31)
- Champions: **9 customers**, responsible for **26.0%** of customer revenue
- At Risk: **7 customers** under the project's `R<=2, F>=3, M>=3` rule
- Lost: **11 customers** with exact RFM code `111`

## Important dataset note

Some benchmark values written in the assignment description do not match this uploaded Kaggle file when the task definitions are followed exactly. The project therefore keeps the requested methodology — especially **Frequency = unique `ORDERNUMBER` count** — and documents the real calculated values rather than changing the logic to imitate preset numbers.

## How to run

1. Open a terminal in the project folder.
2. Install the dependencies:

```bash
pip install -r requirements.txt
```

3. Open `rfm_segmentation.ipynb` in JupyterLab, VS Code, or Jupyter Notebook.
4. Run all cells from top to bottom.

## Libraries

- pandas
- numpy
- matplotlib
- seaborn

## Submission files

For the DevLab submission, the core files are:

- `rfm_segmentation.ipynb`
- `note.md`
- `README.md`

The `outputs/` folder is included the bonus export and visualization requirements.
