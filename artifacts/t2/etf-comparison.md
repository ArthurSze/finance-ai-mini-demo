# T2 ETF Comparison — SPY, TLT, GLD: Annual Fees and Historical Maximum Drawdown

This report upgrades the T1 project plan by replacing the synthetic snapshot metrics with the real **T2 ETF Data Pack** (prepared 2026-09-25): SPY, TLT and GLD are compared on disclosed annual expense ratios and maximum drawdowns calculated from 7,536 daily `adjusted_close` observations.

## Source and inputs

- Price input: `data/t2/daily_prices.csv` (7,536 rows, UTF-8)
- Fee input: `data/t2/fund_info.csv`; dictionary: `data/t2/data_dictionary.md`
- Pack preparation date: **2026-09-25**; retained source history recorded as downloaded on 2026-09-20.
- Common drawdown period: **2016-09-01 through 2026-08-31 (inclusive)**, 2,512 daily observations per ETF; daily frequency on US market session dates (America/New_York), no rows on weekends or full-day closures.
- Adjustment basis: `adjusted_close` (Yahoo chart `adjclose`, provider's split and dividend-distribution adjustments); the unadjusted `close` column was retained for inspection but not used.
- Fee disclosure dates (from `fund_info.csv`, accessed on 2026-09-25):
  - **SPY** 0.0945% — fund-information as-of date 2026-09-10; fee-specific effective date **not stated** (gross of waivers/reimbursements).
  - **TLT** 0.15% — current prospectus; specific date **not stated** in the fee panel.
  - **GLD** 0.4% — effective date **not stated** in the selected field.

## Method and execution

- Script: `artifacts/t2/calculate_drawdown.py` (Python 3.12, standard library only).
- Command executed from the repository root: `python artifacts/t2/calculate_drawdown.py`.
- Input checks: **all passed** — exactly SPY/TLT/GLD; 7,536 rows; unique (ticker, date) pairs; dates parse as YYYY-MM-DD; ascending dates within each group; all `close` and `adjusted_close` positive and finite; 2,512 rows per ETF; first/last dates 2016-09-01 / 2026-08-31; date sets identical across tickers; `fund_info.csv` tickers match.
- Calculation: for each ticker, all `adjusted_close` observations sorted ascending, cumulative high from the window start, `drawdown_t = (adjusted_close_t / high_t - 1) * 100`, maximum drawdown = minimum drawdown over the window. Tie rule: earliest trough and its earliest peak on or before the trough. Full precision kept internally; displayed to two decimals.

## 1. Comparison

| Ticker | Annual expense ratio (%) | Maximum drawdown (%) | Peak date | Trough date |
|---|---|---|---|---|
| SPY | 0.0945 | -33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | -48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | -26.40 | 2026-01-29 | 2026-07-16 |

## 2. Observation

The ETF with the smallest drawdown loss (closest to zero) in this period is **GLD (-26.40%)**, followed by SPY (-33.72%) and TLT (-48.35%). At two decimal places there are no ties among the three displayed values. These drawdowns were **calculated from `adjusted_close`** in this window, not read from any precomputed snapshot. Fees are current issuer-disclosed ratios and are **not** ten-year averages over the price window, and each drawdown is a window-specific daily-close measure, **not** an all-time measure. Limitation: drawdowns use daily closing prices only, so intraday losses and drawdowns outside 2016-09-01..2026-08-31 are not captured.

## 3. Agent Check (self-check)

I selected **GLD** and re-verified its reported peak/trough rows directly from `data/t2/daily_prices.csv`.

- Source rows read:
  - `2026-01-29,GLD,close=495.8999938964844,adjusted_close=495.8999938964844`
  - `2026-07-16,GLD,close=364.9599914550781,adjusted_close=364.9599914550781`
- Check command executed: `python -c "import csv; rows=list(csv.DictReader(open('data/t2/daily_prices.csv',newline='',encoding='utf-8'))); sel=[r for r in rows if r['ticker']=='GLD' and r['date'] in ('2026-01-29','2026-07-16')]; [print('row:',r['date'],r['ticker'],'close=',r['close'],'adjusted_close=',r['adjusted_close']) for r in sel]; d={r['date']:float(r['adjusted_close']) for r in sel}; p=d['2026-01-29']; t=d['2026-07-16']; chk=(t/p-1)*100; print('check (trough/peak-1)*100 =',repr(chk)); print('report max drawdown = -26.404518'); print('difference (abs) =',abs(chk-(-26.404518)))"`.
- Actual output: recomputed `(trough / peak - 1) * 100 = -26.404517857029663%`; report internally computed value `-26.404517857029663%`; report display `-26.40%`.
- Comparison: exact match (the ~1.4e-07 absolute difference appears only against the 6-decimal display string; no correction or recheck was needed).
- Inspection: the script processed all 2,512 GLD `adjusted_close` observations with cumulative highs from the window start; peak date (2026-01-29) is on or before trough date (2026-07-16); the earliest-trough / earliest-peak tie rule was applied. Reviewing all three displayed results (-26.40, -33.72, -48.35) confirms GLD is closest to zero with no ties.
- This was my own self-check using local tools; it is not an independent verification, and no student independently checked the data.

---

*Scope note: this comparison is limited to the supplied teaching pack and is not investment advice.*
