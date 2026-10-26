# Replication guide

## Quick start

```bash
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
jupyter notebook notebooks/01_cost_aware_sparse_curve_allocation_v4_spanning_executed.ipynb
```

Run the notebook top to bottom.

## Data

The notebook retrieves public FRED/Treasury data and uses a local cache. It also attempts to retrieve Treasury ETF OHLC data for the dynamic transaction-cost proxy. If live downloads fail but a cache exists, the notebook can fall back to cached files.

## Expected current sample

The committed executed notebook reports:

- aligned curve sample: 1976-06 through 2026-05;
- evaluation observations after burn-in / horizon requirements: 470 monthly observations.

Public data can be revised or extended. Small differences from the committed output are therefore possible on a fresh run.

## Key outputs

The notebook exports the main research bundle to its configured output directory. The repository also commits clean copies under `outputs/tables/` and `outputs/figures/` so the headline evidence can be inspected without rerunning the notebook.

The most important files are:

- `headline_performance.csv`
- `headline_spanning.csv`
- `spanning_summary_full.csv`
- `spanning_betas_headline.csv`
- `curve_factor_loadings.csv`
- `attribution_dynamic_cost.csv`
