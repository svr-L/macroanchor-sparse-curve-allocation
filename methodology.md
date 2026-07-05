# Data

Raw data are not committed to the repository.

The notebooks use public yield-curve and rate data where available and may retrieve additional ETF OHLC data for transaction-cost proxies. Cached or downloaded data should be stored locally under `data/raw/` or `data/cache/`, both of which are ignored by Git.

Because public macro and market data can be revised or extended after a research cut, small numerical drifts may occur if notebooks are re-run at a later date.
