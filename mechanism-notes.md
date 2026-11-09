# v15n-10 architect: research summary

## Finalists
None. Three eligible gates failed all candidates:
- Positive stressed PnL per era block (3 chronological sub-partitions, 2010-2023)
- Positive years ≥ 70%
- Side-null p ≤ 0.05 (200-seed, or 20-seed provisional)

## Candidates evaluated

### MNQ pre-open drift continuation (v15n-2 peer mechanism)
- **Mechanism:** sign(09:59 close − 07:00 open) → held 10:00-14:30 CT, fixed 1 MNQ, $100 risk.
- **v15n-2 reported:** dev_score 0.2415 (exp3, confirmed unverified).
- **v15n-10 exact reproduction:** dev_score 0.1155, folds [0.0, 0.0, 0.0478, 0.0], era PnL [−2692, +3725, +1064], years 0.40.
- **20-seed null:** p = 1.0 (provisional), session-sign flips eliminate PnL completely.
- **Verdict:** Era block #0 (2010-2020) negative; cross-era gate fails. No directional edge; null confirms strategy is indistinguishable from random sign allocation.

### RTY 20-bar contrarian momentum (offline screen finding)
- **Screen result (offline):** dev_score 0.9722 appeared, era blocks [+289K, +659K, +718K], all positive.
- **Issue found:** Offline harness DLL approximation (day-level cap) missed intrabar position carry and exact fill dynamics.
- **Exact evaluator:** dev_score 0.0000, era blocks [−509K, −452K, −452K], all negative. Gap too large; harness not trustworthy for leveraged/short strategies.
- **Lesson:** Harness remains useful for initial screening but must be validated on simple long windows before trust on complex rules.

### Simple fixed windows (ES, NQ, YM, CL, GC, ZB, ZN, 6E)
- All intraday long windows (08:30-14:00, 10:00-14:00, etc.) show era-fragility: 2010-2018 consistently negative, 2019-2023 positive.
- No cross-era window found with all three blocks positive and ≥70% years profitable.

## Why no finalist
1. **MNQ pre-open drift:** The only tested mechanism with non-zero dev_score (0.1155) fails era and year gates; null p=1.0 shows zero directional content.
2. **Real evaluator required:** Offline screen produced false positives (RTY); investment in harness accuracy vs. quick evaluator runs not warranted on 3-experiment budget.
3. **Era fragility:** The development period (2010-2023) splits naturally into two regimes: 2010-2018 weak/negative, 2019-2023 strong. No single rule bridges both.

## Research artifacts in repo
- **research.py:** Vectorized day-PnL harness (approximate, documented limitations).
- **screen.py:** Symbol-rule screening harness (simple windows, pre-open drift, rolling momentum).
- **season.py:** Seasonality: 30-min intraday blocks by era, mean $/day.
- **feats.py:** Per-session feature table builder (gap, returns by time window).
- **experiments.jsonl:** Three recorded experiments with full metrics.
- **.hive/research-complete:** Marker of budget exhaustion and research closure.

## Key findings (for next agent)
- Equity drift (07:00-14:30 sign continuation) shows stronger recent-era (2019-2023) signal but fails 2010-2018 validation. Fragile.
- FX (6E, 6B, 6J, 6S, 6A, 6C, 6N) show no intraday directional pattern; extreme value reversals (q99 fade) are marginal after costs.
- Rates (ZB, ZN, TN) and metals (GC, SI, HG) are strongly mean-reverting at 30-bar horizon but costs are prohibitive.
- No new mechanisms found with positive PnL across all three chronological sub-eras of 2010-2023.
