# Customer Retention & Revenue Risk Analysis — E-commerce (Olist Brazil)

RFM segmentation and revenue-at-risk analysis for a Brazilian e-commerce marketplace, built end-to-end with SQL, Python, and Power BI.

## Executive Summary

Customers in the "At Risk" segment historically spent nearly as much per person as top-tier "Champions" (R$169.68 vs. R$176.96 average) — but have gone quiet. This segment represents 15.9% of customers yet accounts for **R$2.51M (16.3%) of total historical revenue**. Because their past spending behavior closely mirrors the company's best customers, this group represents the highest-leverage win-back opportunity: retaining even a fraction of this R$2.51M is likely more cost-effective than acquiring new customers of equivalent value.

## Business Problem

Which customers are we losing, why, and how much revenue is at risk? This is one of the most common — and most fundable — questions in e-commerce analytics. This project answers it using RFM (Recency, Frequency, Monetary) segmentation to identify at-risk high-value customers and quantify the revenue tied to their retention.

## Data Source

[Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — real, anonymized transactional data from ~100k orders on a real Brazilian marketplace, including orders, customers, and payments.

## Methodology

1. **SQL (SQLite)** — Loaded raw CSVs into a relational database. Joined orders, customers, and payments tables, filtering to `delivered` orders only.
2. **Data quality check** — Identified and corrected a common pitfall in this dataset: Olist assigns a new `customer_id` to every order, so a repeat customer looks like multiple different people. Used `customer_unique_id` instead to correctly track repeat purchases.
3. **Python (pandas)** — Calculated Recency, Frequency, and Monetary value per customer, scored each on a 1–5 scale using quintiles, and combined scores into 5 business segments (Champions, At Risk, Hibernating, Needs Attention, New Customers).
4. **Power BI** — Built an interactive dashboard: revenue-by-segment chart, a recency-vs-spend scatter plot colored by segment, and a KPI card surfacing the revenue-at-risk figure.

## Key Finding

| Segment | Customers | % of Customers | Avg. Spend | Total Revenue | % of Revenue |
|---|---|---|---|---|---|
| Needs Attention | 33,623 | 36.0% | R$159.78 | R$5.37M | 34.8% |
| Champions | 14,961 | 16.0% | R$176.96 | R$2.65M | 17.2% |
| **At Risk (High Value)** | 14,803 | 15.9% | R$169.68 | **R$2.51M** | **16.3%** |
| New Customers | 14,984 | 16.1% | R$163.43 | R$2.45M | 15.9% |
| Hibernating | 14,986 | 16.1% | R$162.96 | R$2.44M | 15.8% |

The near-identical average spend between Champions and At Risk customers is the core insight: these are not low-value customers drifting away — they are proven high-value customers going quiet, making them the clearest priority for a targeted win-back campaign.

## Dashboard

The Power BI dashboard (`retention_dashboard.pbix`) includes:
- Revenue by customer segment
- Recency vs. spend scatter plot, colored by segment
- KPI card showing R$2.51M revenue at risk

## Tools Used

- **SQL** (SQLite) — data loading, joins, filtering
- **Python** (pandas) — RFM calculation, scoring, segmentation
- **Power BI** — dashboard and visualization
- **Jupyter Notebook** — analysis environment

## What's Next

- Build a churn prediction model (logistic regression or decision tree) to proactively flag customers before they become "at risk"
- Segment the win-back opportunity further by product category and region to prioritize campaign targeting
- Track cohort retention over time to measure whether retention is improving or declining
