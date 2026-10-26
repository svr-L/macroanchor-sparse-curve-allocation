# Roadmap

The project is already strong enough to stand alone. The next work should therefore focus on **falsification and stability**, not strategy proliferation.

## Highest-priority next test

### Spanning-alpha stability

For G1 and G3, report parent-signal, tenor-span and Level/Slope/Curvature alpha through:

- economically meaningful subperiods;
- rolling or expanding windows;
- crisis/regime slices where sufficient observations exist.

The aim is to determine whether the incremental alpha is persistent or concentrated in one episode.

## Secondary robustness

- alternative sensible cost assumptions / implementation instruments;
- modest variations of the risk-estimation lookback;
- a frozen-specification rerun with no new strategy search;
- eventual cross-market replication if comparable tenor data and implementation proxies are available.

## What not to add by default

- more ad-hoc sparse objectives;
- a joint `10Y timing + tenor returns` spanning regression unless there is a clear research reason;
- duration-neutral claims inside this repository (those belong to the separate RV project).
