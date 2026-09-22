# Claims and limitations

## Claim hierarchy

| Claim | Current status |
|---|---|
| Sparse allocation improves the risk-adjusted profile of 10Y timing | supported |
| G1 adds incremental return beyond the parent 10Y timing rule | supported; alpha ~0.97% p.a., NW t ~2.91 |
| G1 adds alpha beyond the full static eligible-tenor span | positive / suggestive; NW t ~1.61 |
| G1 adds alpha beyond fixed Level/Slope/Curvature exposures | positive / suggestive; NW t ~1.67 |
| G3 survives the stricter tenor and L/S/C spans | supported at roughly 2-sigma, but with higher turnover |
| Conditional DV01 risk is competitive with generic return volatility | supported |
| Tail-risk-based sparse allocation leads to similar conclusions | supported |
| Strategy is duration-neutral curve relative value | not claimed |

## Limitations

- The strategy is a research backtest, not a production portfolio.
- Treasury ETF OHLC spreads proxy implementation costs; they are not direct execution quotes for all tenors.
- Public macro and market series can be revised.
- The main result is U.S.-curve based; cross-market replication is not yet part of this repository.
- G1 alpha versus the eligible-tenor and L/S/C spans does not cross a conventional 5% significance threshold.
- Multiple closely related controlled variants are shown for mechanism and robustness; the project should not be interpreted as an unrestricted strategy search.
