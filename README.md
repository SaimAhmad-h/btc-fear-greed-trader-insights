# Bitcoin Market Sentiment vs Trader Performance Analysis

> Exploring the relationship between the Fear & Greed Index and Hyperliquid trader behavior across 211,000+ trades.

---



---

## 📊 Datasets

### 1. Bitcoin Fear & Greed Index
| Column | Description |
|---|---|
| `date` | Date of sentiment reading |
| `value` | Numeric score (0–100) |
| `classification` | Extreme Fear / Fear / Neutral / Greed / Extreme Greed |

### 2. Hyperliquid Historical Trader Data
| Column | Description |
|---|---|
| `Account` | Trader wallet address |
| `Coin` | Traded asset (246 unique coins) |
| `Execution Price` | Price at trade execution |
| `Size Tokens / Size USD` | Trade size |
| `Side` | BUY or SELL |
| `Direction` | Open Long, Close Long, Open Short, Close Short, etc. |
| `Timestamp IST` | Trade timestamp (IST timezone) |
| `Closed PnL` | Realized profit/loss (non-zero on closing trades) |
| `Fee` | Trading fee paid |

---

## 🔍 Notebook Walkthrough

| Cell | Title | What it does |
|---|---|---|
| 1 | Imports | Loads all libraries |
| 2 | Load Data | Reads both CSVs |
| 3 | Clean Trades | Parses dates, coerces numerics, handles nulls |
| 4 | Clean Fear/Greed | Normalizes dates, creates ordered category |
| 5 | Merge | Joins on date; 211,218 / 211,224 rows matched |
| 6 | Volume by Sentiment | Boxplots of daily trade count and USD volume |
| 7 | PnL Distributions | KDE curves per sentiment class (clipped ±500 USD) |
| 8 | Win Rate | % profitable closing trades by sentiment |
| 9 | Mean vs Median PnL | Grouped bar chart per sentiment |
| 10 | Long/Short Bias | % long-side trades by sentiment |
| 11 | Trader Correlation | Per-trader Pearson r between daily PnL and F&G value |
| 12 | Sentiment × Side Heatmap | Avg PnL across sentiment and trade direction |
| 13 | Time-Series Overlay | Rolling 7-day PnL vs F&G index over time |
| 14 | ANOVA Test | Tests whether sentiment significantly affects PnL |
| 15 | Summary Table | Win rate, mean/median PnL, total PnL per sentiment class |

---

## 💡 Key Findings

- **Extreme Greed** produces the highest mean PnL per closing trade (~$130), followed by **Fear** (~$113)
- **Win rates** are highest during **Fear** and **Extreme Greed** periods; lowest during **Neutral**
- Traders open **68.8% long** during Extreme Fear but only **42.3% long** during Greed — a classic contrarian pattern
- **Close Short** win rate drops sharply during Greed (68.9%) compared to Fear (86.2%), suggesting shorting is riskier in bull sentiment
- One-way ANOVA confirms sentiment class has a **statistically significant effect** on per-trade PnL

---

## ⚙️ Setup & Usage

### Requirements
```
pandas
numpy
matplotlib
seaborn
scipy
```

### Install
```bash
pip install pandas numpy matplotlib seaborn scipy
```

### Run
```bash
jupyter notebook analysis.ipynb
```

Or open directly in **Google Colab** and upload both CSV files when prompted.

---

## 📌 Notes

- Only closing trades (`Closed PnL != 0`) are used for win rate and PnL analysis — ~104,000 of 211,000 rows
- Trader correlation analysis (Cell 11) uses a minimum of **5 active days** given the dataset has only 32 unique traders
- Timestamps are in IST; date matching with the Fear/Greed index (UTC dates) may have minor off-by-one effects on late-night trades

---

## 🗂️ Data Sources

- Fear & Greed Index: [alternative.me](https://alternative.me/crypto/fear-and-greed-index/)
- Trader Data: [Hyperliquid](https://hyperliquid.xyz/) via provided dataset
