# Consumer-Signaling-Analysis
Consumer-driven market regime model using discretionary vs staples sector performance to dynamically allocate portfolio risk. 
(This project was developed a few months ago, but its official release was postponed due to exam commitments.)

# Consumer-Driven Macro Signal

## Overview

This project investigates whether consumer spending behaviour can act as a leading indicator of market regimes.

The model uses the relative performance of:

- XLY (Consumer Discretionary ETF)
- XLP (Consumer Staples ETF)

to construct a consumer confidence signal. The intuition is that when consumers are spending on discretionary goods rather than necessities, economic conditions are generally stronger and equity markets tend to perform better.

The signal is then used to dynamically allocate between equities and defensive assets.

---

## Economic Motivation

Consumer behaviour often changes before broader economic data is released.

When consumers feel confident, discretionary spending tends to rise relative to essential spending. Conversely, when economic conditions deteriorate, spending shifts toward staples.

The model assumes that the relative performance of discretionary and staples sectors captures these shifts in behaviour and can therefore provide information about future market conditions.

---

## Methodology

### Step 1: Construct Consumer Signal

Calculate the relative strength of consumer discretionary versus consumer staples:

Consumer Signal = XLY / XLP

### Step 2: Smooth the Signal

Apply a 3-month rolling average to reduce short-term market noise.

### Step 3: Standardise

Convert the signal into a rolling z-score using a 12-month lookback window.

### Step 4: Classify Market Regime

| Signal | Regime |
|----------|----------|
| Z > 0 | Risk-On |
| Z ≤ 0 | Risk-Off |

### Step 5: Portfolio Allocation

| Regime | Allocation |
|----------|----------|
| Risk-On | 100% SPY |
| Risk-Off | 50% SPY / 30% AGG / 20% GLD |

Portfolio weights are rebalanced monthly.

---

## Results

### Performance Summary

| Metric | Strategy | Buy & Hold SPY |
|----------|----------|----------|
| Annualised Return | 16.47% | 15.37% |
| Annualised Volatility | 11.76% | 15.10% |
| Sharpe Ratio | 0.94 | 0.70 |
| Maximum Drawdown | -17.70% | -23.93% |
| Daily VaR (95%) | -4.10% | -6.88% |

### Key Findings

- Annual returns modestly exceeded a passive SPY benchmark.
- Portfolio volatility was reduced by approximately 22%.
- Maximum drawdown improved by over 6 percentage points.
- Risk-adjusted performance improved significantly, with the Sharpe Ratio increasing from 0.70 to 0.94.
- Strong consumer signals were associated with stronger forward equity returns.

The results suggest that consumer spending behaviour may contain useful information about broader market conditions and can improve portfolio risk management when used as a regime filter.

---

## Dashboard

![Consumer Signal Analysis](output/consumer_signal_analysis.png)

---

## Practical Application

The signal is designed as a market regime indicator rather than a market timing tool.

| Z-Score | Interpretation |
|----------|----------|
| > +1 | Strong Risk-On |
| 0 to +1 | Mild Risk-On |
| -1 to 0 | Mild Risk-Off |
| < -1 | Strong Risk-Off |

Potential applications include:

- Adjusting equity exposure based on economic conditions.
- Supporting tactical asset allocation decisions.
- Complementing existing macroeconomic indicators.
- Improving downside risk management during weaker consumer environments.

---

## Limitations

- XLY and XLP are market-based proxies rather than direct measures of consumer spending.
- The sample period begins in 2015 and does not cover multiple full economic cycles.
- The model assumes bonds and gold provide defensive diversification.
- Transaction costs and taxes are excluded.
- Structural changes in consumer behaviour may weaken predictive power over time.

---

## Future Improvements

Potential extensions include:

- Replacing ETF proxies with FRED retail sales data.
- Introducing a neutral regime rather than binary classification.
- Incorporating credit spreads as a second macro signal.
- Adding a VIX-based volatility overlay.
- Conducting walk-forward out-of-sample testing.
- Testing sector-specific predictive power.

---

## Technologies Used

- Python
- NumPy
- Matplotlib
- yFinance

---

## Repository Structure

```text
Consumer_Retaildata_py/
│
├── consumer_signal.py
│
└── output/
    ├── consumer_signal_analysis.png
    └── assumptions_and_macro.png
```

## Author

Economics undergraduate interested in macroeconomics, quantitative investing, and systematic portfolio construction.
