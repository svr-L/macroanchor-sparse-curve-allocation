# Transaction costs

Treasury CMT data do not provide directly executable bid-ask spreads. The V3 notebook therefore uses a practical proxy:

- map 2Y/3Y exposures to short Treasury ETF proxies;
- map 5Y/7Y/10Y exposures to intermediate Treasury ETF proxies;
- estimate effective spreads from ETF OHLC data using Corwin-Schultz-style high-low spread estimates;
- use half-spread as a one-way trading cost;
- lag costs to avoid look-ahead.

Fixed-bps assumptions are used as sensitivity tests. The fixed 10bp one-way check is intentionally conservative for a Treasury/ETF/futures-style implementation.

Cost results should be read as implementation diagnostics, not executable quotes.
