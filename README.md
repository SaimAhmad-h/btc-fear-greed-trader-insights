# Crypto Trader Sentiment Analysis
### Do traders perform better during Fear or Greed?

---

## Overview

This project analyses **211,224 on-chain trades** from **32 traders** over a 2-year period (May 2023 – May 2025), cross-referenced with the daily **Fear & Greed Index** to measure how market sentiment influences trading behaviour and profitability.

---

## Datasets

| File | Rows | Description |
|---|---|---|
| `historical_data.csv` | 211,224 | On-chain trade records (price, size, PnL, side, timestamp) |
| `fear_greed_index.csv` | 2,644 | Daily Fear & Greed value + classification |

---

## What the Analysis Covers

**Cell 6 — Trade Activity by Sentiment**
Daily trade count and USD volume broken down by sentiment class (boxplots).

**Cell 7 — PnL Distribution**
KDE curves of closed PnL per sentiment class, clipped to ±500 USD to reduce outlier distortion.

**Cell 8 — Win Rate by Sentiment**
Percentage of profitable closing trades per sentiment class with trade counts.

**Cell 9 — Mean vs Median PnL**
Compares average and median closed PnL per trade across sentiment classes.

**Cell 10 — Long/Short Bias**
Proportion of BUY vs SELL trades per sentiment class.

**Cell 11 — Per-Trader Correlation**
Pearson r between each trader's daily PnL and the Fear & Greed value (traders with ≥ 30 active days only).

**Cell 12 — Heatmap**
Average closed PnL broken down by sentiment × trade side (BUY/SELL).

**Cell 13 — Time-Series Overlay**
7-day rolling aggregate PnL plotted against the Fear & Greed index over the full 2-year window.

**Cell 14 — ANOVA Test**
One-way ANOVA testing whether sentiment class significantly affects per-trade PnL.

**Cell 15 — Summary Table**
Final consolidated stats per sentiment class.

---

## Key Results

| Sentiment | Trades | Win Rate | Mean PnL | Total PnL |
|---|---|---|---|---|
| Extreme Fear | 10,406 | 76.2% | $71.03 | $739,110 |
| Fear | 29,808 | 87.3% | $112.63 | $3,357,155 |
| Neutral | 18,159 | 82.4% | $71.20 | $1,292,921 |
| Greed | 25,176 | 76.9% | $85.40 | $2,150,129 |
| Extreme Greed | 20,853 | 89.2% | $130.21 | $2,715,171 |

**ANOVA result:** F = 7.738, p = 3.14e-06 — the difference in PnL across sentiment classes is statistically significant.

**Correlation finding:** Mean Pearson r across qualified traders = 0.148, suggesting a weak positive relationship between higher Fear & Greed values and daily PnL.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
```

Install with:
```bash
pip install pandas numpy matplotlib seaborn scipy
```

---

## How to Run

1. Place `historical_data.csv` and `fear_greed_index.csv` in your working directory
2. Update the file paths in Cell 2
3. Run all cells top to bottom

---

## Notes

- Trades with `closed_pnl == 0` are excluded from win rate, PnL distribution, and correlation analysis (they represent open or fee-only records)
- Fear & Greed data goes back to 2018 but trades only start May 2023 — unmatched dates are dropped
- Per-trader correlation requires ≥ 30 active trading days to qualify
- PnL in Cell 7 is clipped to ±500 USD for visualisation clarity only; raw values are used in all statistical calculations
