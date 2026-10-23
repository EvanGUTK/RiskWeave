# RiskWeave — product specification

## Intended outcome

Build an OCaml decision core that validates policy bundles, evaluates typed order intents against a versioned portfolio snapshot, atomically reserves exposure, and emits an inspectable decision trace. Keep the mathematical decision layer independent from broker-specific order routing.

## Primary users and jobs

| User | Job | Successful outcome |
| --- | --- | --- |
| Execution engineer | Enforce policy before routing | Receive an auditable accept or reject and a valid reservation |
| Risk reviewer | Understand policy changes | Inspect which scenarios change and the triggering rule |
| Strategy researcher | Investigate blocked intents | See the exact state and calculation without broker access |

## First journey

A simulated account holds 70 units of exposure under a 100-unit limit. Two incoming orders each request 20 more units. The first accepted request reserves 20; the second sees the reservation and is rejected. The operator expands the trace to inspect the position, outstanding exposure, policy version, and arithmetic. A later cancellation releases capacity only when the execution client establishes the corresponding external order state.

## Functional requirements

| ID | Requirement | Acceptance evidence |
| --- | --- | --- |
| FR-01 | Compile policies before activation | Invalid units and inconsistent bounds cannot activate |
| FR-02 | Reserve with revision control | Concurrent-order fixture admits only permitted combined exposure |
| FR-03 | Keep unknown outcomes pending | Transport timeout cannot free possible live exposure |
| FR-04 | Deduplicate external lifecycle events | Repeated fill or cancellation leaves state unchanged |
| FR-05 | Pin policy and context identity | Every trace names exact policy and input revisions |
| FR-06 | Support offline policy comparison | A fixture produces a complete changed-decision report |

## Scope and product constraints

Single-account spot trading, instrument permissions, order-notional and position limits, outstanding-order reservations, stale-market-data rejection, idempotent lifecycle handling, a policy-difference report, and synthetic property scenarios.

No brokerage routing inside the core, regulatory certification, options portfolio margin, cross-venue netting, derivatives liquidation modeling, or claims of mathematically complete financial safety. Complex valuation and multi-currency conversion require separately specified sources and freshness rules.

## Product quality requirements

Every visible result identifies its source version and completeness. Repeating an action cannot silently create duplicate domain effects. Invalid input produces an actionable diagnostic tied to the field or event that failed validation. Long operations report progress and cancellation boundaries. A cancelled or interrupted operation is visibly different from a completed one.

The initial deployment is a single-user local workflow. Collaboration, tenancy, mobile apps, hosted services, billing, and distributed orchestration are separate scope decisions. An interface proposal must explain the user task it supports before adding new screens or infrastructure.

## Success and non-success

Under the supported spot model, generated accepted-order sequences must respect configured exposure bounds including reservations. A crash-and-replay fixture must reconstruct the same accepted policy state. Pure evaluation is deterministic for the same explicitly supplied context.

Repository stars, document length, and interface polish do not substitute for the domain acceptance criteria. A result that cannot be explained or reproduced remains provisional. Scope expansion is deferred until the first complete scenario can be demonstrated and reviewed.

## Open product decisions

- What precise long-only spot exposure model is sufficient for the first consumer?
- Which context sources and freshness bounds are authoritative?
- What local process and SQLite bindings meet the required support and performance needs?
