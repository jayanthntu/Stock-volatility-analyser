# Stock-volatility-analyser

**Team Members:** Phua Gu Guang, Jayanth Sandalya Avadhanam Srihari, Kogeshwaran Kalathran

## Project Overview

This project builds a binary volatility classifier to help retail investors identify
when a stock is likely to enter a high-volatility period in the near term. The core
question addressed is:

> *Can historical stock prices, trading activity, market-wide fear indicators,
> macroeconomic signals, and earnings surprises be used to predict near-term
> stock volatility?*

Three stocks representing different volatility regimes are analysed — **AAPL** (stable),
**JNJ** (low volatility), and **TSLA** (high volatility) — covering the period 2021–2025.

## Datasets

| # | Dataset | Source | Role |
|---|---------|--------|------|
| 1 | Daily stock prices (OHLCV) | Yahoo Finance (`yfinance`) | Log returns, rolling volatility |
| 2 | Trading volume & liquidity metrics | Yahoo Finance (`yfinance`) | Abnormal trading pressure |
| 3 | VIX market fear index | FRED | Market-wide systemic risk |
| 4 | 10-Year US Treasury Yield | Kaggle | Macroeconomic interest rate context |
| 5 | Quarterly EPS earnings surprises | Alpha Vantage | Firm-specific event-driven shocks |

## Methodology

1. **ASK** — Define the data science problem and identify required data sources
2. **PREPARE** — Source, profile, and validate all five datasets
3. **PROCESS** — Merge datasets on a common daily date index, engineer features,
   define the binary target variable (top 25% volatility = high, rest = normal),
   and perform a chronological train/test split (2021–2023 train, 2024–2025 test)
4. **ANALYSE** — Train and compare two models:
   - *Logistic Regression* — linear baseline
   - *Random Forest* — main model, evaluated on accuracy, precision, recall, and F1

## Key Results

- Random Forest outperforms Logistic Regression, particularly on recall for the
  high-volatility class — meaning it catches more actual volatility spikes
- Feature importance analysis confirms that recent rolling volatility (DS1) and VIX (DS3)
  are the strongest predictors, validating the dataset selection choices
- The model serves as a **risk awareness tool**: when it flags high volatility, investors
  may consider reducing position size or widening stop-loss levels

## Requirements
```
pip install pandas numpy matplotlib scikit-learn yfinance kagglehub requests
```

## How to Run

Run all cells top to bottom in order. Ensure the Alpha Vantage API key is set in
the DS5 cell before running. VIX data can alternatively be loaded from a locally
saved `VIXCLS.csv` downloaded from [FRED](https://fred.stlouisfed.org/series/VIXCLS).
