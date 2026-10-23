# RFM Customer Segmentation

Segmenting retail customers by **Recency, Frequency and Monetary value** with Python, and a recommended marketing action for each segment.

🇷🇺 [Русская версия](README.ru.md) · [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dreamkeeperx/rfm-customer-segmentation/blob/main/RFM_Customer_Segmentation.ipynb)

## Overview

Not all customers are equally valuable, so one generic campaign for everyone wastes budget. RFM analysis groups customers by their purchase history:

- **Recency (R)** – how many days ago the customer made the last purchase
- **Frequency (F)** – how many purchases the customer made
- **Monetary (M)** – how much money the customer spent in total

In this project, 476 customers are scored on each metric, split into **9 segments**, and every segment gets a practical recommendation (retention, upsell, win-back, etc.).

## Key Results

![Customer segments distribution](images/segment_distribution.png)

| Segment | Customers | Share | Recommended action |
|---|---:|---:|---|
| Hibernating | 195 | 41.0% | Low-cost automated emails with discounts on popular products |
| Promising | 52 | 10.9% | Bundles, accessory recommendations, free-shipping threshold |
| Champions | 49 | 10.3% | VIP status, priority service, early access (no direct discounts) |
| Lost | 46 | 9.7% | One last-chance campaign, then archive from active CRM |
| New Customers | 37 | 7.8% | Welcome emails, short-term promo code for the 2nd order |
| Loyal Customers | 36 | 7.6% | Cross-sell, multi-tier loyalty program |
| Potential Loyalists | 29 | 6.1% | Subscriptions, premium upsell, time-limited coupons |
| About to Sleep | 23 | 4.8% | Personalized picks, satisfaction survey, bonus expiry reminders |
| At Risk | 9 | 1.9% | Strong win-back offers, personal manager call |

## Dataset

[Retail Sales Dataset](https://www.kaggle.com/datasets/mohammadtalib786/retail-sales-dataset) from Kaggle: 1,000 transactions, 9 columns (transaction ID, date, customer ID, gender, age, product category, quantity, price per unit, total amount). Transactions cover 2023 up to 2024-01-01.

> ⚠️ **Data note.** In the original dataset every customer has exactly one transaction, so RFM cannot work on it. To simulate repeat purchases, I randomly reassigned customer IDs (`np.random.seed(42)`, IDs from 0 to 599, which gives 476 unique customers). Because of this, **segment sizes are illustrative: the project demonstrates the method, not real business findings.** Gender and age were not changed and are not used in the analysis.

## Methodology

1. **Preprocessing** – column names to snake_case, date conversion, simulation of repeat purchases (see data note).
2. **Reference date** – the last transaction date in the data.
3. **Customer-level table** – Recency, Frequency and Monetary per customer (`groupby` + `agg`).
4. **Scoring** – quartile-based scores from 1 to 4 for each metric (for Recency, fewer days = higher score).
5. **RFM class** – the three scores are combined into a code like `443`.
6. **Segmentation** – RFM classes are mapped to 9 business segments with rule-based logic (`np.select`).
7. **Visualization and recommendations** – segment distribution and an action plan per segment.

## Tech Stack

Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter Notebook · kagglehub

## Project Structure

```
rfm-customer-segmentation/
├── RFM_Customer_Segmentation.ipynb   # full analysis
├── images/
│   └── segment_distribution.png
├── requirements.txt
└── README.md
```

## How to Run

```bash
git clone https://github.com/dreamkeeperx/rfm-customer-segmentation.git
cd rfm-customer-segmentation
pip install -r requirements.txt
jupyter notebook RFM_Customer_Segmentation.ipynb
```

The dataset is downloaded automatically with `kagglehub` (a free Kaggle account may be required). You can also open the notebook in Google Colab with the badge above.

## Limitations and Next Steps

- Repeat purchases are simulated, so results should be tested on real transaction data (e.g. Online Retail II).
- Quartile thresholds are calculated on this small sample; with more data, quintiles or business-defined thresholds may fit better.
- Possible extension: compare rule-based RFM segments with K-Means clustering and build a Power BI dashboard.
s
## Author

[GitHub](https://github.com/dreamkeeperx)
