# Data sources

Note: `raw_prices.csv` is the Yahoo Finance data **after** spike cleaning and exclusions (not the raw download). `factors.csv` holds Brent, DXY and VIX daily closes.

## Yahoo Finance

- Exchange rates, gold (GC=F), Brent (BZ=F), DXY (DX-Y.NYB), VIX (^VIX): Yahoo Finance via `yfinance`, daily close.
- Downloaded on: 2026-10-14
- Period: 2015-08-01 – 2026-09-30 (study period starts 2015-09-01, after the tenge free float on 2015-08-20)
- EUR and AUD inverted to units per 1 USD.
- Cleaning: one-day spikes (>10%) that reverse the next day were treated as data errors and replaced by the previous value (15 days removed).

## Excluded currencies
| Currency | Reason |
|---|---|
| KGS | No data on Yahoo Finance (ticker not found) |
| UZS | Rate not market-determined before the September 2017 liberalisation |

## Official rates (used for KZT and RUB in the analysis)
- KZT: National Bank of Kazakhstan official (market) rate, nationalbank.kz RSS service (`get_rates.cfm`), every Wednesday, 575 dates, 0 failures.
- RUB: Bank of Russia official rate, cbr.ru XML service (code R01235). The Bank of Russia sets the rate for day X on the previous business day, so dates are shifted one business day back.
- Both are downloaded directly inside `analysis.ipynb`, so the analysis is fully reproducible.

## Verification: Yahoo Finance vs official rates (weekly returns)
| | KZT | RUB |
|---|---|---|
| Mean abs. level difference | 0.61% | 0.64% |
| Weekly-return correlation | 0.935 | 0.817 |
| Correlation, official shifted 1 business day back | 0.905 (worse) | 0.922 |
| — before Feb 2022 (shifted) | 0.909 | 0.960 |
| — after Feb 2022 (shifted) | 0.867 | 0.890 |

Decision rule (set before seeing the results): keep Yahoo if the correlation is above 0.95, otherwise use the official rate. Both KZT and RUB use official rates. Yahoo showed a spurious ruble jump on 2022-07-06 and an unexplained ~3.5% gap in the tenge from about June 2026.

## Not verified
- Single large moves kept as real: CLP 2022-07-21, GOLD 2026-01-30.
