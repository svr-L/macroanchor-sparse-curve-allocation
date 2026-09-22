# Methodology

## 1. Research question

The project asks whether macro-anchored bond-risk-premium forecasts can be converted into an **interpretable sparse allocation across Treasury maturities** that improves on a simple 10Y timing rule.

The allocator is not designed to be market neutral. Duration exposure is permitted when compensated by expected return.

## 2. Opportunity set

Eligible traded tenors are 2Y, 3Y, 5Y, 7Y and 10Y. The curve data layer also uses the 1Y point for interpolation/return construction. The current executed run spans 1976-06 through 2026-05; the evaluation tables contain 470 monthly observations after burn-in and forecast-horizon requirements.

## 3. Macro anchor and term-premium forecasts

The macro anchor is built as a slow-moving short-rate central tendency using trend inflation and a neutral-real-rate proxy. The short-rate process is estimated under the physical measure and used to construct model-implied pure-expectations yields. The observed-minus-model wedge forms a term-premium signal by tenor.

The portfolio layer uses the resulting cross-tenor expected-excess-return surface. The key separation is:

1. **signal formation** comes from the parent macro-anchor research;
2. **portfolio construction** determines how the forecast surface is translated into exposures.

## 4. Sparse greedy allocation

At each rebalance date:

1. rank eligible tenors by forecast expected excess return;
2. choose the strongest pure-return tenor as the core;
3. consider additional tenor exposures on a discrete grid;
4. accept a satellite only if it improves the selected risk-adjusted objective by at least the implementation hurdle;
5. preserve a minimum fraction of the core expected return;
6. enforce gross-exposure constraints.

The main risk objectives are:

- **G1:** conditional return-volatility risk;
- **G2:** conditional DV01 / yield-shock risk;
- **G3:** core exposure plus a short DV01 hedge;
- **G4:** rolling tail expected shortfall.

## 5. Implementation controls

V3/V4 introduce controls intended to reduce turnover and make the greedy allocation economically implementable:

- weight smoothing;
- no-trade bands;
- quarterly rebalance variants;
- explicit implementation hurdles;
- dynamic transaction-cost estimates.

## 6. Statistical evaluation

Strategy means are evaluated using Newey-West/HAC inference with 12 monthly lags.

V4 adds three spanning regressions:

### Parent-signal spanning

`Sparse return ~ constant + 10Y timing return`

This asks whether the portfolio-construction layer adds return beyond the simplest implementation of the same macro-anchor signal.

### Eligible-tenor spanning

`Sparse return ~ constant + 2Y + 3Y + 5Y + 7Y + 10Y excess returns`

This asks whether dynamic sparse allocation can be replicated by a **static linear combination of the same assets available to the allocator**. The standardized-regressor condition number is reported because Treasury tenor returns are collinear.

### Curve-factor spanning

`Sparse return ~ constant + Level + Slope + Curvature factor returns`

Level/Slope/Curvature factor-mimicking portfolios are estimated once using only the pre-evaluation yield-change sample and then frozen. This avoids using evaluation-period information to define the factors.

The deliberately omitted specification is the joint `10Y timing + tenor returns` regression; it is not part of the current test suite.
