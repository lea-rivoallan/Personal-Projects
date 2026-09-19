# Modeling EUR/CNY Volatility (vs. EUR/USD benchmark)

## Objective
Model and compare the volatility dynamics of EUR/CNY against the EUR/USD
benchmark using a GARCH(1,1) framework, and interpret the results in light
of China's capital controls and partial market integration.

## Data
- **Source:** Investing.com — EUR/CNY and EUR/USD daily historical spot prices
- **Period:** 01/01/2010 – 12/31/2025
- **Frequency:** Daily

Place the two source CSVs in a `data/` folder before running the notebook:
- `data/EUR_CNY_Historical_Data.csv`
- `data/EUR_USD_Historical_Data.csv`

## Method
1. Compute daily log returns for both series
2. Fit a GARCH(1,1) model with a Student-t error distribution to each series
   (returns scaled by x100 for numerical stability, consistently across both
   series so that omega, alpha and beta are directly comparable)
3. Extract and plot conditional volatility
4. Compare persistence (alpha + beta) and tail heaviness (degrees of freedom, ν)
   between the two currency pairs

## Key findings
- EUR/CNY volatility is highly persistent (alpha + beta ≈ 0.995) and
  heavy-tailed (ν ≈ 7.6), consistent with capital controls, partial RMB
  convertibility, and slower information transmission between European and
  Chinese markets
- EUR/USD, as a mature and liquid market, shows sharper but faster-fading
  reactions to macro shocks

## Requirements
```
pandas
numpy
matplotlib
arch
```

## Notes
- This notebook was cleaned up for portability (relative paths, consistent
  return scaling across both series). The EUR/USD conclusion cell still
  quotes figures from an earlier run under a different scale — alpha and
  beta are scale-invariant in a GARCH(1,1) model, so those readings still
  hold, but the notebook should be re-run end-to-end once the source data is
  back in `data/` to refresh the omega value and all plots.
