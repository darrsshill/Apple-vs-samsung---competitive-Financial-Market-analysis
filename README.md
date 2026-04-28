# Apple vs Samsung — Competitive Financial & Market Analysis

A data-driven analysis comparing Apple (AAPL) and Samsung Electronics (005930.KS) across stock performance, financial fundamentals, and macroeconomic sensitivity over the period **January 2015 – April 2026**.

---

## Research Questions

1. How have Apple and Samsung stock prices **performed and correlated** over 2015–2025?
2. How do the two companies compare on **key financial fundamentals** (revenue, profitability, cash flow)?
3. Can **macroeconomic factors** (inflation and interest rates) explain monthly stock return variations?

---

## Project Structure

```
.
├── Data_download.ipynb              # Data collection from Yahoo Finance & FRED
├── Apple_vs_Samsung_Analysis.ipynb  # Full analysis, visualizations, regression
├── Apple_vs_Samsung_Presentation.pptx
│
├── Data (CSV)
│   ├── stock_prices.csv             # Daily OHLCV — Apple & Samsung (2015–2026)
│   ├── apple_income_stmt.csv
│   ├── apple_balance_sheet.csv
│   ├── apple_cash_flow.csv
│   ├── samsung_income_stmt.csv
│   ├── samsung_balance_sheet.csv
│   ├── samsung_cash_flow.csv
│   ├── fred_macro.csv               # CPI + 10Y Treasury (merged)
│   ├── fred_cpi_us.csv
│   └── fred_treasury_10y.csv
│
└── Plots (PNG)
    ├── plot1_normalized_prices.png
    ├── plot2_rolling_correlation.png
    ├── plot3_scatter_annual_corr.png
    ├── plot4_revenue_netincome.png
    ├── plot5_profit_margins.png
    ├── plot6_cashflow.png
    ├── plot7_macro.png
    ├── plot8_regression.png
    ├── plot9_coefficients.png
    ├── plot10_corr_heatmap.png
    └── plot11_volatility.png
```

---

## Data Sources

| # | Source | Method | Coverage | Variables |
|---|--------|--------|----------|-----------|
| 1 | [Yahoo Finance](https://finance.yahoo.com) | `yfinance` | 2015–2026 (daily / annual) | OHLCV prices; Revenue, Net Income, Gross Profit, Operating Income, Free Cash Flow |
| 2 | [FRED — Federal Reserve Bank of St. Louis](https://fred.stlouisfed.org) | `pandas-datareader` | 2015–2026 (monthly / daily) | `CPIAUCSL` — US CPI; `DGS10` — 10-Year Treasury Rate |

**Companies:** Apple Inc. (AAPL, NASDAQ) | Samsung Electronics (005930.KS, KRX)

---

## Key Findings

### RQ1 — Stock Performance & Correlation
- Apple delivered a **~1,016% total return** (annualized: 31.0%) vs Samsung's **~956%** (annualized: 30.5%) over the period.
- Both stocks carry nearly identical annualized volatility (~29–30%) and Sharpe ratios (~1.0).
- Despite being direct product competitors, the **daily return correlation is very low (r = 0.068)**, reflecting different exchange listings, investor bases, and business mix.
- Rolling correlation spikes during broad market stress (e.g., COVID-19 March 2020) but collapses at other times, confirming the relationship is unstable.

### RQ2 — Financial Fundamentals
- **Apple consistently outperforms on profitability**: gross margin ~47% vs Samsung ~37%; net margin ~25% vs ~12%.
- Apple generates ~$100B/year in free cash flow. Samsung's FCF is more volatile, turning negative in 2023 due to heavy semiconductor capex.
- Samsung's revenue and margins are highly sensitive to the **semiconductor cycle** (significant 2023 downturn, strong 2025 recovery).

### RQ3 — Macroeconomic Regression
- OLS models using CPI change and 10Y Treasury yield change explain only **~1.6% (Apple)** and **~2.3% (Samsung)** of monthly return variance — the F-statistics are not significant at the 5% level.
- Coefficient signs are directionally consistent with theory: rising rates carry a negative coefficient for both stocks.
- The bulk of return variation is driven by **firm-specific factors** (earnings surprises, product cycles, geopolitical events) rather than macro variables.

---

## Setup & Installation

```bash
pip install yfinance pandas numpy matplotlib seaborn scikit-learn statsmodels pandas-datareader
```

Run notebooks in order:

```
1. Data_download.ipynb           # downloads and saves all CSV files
2. Apple_vs_Samsung_Analysis.ipynb  # loads CSVs, runs analysis, generates plots
```

> The CSVs are already committed to the repo, so you can run the analysis notebook directly without re-downloading data.

---

## Limitations

- **Currency**: Samsung prices are in KRW; correlation and regression analyses do not adjust for USD/KRW exchange rate movements.
- **Financial history**: Only 4–5 years of annual financial statements are available via `yfinance`.
- **Omitted variables**: The macro regression excludes market beta (S&P 500/KOSPI), earnings momentum, and sector factors.
- **Survivorship bias**: Both companies are industry leaders; results may not generalize to the broader tech sector.

---

## References

1. Yahoo Finance — Apple Inc. (AAPL) & Samsung Electronics (005930.KS)
2. Federal Reserve Bank of St. Louis (FRED) — CPIAUCSL, DGS10
3. McKinney, W. (2010). *Data Structures for Statistical Computing in Python*. SciPy Proceedings.
4. Seabold, S. & Perktold, J. (2010). *Statsmodels: Econometric and Statistical Modeling with Python*. SciPy Proceedings.
