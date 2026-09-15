# T1 Project Plan

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes:

- `SPY` — US equities
- `TLT` — long-term US Treasury bonds
- `GLD` — gold

The plan starts with this written document; later tutorials will use the same repository to design a bounded analysis task and organize a verifiable agent workflow.

## Available Data

`data/etf_snapshot.csv` contains one row per illustrative ETF with the following columns (see `data/data_dictionary.md`):

| Column | Meaning |
|---|---|
| `ticker` | Short identifier for the illustrative ETF |
| `asset_class` | Broad type of asset represented by the ETF |
| `expected_return_pct` | Illustrative annual return assumption (percent per year) |
| `volatility_pct` | Illustrative annual variability assumption (percent per year) |
| `max_drawdown_pct` | Illustrative largest peak-to-trough loss (percent; negative values represent losses) |
| `expense_ratio_pct` | Illustrative annual fund fee as a percentage of invested assets |

Rows: SPY (US Equity), TLT (Long-Term US Treasury), GLD (Gold).

The dataset is synthetic teaching data. It is deliberately small and fixed, so no download or data-cleaning step is required during the tutorials.

## Expected Final Deliverable

The expected final deliverable is a concise comparison of the three ETFs based on the snapshot metrics, produced by a reproducible and verifiable analysis workflow. The exact form of the analysis output will be defined in a later task; this T1 deliverable is the written project plan itself.

## Three Project Milestones

1. **T1 — Project setup and plan**: Read the repository overview, data dictionary, and snapshot; write this project plan (`artifacts/t1/project-plan.md`) and save it with Git.
2. **Analysis task design**: Define a bounded analysis question for SPY, TLT, and GLD using the snapshot metrics and specify the expected output.
3. **Verifiable agent workflow**: Organize and run the analysis as an agent workflow, then verify that the results match the task specification.

## One Data Limitation

All numeric values in `etf_snapshot.csv` are synthetic teaching assumptions, not live or historical market observations. They are not current quotations, verified historical estimates, or forecasts, and the dataset omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints. The data must not be used as investment advice or as the basis for a real investment decision.

## Next Action

Review this project plan, then save it with Git. No Git commands that change files, commits, branches, or remotes were run while creating this document.
