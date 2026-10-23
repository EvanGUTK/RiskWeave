# RiskWeave — pipeline specification

## Stage contracts

| Stage | Input | Output / postcondition | Failure and recovery |
| --- | --- | --- | --- |
| Compile policy | Versioned rule specification | Typed, validated PolicyBundle | Reject missing units, inconsistent bounds, and unknown rule kinds |
| Validate context | Order intent + portfolio revision + market metadata | Normalized evaluation context | Reject stale, missing, or incompatible required inputs |
| Evaluate pure rules | PolicyBundle + evaluation context | Ordered rule outcomes and candidate exposure | Unknown rule result is explicit and blocks required acceptance |
| Reserve atomically | Candidate decision + expected portfolio/reservation revision | Accepted DecisionTrace + reservation, or revision conflict | Retry evaluation on conflict; do not reserve from stale state |
| Route externally | Accepted decision reference | Broker action owned by caller | Unknown external outcome keeps reservation pending reconciliation |
| Apply lifecycle | Deduplicated fills, rejects, cancel confirmations | Updated position and outstanding reservation | Out-of-order events enter reconciliation; never double-release exposure |
| Compare revisions | Recorded scenarios + two policy bundles | Changed-decision report | Incompatible context schema is rejected with explanation |

## Ordering and checkpoints

The journal uses monotonic local revisions and stable external event identities. Lifecycle timestamps are descriptive and cannot override known causal references. Partial fills may race with cancellation acknowledgments; the reducer validates cumulative filled quantity and remaining open quantity before releasing residual exposure. Policy activation establishes a specific revision boundary. Existing reservations retain their original decision references and are reevaluated only under an explicit migration or containment procedure.

## Invariants across stages

- Exposure includes positions and supported outstanding-order reservations under the policy’s valuation rule.
- Price, quantity, notional, and currency conversions are distinct typed dimensions.
- Repeated lifecycle events cannot add a fill or release capacity twice.
- An accepted decision and its reservation are committed atomically.
- A policy revision cannot silently reinterpret an earlier accepted decision.

## Completion protocol

An operation starts by assigning a run identity and fingerprinting its effective configuration. Input validation completes before irreversible domain effects. Intermediate files remain staged and include an incomplete marker. Completed outputs are hashed and referenced by a manifest committed atomically with their accepted status. A crash before publication leaves recoverable intermediate work, not a plausible final report.

Retries identify the prior operation and preserve the original input references. A repair that changes semantics becomes a new revision with an explicit reason. Cancellation is honored at documented boundaries and records the last committed checkpoint. Importers reject incomplete outputs by default; diagnostic tools can inspect them only with an explicit incomplete status.

## Worked scenario

Synthetic sequence: limit 100; existing exposure 70; request A adds 20 at revision 5 and commits reservation revision 6. Request B evaluated at revision 5 conflicts, reevaluates with exposure 90, and rejects because 110 exceeds 100. If A receives a 5-unit fill, supported state becomes position exposure 75 and remaining reservation 15, keeping total 90. A pending cancellation leaves the remaining 15 reserved until confirmed or reconciled.

## Pipeline acceptance gate

The first vertical slice must demonstrate one ordinary case, one malformed input, one duplicate, and one interruption or recovery case. Its output includes input lineage and enough diagnostics to explain failure without reconstructing the operator's shell history. Domain-specific scenarios in [VALIDATION.md](VALIDATION.md) take precedence over generic throughput goals.
