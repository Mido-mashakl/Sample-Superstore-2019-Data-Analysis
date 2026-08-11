# Sample Superstore 2019 — Data Analysis

A multinational retail company wants an automated analytical solution to monitor sales,
profitability, customer behavior, and operational performance. This project takes the
classic **Sample Superstore** dataset from raw CSV to a set of business-ready insights
and visuals, following a repeatable, four-stage analytics workflow.

## Project Workflow

The analysis is split across four notebooks, each picking up exactly where the last one
left off — every notebook loads only the output of the previous stage, so the whole
pipeline can be re-run end to end or re-entered at any stage.

| Stage | Notebook | What it does |
|---|---|---|
| 1. Clean | [`exploring_cleaning_data.ipynb`](exploring_cleaning_data.ipynb) | Loads the raw CSV, profiles it, fixes types/duplicates/missing values, and saves a clean copy. |
| 2. Engineer | [`feature_engineering_analysis.ipynb`](feature_engineering_analysis.ipynb) | Defines the business questions, builds derived features (dates, margins, discount buckets, RFM), and prepares the analysis-ready dataset. |
| 3. Analyze | [`eda_and_data_analysis.ipynb`](eda_and_data_analysis.ipynb) | Runs the EDA and answers each business question with grouped/aggregated tables, then exports them as reusable "handoff" tables. |
| 4. Visualize | [`data_visualization.ipynb`](data_visualization.ipynb) | Turns the handoff tables into charts — regional profit, seasonality, discount impact, shipping performance, RFM segmentation, top products — and a one-page executive summary dashboard. |

## Business Questions Answered

1. Which State generates the most total Profit, and which generates the biggest total loss?
2. Is there a relationship between Discount and Profit?
3. Does Ship Mode relate to profitability or shipping time?
4. Is there seasonality in Sales, by month or by day of week?
5. Who are the most valuable customers, and how should we segment them using RFM?
6. Is Sales related to time (year, quarter, month)?
7. Did Shipping Days affect order volume, profit, or vary by Ship Mode / Region?
8. How does Profit Margin vary across Categories?
9. What is the relationship between Profit Margin and Quantity?
10. How does Profit Margin vary across Customer Segments?
11. Which Products have the highest Profit per Unit?

## Data

- **`Sample-Superstore2019.csv`** — the raw source data (9,995 orders, 22 columns: order/ship
  info, customer, geography, product, sales, quantity, discount, profit).
- **`*.parquet`** — cleaned / prepared / RFM snapshots saved between stages.
- **`handoff_data/`** — the analysis-ready tables (entity tables in Parquet, summary tables in
  CSV) produced by the EDA notebook and consumed directly by the visualization notebook.

## Key Findings

- **Geography:** Profit is concentrated in California and New York, while Texas, Ohio and
  Pennsylvania post the largest losses despite solid sales.
- **Discounting:** Profit margin declines steadily as discount depth increases, turning
  negative at the highest discount tier.
- **Seasonality:** Sales climb through the year and peak in Sep–Dec; weekends underperform
  weekdays.
- **Shipping:** Ship Mode strongly controls delivery speed but barely moves average profit —
  it's an operations lever, not a profitability lever.
- **Category / Segment margin:** Furniture's margin (≈2.5%) lags far behind Technology and
  Office Supplies (≈17%); Home Office is the most profitable customer segment.
- **Customers (RFM):** Champions make up well under half the customer base but drive the
  single largest share of revenue; At Risk customers hold enough remaining value to justify
  a targeted win-back campaign.
- **Products:** Profit-per-unit is dominated by a small set of high-value Technology products
  (copiers, printers), not high-volume Office Supplies items.

See [`data_visualization.ipynb`](data_visualization.ipynb) for the charts behind each finding.

## Getting Started

```bash
git clone https://github.com/Mido-mashakl/Sample-Superstore-2019-Data-Analysis.git
cd Sample-Superstore-2019-Data-Analysis
pip install -r requirements.txt
pip install pyarrow scikit-learn squarify   # needed by the notebooks, not yet pinned in requirements.txt
jupyter lab
```

Then open the notebooks in order (1 → 4) listed above, or jump straight into
`data_visualization.ipynb` — it reads directly from `handoff_data/` and needs no prior
notebook to be re-run.

## Tech Stack

pandas · NumPy · Matplotlib · scikit-learn (KMeans clustering for RFM) · squarify (treemaps) ·
PyArrow (Parquet I/O)
