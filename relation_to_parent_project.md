# Methodology

This repository converts macro-anchored bond-risk-premium forecasts into sparse portfolios along the Treasury curve.

## Signal input

The signal is inherited from the parent MacroAnchor project: a macro-consistent short-rate central tendency is embedded in an affine/short-rate framework, and the wedge between observed yields and model-implied pure-expectations yields is interpreted as a term-premium signal by tenor.

## Portfolio-construction problem

The allocation problem is not framed as market-neutral relative value. It is framed as sparse tenor allocation:

1. rank tenors by expected excess return;
2. select the best expected-return tenor as the core;
3. test whether additional tenors improve a risk-adjusted objective;
4. accept incremental legs only if the marginal improvement clears risk and implementation hurdles.

This mirrors the sparse/greedy design pattern used in sparse strategic allocation: start from the strongest standalone exposure and add only exposures with a clear marginal role.

## Risk models

The V3 notebook compares three risk controls:

- conditional return volatility;
- conditional DV01/yield-shock risk;
- rolling tail ES.

The key methodological result is that the rates-native DV01/yield-shock risk version is competitive with generic return-volatility scaling.

## Implementation controls

V3 introduces:

- smoothing/no-trade bands;
- quarterly rebalance variants;
- cost hurdles;
- dynamic transaction-cost estimates;
- fixed-bps transaction-cost checks.

The main conclusion is driven by cost-aware, lower-turnover variants rather than raw monthly switching.
