# Predicting Dominican Gasoline Prices with Simple Linear Regression

A pedagogical machine learning project applying concepts from Andrew Ng's Machine Learning Specialization to real, publicly available Dominican Republic fuel price data (2000–2026).

## What this notebook does

This notebook builds a simple linear regression model that predicts the weekly official **Gasolina Regular** price in the Dominican Republic using just two inputs:

1. **This week's USGC benchmark price** (U.S. Gulf Coast gasoline spot price), converted to RD$/gallon, observed the Tuesday before the price is set, per Decree 307-01.
2. **Last week's official Gasolina Regular price.**

It walks through the complete pipeline end to end:

- **Data loading and cleaning** — merges three public sources: MICM weekly fuel prices, EIA's USGC benchmark series, and BCRD's daily exchange rate, joined using the legally mandated Tuesday-lag rule.
- **Exploratory data analysis** — descriptive statistics, price history visualization, and correlation analysis, including the discovery that ~89% of post-2022 weeks show a frozen (unchanged) price due to a government subsidy policy.
- **Mathematical foundation** — the hypothesis function, cost function, and gradient descent, all implemented from scratch in NumPy (not just scikit-learn), with the cost function's convergence tracked and plotted.
- **Model training and evaluation** — an honest, chronological (non-shuffled) train/test split, so the model is tested on a pricing regime (the 2022 price freeze) it never saw during training.
- **Naive baseline comparison** — tests the model against the simplest possible alternative ("assume no change from last week") to check whether the model's high R² reflects real learned structure or just the persistence of the price series.
- **Live, real-world validation** — a genuine out-of-sample prediction test against an actual MICM bulletin, showing the model closely recovers the pre-subsidy formula price even though it can't predict the government's discretionary adjustment.
- **A reusable prediction cell** — plug in fresh weekly data to generate a live prediction and check its accuracy once the real price is announced.

## Key result

Test R² = 0.9648, MAE ≈ RD$1.59/gal. But the more interesting finding: the model's prediction error against the actual consumer price closely tracks the size of the government's subsidy adjustment, turning a "miss" into a useful, real-time estimate of policy intervention.

## Data sources

- [MICM](https://micm.gob.do/) — Ministerio de Industria, Comercio y MiPymes, weekly fuel price bulletins
- [U.S. EIA](https://www.eia.gov/) — USGC Conventional Gasoline Regular Spot Price (series `EER_EPMRU_PF4_RGC_DPG`)
- [BCRD](https://www.bcrd.gov.do/) — Banco Central de la República Dominicana, daily exchange rate

## Disclaimer

This is a pedagogical exercise, not a production forecasting tool or a definitive economic model of Dominican fuel pricing.

## License

CC BY 4.0 — free to use, share, and adapt, with attribution.

## Author

Allen R. Silverio Olivo, Independent Research
