# Data sources

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

## To verify on Day 3
- RUB 2022-07-06 jump, compare with the Bank of Russia official rate
- KZT levels, compare with the National Bank of Kazakhstan
