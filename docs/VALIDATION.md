# RiskWeave — validation and benchmark plan

This is a proposed validation plan. No runtime results or benchmark numbers are claimed.

## Domain scenario matrix

| Scenario | Expected behavior | Evidence |
| --- | --- | --- |
| Two simultaneous orders | Only valid combined exposure is reserved | Serialized revision trace |
| Duplicate partial fill | Position changes once | Lifecycle identity ledger |
| Cancel-fill race | Filled amount retained; only residual released | Cumulative quantity reference fixture |
| Routing timeout | Reservation remains pending | Unknown-outcome state |
| Stale valuation | Required notional check cannot accept | Reason with source age and threshold |
| Policy activation | Earlier decisions preserve prior bundle | Versioned trace pair |
| Crash after acceptance | Reservation survives restart | Journal replay and reconciliation report |

## Measurement protocol

Measure pure evaluation separately from acceptance transactions, serialization, and client routing. Report rule count, context size, journal mode, concurrency, and conflict rate. Tail latency matters for stateful acceptance; an in-memory rule microbenchmark must not be labeled broker execution latency.

## Reproducibility record

Record source revision, environment and dependency lock, operating system, CPU/GPU where relevant, workload identity, input size, data distribution, random seeds, concurrency, warm-up policy, repetitions, and output digests. Report variability and failures as well as the preferred statistic. Distinguish pure kernel timing from parsing, serialization, storage, network, and UI costs. Comparisons use the same semantics and workload.

## Correctness before speed

Under the supported spot model, generated accepted-order sequences must respect configured exposure bounds including reservations. A crash-and-replay fixture must reconstruct the same accepted policy state. Pure evaluation is deterministic for the same explicitly supplied context.

Use a small independent reference or analytically solved fixture where feasible. A second implementation that copies the same assumptions is not independent evidence of realism. Numerical comparisons define tolerances; discrete identifiers, units, and state transitions require exact agreement. Every discovered defect becomes a minimized regression scenario with its original cause explained.

## Publication rules

Illustrative values must be labeled. A benchmark badge is added only when its method and source artifacts are available. Missing data, incomplete runs, rejected inputs, and failed experiments remain in the evaluation record. No annualized financial performance, behavioral realism, or platform fidelity is inferred from a short convenient sample.
