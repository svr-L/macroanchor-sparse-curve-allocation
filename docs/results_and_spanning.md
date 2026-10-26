# Results and spanning diagnostics

All figures below refer to the executed V4 notebook and the dynamic transaction-cost specification unless stated otherwise.

## Headline performance

| Strategy | Ann. return | Ann. vol | Sharpe | MaxDD | NW t | Turnover |
|---|---:|---:|---:|---:|---:|---:|
| 10Y timing | 1.46% | 4.77% | 0.306 | -25.28% | 1.68 | 0.69x |
| G1 sparse vol + cost hurdle | 1.78% | 3.09% | 0.576 | -14.68% | 2.59 | 1.65x |
| G2 sparse DV01 + cost hurdle | 1.76% | 3.10% | 0.567 | -15.37% | 2.53 | 1.65x |
| G4 tail ES + cost hurdle | 1.68% | 2.92% | 0.575 | -14.68% | 2.57 | 1.68x |
| G3 core + short DV01 + cost hurdle | 2.16% | 3.80% | 0.569 | -13.31% | 2.77 | 3.46x |

The G1 allocator is the headline specification because it combines the highest net Sharpe among the main controlled variants with substantially lower turnover than the G3 short-DV01 challenger.

## G1 spanning results

| Benchmark span | Alpha p.a. | NW t | R² | Condition number |
|---|---:|---:|---:|---:|
| Parent 10Y timing | 0.97% | 2.91 | 72.71% | 1.00 |
| Eligible tenor returns | 0.77% | 1.61 | 56.07% | 32.31 |
| Fixed Level/Slope/Curvature | 0.75% | 1.67 | 56.06% | 13.46 |

The strongest result is the parent-signal spanning test: the headline allocator retains roughly 1% annualized incremental return with a Newey-West t-statistic near 2.9. Against the stricter asset-span and curve-factor benchmarks, residual alpha remains positive but is only suggestive.

## G3 spanning results

| Benchmark span | Alpha p.a. | NW t | R² |
|---|---:|---:|---:|
| Parent 10Y timing | 1.13% | 3.41 | 77.66% |
| Eligible tenor returns | 1.15% | 2.01 | 41.01% |
| Fixed Level/Slope/Curvature | 1.19% | 2.05 | 40.96% |

G3 passes the stricter spans more convincingly, but at annual turnover of roughly 3.46x versus 1.65x for G1. The correct interpretation is therefore **challenger evidence**, not a reason to replace the cleaner headline implementation mechanically.

## Why the spanning tests matter

A better Sharpe ratio alone cannot distinguish between three possibilities:

1. the allocator simply scales down the parent 10Y exposure;
2. it repackages a static combination of curve tenors;
3. the dynamic construction adds incremental value.

The current evidence rejects the first explanation for G1 at conventional significance levels. The stricter static-tenor and Level/Slope/Curvature tests are more demanding: G1 remains positive but borderline, while G3 retains approximately 2-sigma alpha.
