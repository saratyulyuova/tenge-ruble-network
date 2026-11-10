Day 1 - Mantegna (1999)
Citation: Mantegna, R. N. (1999). Hierarchical structure in financial markets. European Physical Journal B, 11, 193–197.
 (I read the arXiv preprint from 1998. It uses a different distance, d = 1 − ρ². The journal version uses d = √(2(1 − ρ)).)
1. What problem does the paper solve?
 Stock prices look random, but do stocks move on their own, or do some of them move together because of common factors (like oil prices or the economy)? Mantegna wants to find groups of stocks using only their price data. Then he checks if these groups match real industries.
2. Which data did he use (assets, period, frequency)?
Assets: 30 Dow Jones stocks, and 443 S&P 500 stocks (only the ones that were in the index for the whole period).
Period: July 1989 – October 1995.
Frequency: daily closing prices. He uses daily log returns: Y = ln P(t) − ln P(t−1).
3. Why d = √(2(1 − ρ)) and not just (1 − ρ)? What are the 3 metric axioms?
 A distance must follow 3 rules:
The distance is 0 only between a stock and itself.
The distance from A to B is the same as from B to A.
Triangle rule: going straight from A to B is never longer than going A → C → B.
1 − ρ can break rule 3, so it is not a real distance. √(2(1 − ρ)) is the normal straight-line distance between two (standardized) return series, so all 3 rules always work. It goes from 0 (ρ = 1, same movement) to 2 (ρ = −1, opposite movement).
4. What does the MST show that the correlation matrix alone does not?
The matrix for 443 stocks has about 98,000 numbers. Nobody can read that. The MST keeps only 442 links, the most important ones.
In the MST you can see groups of stocks, and they match real sectors: oil, banks, electricity, telecom, gold.
The tree shows how strongly a group is connected to the rest of the market. If a group joins the rest very late (high distance), it is driven by its own factor. Example: gold companies follow the price of gold, not the market.
Sometimes the tree splits companies that the official classification puts together. Example: gold companies are far from aluminium and copper companies.
5. What is ONE idea I will use in my project?
 I will take daily log returns, compute correlations, turn them into distances with √(2(1 − ρ)), and build an MST. Then I will check if the groups make sense, for example whether KZT is close to RUB or to oil-linked currencies.
6. Words / steps I did not understand:
MST (minimum spanning tree): connects all stocks with the fewest and shortest links, with no loops.
Subdominant ultrametric: the distance between two stocks in the tree = the longest link on the path between them. This is used to draw the hierarchical tree.
Dendrogram: the tree picture. The lower two stocks join, the more similar they are.
APT (Arbitrage Pricing Theory): the idea that stock returns depend on several common factors.

## Day 2 — data download and cleaning
- Downloaded daily closes for 26 currencies, gold and 3 factors (Brent, DXY, VIX) from Yahoo Finance, Aug 2015 – Sep 2026 (2,909 days). Flipped EUR and AUD to "units per 1 USD".
- Missing values ~0.1% for all currencies (3.5% for gold, US holidays). No currency was frozen (highest no-change share: UZS 8.4%).
- Excluded KGS (no data) and UZS (not market-determined before the 2017 liberalisation). Final sample: 24 currencies + gold.
- Yahoo data contain one-day spikes that reverse the next day (e.g. NOK on 1 Jan 2021, when the market is closed). Rule: a >10% daily move almost fully reversed the next day = data error, replaced by the previous value. 15 days removed.
- Large moves that do not reverse were kept as real events: RUB March 2022, TRY Aug 2018, Mar 2021, Nov–Dec 2021.

## Day 3 — verification against official central-bank rates
- KZT from the National Bank of Kazakhstan (every Wednesday), RUB from the Bank of Russia.
- RUB: correlation of weekly returns with Yahoo 0.82. After shifting the official rate one business day back (it is set the day before), 0.96 before 2022 but only 0.89 after → the ruble market fragmented after the sanctions. The 2022-07-06 jump exists only in Yahoo.
- KZT: 0.935; shifting makes it worse, so the NBK rate is dated correctly. Yahoo is ~0.5% below official and shows a ~3.5% gap from mid-2026.
- Decision: official rates for KZT and RUB, Yahoo for the other 22 currencies.

## Day 4 — weekly returns
- 578 weekly (Wednesday) log returns, 24 currencies. Sign check passed: KZT, RUB, NOK, CAD correlate positively with oil and negatively with DXY; JPY and CHF positively with VIX.
- KZT is more correlated with oil than RUB (0.26 vs 0.14). KZT and RUB are weakly linked to DXY (−0.16, −0.18) compared with NOK (−0.57).
- RUB is the most volatile currency (~21% per year). KZT: excess kurtosis ~17, skewness ~−2.5 (rare sharp devaluation-type weeks).

## Day 5 — trees and hypothesis test (analysis.ipynb)
- The ruble is the tenge's nearest neighbour in the minimum spanning tree both before and after 24 Feb 2022. Correlation 0.417 → 0.393.
- Block bootstrap (5,000 resamples, 8-week blocks): raw Δd = +0.022, 95% CI [−0.044, +0.473]; after oil, DXY, VIX Δd = −0.072, 95% CI [−0.123, +0.358]. Both contain zero → no significant change.
- The ruble's own position changed: neighbours CAD → HUF, TRY; betweenness 0.087 → 0.170. Mean edge length 0.906 → 0.869.
- Bootstrap intervals are skewed because the correlation depends on a few extreme weeks; the conclusion uses the interval, not the p-value.
