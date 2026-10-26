# Transaction-cost treatment

Constant-maturity Treasury series do not contain executable bid/ask quotes. The current implementation therefore uses a practical market-data proxy rather than pretending the research data are tradeable instruments.

## Dynamic proxy

The headline cost layer:

- maps curve exposures to liquid Treasury ETF proxies;
- estimates Corwin-Schultz high-low spreads from ETF OHLC data;
- uses half of the estimated full spread as a one-way trading-cost proxy;
- lags the cost estimates to avoid look-ahead;
- applies costs tenor by tenor to changes in portfolio weights.

## Sensitivity checks

Fixed one-way bps assumptions are retained as stress/sensitivity cases. They are useful precisely because the empirical ETF spread proxy can be very small for liquid Treasury exposures.

## Interpretation

These costs are **implementation diagnostics**, not executable Treasury or futures quotes. A production implementation would need instrument-specific bid/ask, contract rolls, financing/margin, market impact and capacity analysis.
