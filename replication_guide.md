# Relation to the parent MacroAnchor project

The parent repository, `macro-anchored-bond-risk-premia`, establishes the signal and the audit framework:

- macro anchor as short-rate central tendency;
- model-implied term premium by tenor;
- out-of-sample bond-risk-premium prediction;
- G10 and specification-audit diagnostics.

This repository starts after that signal has been created. Its contribution is portfolio construction: how to allocate across curve tenors once the forecasts exist.

The separation is intentional:

- parent project = forecasting and term-premium research;
- this project = sparse portfolio construction along the curve;
- curve-RV project = duration-neutral residual relative value.
