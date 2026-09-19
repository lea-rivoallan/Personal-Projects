# Global Supplier Disruption Risk Modeling: A Multivariate Analysis

Exploratory analysis of a global supply chain dataset, combining a Principal Component
Analysis (PCA) of continuous risk factors with a Random Forest regression to identify
the strongest drivers of supplier delivery delays.

## Context

Supply chains are exposed to a mix of geopolitical, climatic, and economic shocks.
This project explores which of these factors — and which categorical attributes
(route, transportation mode, product category) — correlate most strongly with
delivery delays, using a public dataset of global shipments.

## Data

- **File:** `data/global_supply_chain_disruption_v1.csv`
- **Source:** *University source*
- Each row represents a shipment, with continuous risk indices (geopolitical risk,
  weather severity, inflation, shipping cost, order weight) and categorical attributes
  (origin/destination city, route type, transportation mode, product category,
  disruption event, delay in days).

## Method

1. **Standardization** of the five continuous exogenous features.
2. **Correlation analysis** to check for redundancy between the continuous features.
3. **PCA (exploratory)** — eigen-decomposition of the covariance matrix to read how
   variance is distributed across the continuous risk factors. This step is exploratory
   only: the Random Forest below is trained on the raw feature set, not on the
   principal components.
4. **Random Forest Regression** on the full feature set (continuous + one-hot encoded
   categoricals) to rank the top drivers of `Delay_Days`.
5. **Visualization** of the PCA scree/cumulative variance plot and the top 10 delay
   drivers.

## Key results

- Shipping cost (38.7%) and order weight (19.0%) together account for close to 58% of
  the Random Forest's delay-driver importance — shipment economics is the strongest
  predictor of delay.
- Geopolitical risk (10.1%) outweighs weather severity (4.7%) as a delay driver.
- Sea freight (10.0%) and chokepoint routes such as the Suez Canal (6.6%) are
  disproportionately associated with delays.
- In the PCA, geopolitical risk is the single largest source of variance (26.4%);
  weather severity contributes the least (13.7%).

## How to run

Run all cells from top to bottom. The dataset path is relative
(`data/global_supply_chain_disruption_v1.csv`), so keep the notebook and the `data/`
folder together.

## Possible extensions

- Feed the PCA components (instead of raw features) into the Random Forest and compare
  performance.
- Add LDA/QDA to classify shipments into delay-risk categories (low/medium/high)
  instead of predicting delay in days.
- Validate the Random Forest with a train/test split and cross-validation — the current
  model is fit on the full dataset for exploratory feature ranking only.

## Tools

Python, pandas, NumPy, scikit-learn (StandardScaler, RandomForestRegressor),
matplotlib, seaborn, jupyter
