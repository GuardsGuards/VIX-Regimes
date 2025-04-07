# 📊 VIX Regimes: Volatility Classification Using GARCH, Entropy, and Persistence

## Overview

This project classifies market volatility into distinct **VIX regimes** using a combination of:

- 📈 **GARCH** — Volatility Clustering  
- 🔀 **Permutation Entropy** — Market Chaos  
- 📐 **Hurst Exponent** — Trend Persistence  
- 🧠 **K-Means Clustering**  
- 🔁 **Markov Chain Transitions**

These indicators are combined into a composite regime index that can be used for market interpretation, forecasting, and strategic portfolio management.

---

## 🧠 Abstract

On **April 4, 2025**, the **VIX spiked to $45**, a nearly **200% increase** within just over a week — coinciding with a $5 trillion market wipeout. As a proxy for expected S&P 500 volatility, the VIX captures broad investor sentiment and fear.

This study applies **unsupervised learning and time-series analysis** to segment VIX behavior into interpretable regimes. Each regime is characterized by:

- Volatility clustering (via **GARCH**)
- Chaos or unpredictability (via **Permutation Entropy**)
- Trend persistence (via **Hurst Exponent**)

Each metric is clustered into discrete bins (0, 1, 2), then concatenated into **composite regime labels** (e.g., `0.0_1.0_2.0`). Transitions and stability are assessed using **Markov chains**. Notably, some less frequent regimes exhibit **high day-to-day persistence**, making them valuable for risk-adjusted strategy design.

---

## 📐 Indicators

| Metric               | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **GARCH(1,1)**        | Measures volatility memory and clustering                                  |
| **Permutation Entropy** | Captures market disorder or unpredictability                                |
| **Hurst Exponent**     | Detects trend-following (>0.5) vs mean-reverting (<0.5) behavior            |

All metrics are tested for **low multicollinearity** (via VIF) and **cointegration** (via Johansen test) to ensure statistical soundness.

---

## 🔬 Methodology

### 📊 Clustering

- **K-Means** is used to bin each indicator into 3 states: low (0), moderate (1), and high (2)
- Composite regimes are formed from the combination of binned indicators

### 🔁 Regime Transition Modeling

- **Markov Chains** track regime persistence and switching probabilities
- Stability scores are computed based on one-day regime retention

---

## 📌 Key Findings

### Dominant Regimes (Price-Based)

| Regime         | Interpretation                                                            | Stability |
|----------------|----------------------------------------------------------------------------|-----------|
| `0.0_1.0_0.0`  | Most stable, calm volatility, moderate entropy, no trend memory           | 0.80      |
| `0.0_1.0_1.0`  | Calm volatility, moderate entropy, mild persistence                       | 0.76      |
| `0.0_1.0_2.0`  | Calm volaility, chaotic memory of past shocks                             | 0.77      |
| `2.0_1.0_0.0`  | High volatility clustering with no historical memory                      | 0.65      |

Most regimes show **GARCH = 0**, indicating that **volatility clustering is typically low** — shocks are short-lived and don't persist.

---

## 📈 Market Implications

### For Traders & Portfolio Managers

- **High GARCH → Persistent risk:** Hedge, reduce exposure
- **High Entropy → Market chaos:** Consider straddles, flexible strategies
- **High Hurst → Trending:** Favor trend-following strategies
- **Low Hurst → Mean-reverting:** Deploy contrarian/mean-reversion strategies

> Use regime transitions (e.g., from `0.0_1.0_0.0` → `0.0_1.0_2.0`) as **early warning signals** of regime shift.

