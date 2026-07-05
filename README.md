# MacroAnchor Sparse Curve Allocation

Sparse yield-curve allocation using macro-anchored term-premium forecasts.

This repository is a portfolio-construction spin-off of the parent `macro-anchored-bond-risk-premia` research project. The parent project asks whether a macro-consistent short-rate anchor can generate bond-risk-premium forecasts. This repository asks a different question:

> Can those forecasts be converted into sparse, cost-aware tenor portfolios that improve the risk-adjusted profile of duration-risk-premium timing?

The answer from the current evidence is **yes, with the right interpretation**. This is not marketed as duration-neutral curve relative value. It is a sparse tenor-allocation framework: the strategy starts from the tenor with the strongest expected excess return and adds other curve exposures only when they improve the risk-adjusted profile under conditional volatility, DV01/yield-shock risk, or tail-risk criteria.

## Core result

The V3 implementation improves the risk-adjusted profile of a 10Y timing benchmark while keeping turnover materially lower than the raw greedy V2 allocation.

| Strategy | Cost model | Ann. return | Ann. vol | Sharpe | MaxDD | NW t-stat | Ann. turnover | Interpretation |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| 10Y timing benchmark | dynamic TC | 1.51% | 4.78% | 0.32 | -24.03% | 1.74 | 0.69x | benchmark signal applied only to 10Y |
| Sparse core, conditional vol | dynamic TC | 1.81% | 3.09% | 0.59 | -14.68% | 2.64 | 1.62x | headline allocation candidate |
| Sparse core, conditional DV01 | dynamic TC | 1.79% | 3.11% | 0.58 | about -15% | 2.57 | 1.62x | rates-native risk version |
| Sparse core, tail ES | dynamic TC | 1.71% | 2.93% | 0.59 | about -15% | 2.62 | 1.66x | tail-risk version |
| Sparse core, conditional vol | fixed 10bp | 1.65% | 3.09% | 0.54 | -15.26% | n/a | 1.62x | conservative fixed-cost check |

The economic message is not that the sparse portfolio always has the highest absolute return. The message is that it delivers similar or better return than 10Y timing with lower volatility, lower drawdown, and stronger statistical evidence.

## Research design

The allocation is deliberately sparse and interpretable:

1. Estimate macro-anchored term-premium forecasts by tenor.
2. Select the best pure expected-return tenor as the core holding.
3. Add other tenors only if they improve the risk-adjusted objective.
4. Evaluate risk using conditional return volatility, conditional DV01/yield-shock risk, or rolling tail ES.
5. Apply turnover controls, smoothing, quarterly variants, and cost hurdles.
6. Evaluate against static 10Y, equal-weight 2Y-10Y, and 10Y timing benchmarks.

## What this is, and what it is not

This repository is:

- a sparse yield-curve allocation engine;
- a cost-aware extension of a macro-anchored bond-risk-premium signal;
- a portfolio-construction experiment linking forecast strength, conditional risk, and sparse tenor selection.

It is not:

- a fully market-neutral relative-value system;
- a claim that all yield-curve residuals are tradable;
- a production trading system.

For pure duration-neutral curve relative value, see the separate `macroanchor-curve-relative-value` repository.

## Repository structure

```text
macroanchor-sparse-curve-allocation/
├── README.md
├── requirements.txt
├── environment.yml
├── LICENSE
├── CITATION.cff
├── notebooks/
│   ├── 01_cost_aware_sparse_curve_allocation_v3_executed.ipynb
│   └── archive/
│       ├── 00_v2_sparse_greedy_parallel_executed.ipynb
│       └── reference_stress_weighted_sparse_saa.ipynb
├── docs/
│   ├── methodology.md
│   ├── transaction_costs.md
│   ├── relation_to_parent_project.md
│   ├── interpretation_and_claims.md
│   ├── replication_guide.md
│   └── roadmap.md
├── outputs/
│   ├── tables/
│   └── figures/
├── data/
│   └── README.md
└── src/
    └── README.md
```

## Headline figure

![Sparse allocation comparison](outputs/figures/sparse_allocation_headline.png)

## Notebooks

- `01_cost_aware_sparse_curve_allocation_v3_executed.ipynb` is the main notebook.
- `archive/00_v2_sparse_greedy_parallel_executed.ipynb` documents the broader V2 search that separated sparse allocation from pure residual RV.
- `archive/reference_stress_weighted_sparse_saa.ipynb` is included as a reference for the sparse/greedy allocation design pattern. It is not required to run the rates notebook.

## Transaction costs

The V3 notebook uses a dynamic transaction-cost proxy based on Corwin-Schultz ETF-implied half-spreads, with fixed-bps checks as sensitivity tests. Treasury CMT series do not provide executable bid-ask spreads; the cost layer therefore uses liquid Treasury ETF proxies when OHLC data are available, and fixed-bps assumptions as fallback/sensitivity.

## Claim hierarchy

| Claim | Status |
|---|---|
| Macro-anchored term-premium forecasts are useful for duration timing | inherited from parent project |
| Sparse tenor allocation improves the risk-adjusted profile of 10Y timing | supported |
| Conditional DV01/yield-shock risk is competitive with generic return volatility | supported |
| Tail-risk-based sparse allocation gives similar conclusions | supported |
| The strategy is pure curve relative value | not claimed |

## License

MIT License. See `LICENSE`.

## Disclaimer

This repository is for research and educational purposes only. It is not investment advice, not a production trading system, and not a recommendation to trade any instrument.
