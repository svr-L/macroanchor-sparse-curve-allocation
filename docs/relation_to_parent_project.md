# Relation to the parent project

`macro-anchored-bond-risk-premia` is the signal-research parent. It studies whether a macro-consistent short-rate central tendency can generate useful model-implied term-premium forecasts under out-of-sample discipline.

This repository begins **after** those forecasts exist. Its object is portfolio construction:

1. take the cross-tenor expected-return surface;
2. identify the strongest pure-return tenor;
3. add only exposures that improve the risk-adjusted profile;
4. control turnover and implementation costs;
5. test whether the portfolio layer adds incremental return beyond the parent timing implementation and standard curve exposures.

The sibling `macroanchor-curve-relative-value` project asks a different question again: can residual curve richness be isolated after removing duration exposure? That project imposes much stricter neutrality requirements.

Keeping these repositories separate avoids mixing three distinct claims: **predictability**, **allocation**, and **relative value**.
