# Data

Raw market and macro data are **not redistributed** in this repository.

The main notebook retrieves public U.S. Treasury/FRED series programmatically and caches them locally when possible. The core curve inputs are the 1Y, 2Y, 3Y, 5Y, 7Y and 10Y constant-maturity Treasury yields, the 3-month Treasury bill rate, and CPI. Treasury ETF OHLC data are used only as transaction-cost proxies when available.

Local caches created by the notebook are ignored by Git. Public data can be revised or extended, so a fresh rerun may differ slightly from the executed notebook included in `notebooks/`.
