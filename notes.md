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
