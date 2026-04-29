# ✈️ Cleared for Takeoff?
### A Visual Analysis of U.S. Domestic Flight Delay Patterns (2019–2023)

**Author:** Bobby Bagley  
**Date:** April 2026

---

## Overview

This project is a data-driven visual story built around one central question: **what actually causes flight delays, and can we see the patterns?**

Using five years of U.S. domestic flight records from the Bureau of Transportation Statistics, the analysis is structured as four chapters — each answering a distinct investigative question. The emphasis is on clear, interpretable visualizations and actionable insights rather than modeling.

---

## Central Questions

| Chapter | Question |
|---|---|
| 1 — Temporal Patterns | *When* do delays peak? |
| 2 — Geographic Patterns | *Where* are delays most severe? |
| 3 — Delay Cause Breakdown | *Why* do flights get delayed? |
| 4 — Airline & Route Analysis | *Who* is most affected? |

---

## Dataset

| | |
|---|---|
| **Source** | [Flight Delay & Cancellation Dataset 2019–2023](https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023) |
| **Origin** | U.S. Department of Transportation — Bureau of Transportation Statistics (BTS) |
| **Format** | CSV |
| **Raw Size** | ~3 million rows, 32 columns |
| **Time Span** | January 2019 – December 2023 |

The dataset is loaded directly from Kaggle using the `kagglehub` library. No CSV file needs to be attached or downloaded manually — a free Kaggle account and API key are all that is required to run this notebook.

---

## Key Findings

**Chapter 1 — When?**
- The domino effect is real: delay rate climbs from **7.3% at 5AM** to **28.3% at 9PM** as delays compound throughout the day
- Summer (Jun–Aug) and the winter holiday corridor (Nov–Jan) are the peak delay seasons every year
- COVID-19 is the single greatest structural break in the data — delays collapsed to near zero in March 2020 as air travel fell by over 60%
- Day of week has minimal impact — only a 3.7% spread separates the best day (Tuesday) from the worst (Friday)

**Chapter 2 — Where?**
- Airport size does **not** predict delay rate — large hubs and small regional airports often perform similarly
- Chicago Midway (MDW) accounts for **7 of the 20 most-delayed routes** in the country
- Houston Hobby (HOU) carries a **24.3% delay rate** — one of the worst in the country — while Bush Intercontinental (IAH) sits right at the national average of **18.2%**

**Chapter 3 — Why?**
- Carrier and Late Aircraft delays dominate every year — both are **100% within airline control**
- Weather ranks as the least common cause, ahead of only Security — a counterintuitive finding
- When weather does delay a flight, it delays it significantly (~64–73 minutes) regardless of season — summer thunderstorms are just as disruptive as winter storms
- SkyWest (OO) has the highest carrier delay at ~50 minutes, likely reflecting scheduling pressure from mainline carriers it operates for

**Chapter 4 — Who?**
- The five worst-performing carriers are all low-cost or ultra-low-cost carriers (JetBlue, Frontier, Allegiant, Southwest, Spirit)
- Flight distance is a **poor predictor** of delay risk — the trend line is nearly flat
- Hawaiian Airlines (HA) is the standout best performer with the tightest, lowest delay distribution
- What separates good carriers from bad is not just how often they delay but **how long and how consistently**

---

## Visualizations

| Chart | Type | Library | Chart |
|---|---|---|---|
| Monthly delay rate heatmap | Heatmap | seaborn | |
| Delay rate by hour of day | Line chart with confidence band | **Altair** | |
| Delay rate by day of week | Bar chart | seaborn | |
| Departure delay by airport | Interactive bubble map | plotly | |
| Top 20 most-delayed routes | Horizontal bar chart | matplotlib | |
| Houston IAH vs. HOU spotlight | Annotated bar chart | matplotlib | |
| Delay cause composition by year | 100% stacked bar chart | matplotlib | |
| Delay cause by airline | Grouped bar chart | seaborn | |
| Weather delay seasonality | Layered area chart | **Altair** | |
| Delay rate by airline | Ranked horizontal bar chart | matplotlib | |
| Delay rate vs. flight distance | Scatter plot with regression line | **Altair** | |
| Distribution of delay length | Box plot | seaborn | |


---

## Getting Started

### Prerequisites
- A free [Kaggle account](https://www.kaggle.com) and API key
- Python 3.10+

### Installation

```bash
pip install pandas numpy matplotlib seaborn plotly altair kagglehub
```

### Running the Notebook

1. Open the notebook in Google Colab or Jupyter
2. Run the environment setup cell
3. When prompted by `kagglehub.login()`, enter your Kaggle username and API key
4. Run all remaining cells in order

> The dataset downloads automatically to a local cache directory. No manual file handling required.

---

## Project Structure

```
├── domestic_flight_delay_analysis.ipynb   # Main analysis notebook
├── README.md                              # This file
```

---

## Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, aggregation |
| `numpy` | Numerical operations |
| `matplotlib` | Static charts — bar charts, annotated comparisons |
| `seaborn` | Statistical charts — heatmaps, box plots, grouped bars |
| `altair` | Interactive charts — line chart, scatter plot, area chart |
| `plotly` | Interactive geographic bubble map |
| `kagglehub` | Dataset acquisition from Kaggle |

---

## Notes

- A second supplementary chart (unbinned scatter) is included in Section 4.2 to illustrate why distance binning was necessary — the raw scatter is included for comparison
- The `DELAY_DUE_WEATHER` analysis in Section 3.3 filters to flights with actual weather delays (>0 minutes) to show meaningful delay duration rather than a dataset-wide average diluted by non-weather flights
- Airport coordinates for the bubble map are sourced from the [Airport Codes dataset](https://raw.githubusercontent.com/datasets/airport-codes/master/data/airport-codes.csv) and merged on IATA code at runtime

---

## Related Project

This notebook is the **data visualization companion** to a parallel machine learning project that builds a binary classification model predicting flight delays on the same dataset. Together they form a cohesive, end-to-end portfolio piece.

See: `flight_delay_predictor.ipynb`
