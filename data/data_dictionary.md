# ETF Snapshot Data Dictionary

`etf_snapshot.csv` contains one row for each illustrative exchange-traded fund (ETF). The dataset is deliberately small and fixed so no download or data-cleaning step is required during the tutorials.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `ticker` | Text | — | Short identifier used for the illustrative ETF |
| `asset_class` | Text | — | Broad type of asset represented by the ETF |
| `expected_return_pct` | Number | Percent per year | Illustrative annual return assumption |
| `volatility_pct` | Number | Percent per year | Illustrative annual variability assumption; a larger value indicates more uncertainty |
| `max_drawdown_pct` | Number | Percent | Illustrative largest peak-to-trough loss; negative values represent losses |
| `expense_ratio_pct` | Number | Percent per year | Illustrative annual fund fee as a percentage of invested assets |

## Important Limitation

All numeric values are synthetic teaching assumptions. They are not current quotations, verified historical estimates, or forecasts. The dataset omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints.
