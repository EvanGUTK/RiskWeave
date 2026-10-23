# RiskWeave — data model

## Canonical entities

| Entity | Identity / fields | Lifecycle / invariant |
| --- | --- | --- |
| PolicyBundle | Policy ID, schema version, rules, units, effective revision | Validated before activation; immutable once referenced |
| OrderIntent | Client order identity, instrument, side, quantity, price constraint | New identity required for materially changed request |
| PortfolioSnapshot | Account namespace, positions, balances, valuation time, revision | Freshness and completeness checked per policy |
| DecisionTrace | Decision ID, input hashes, outcomes, arithmetic, policy identity | Accepted/rejected/invalid/conflict distinguished |
| Reservation | Decision ID, outstanding amount, instrument, lifecycle state | Transfers on fills and releases only under supported transitions |
| LifecycleEvent | External event identity, cumulative fill, order state | Idempotent application with reconciliation for inconsistency |

## Domain semantics

The first supported exposure model must be fully specified for long-only spot trading. Gross and net exposure are different rule types. Market orders require an explicit conservative reference or price bound for notional checks; an unavailable bound blocks valuation. Currency conversion requires a source, age, and rounding policy and is deferred if unnecessary. A client cannot label an order “risk reducing” to bypass checks; the core derives that property from supported position semantics.

## Units, nulls, and identifiers

- Exposure includes positions and supported outstanding-order reservations under the policy’s valuation rule.
- Price, quantity, notional, and currency conversions are distinct typed dimensions.
- Repeated lifecycle events cannot add a fill or release capacity twice.
- An accepted decision and its reservation are committed atomically.
- A policy revision cannot silently reinterpret an earlier accepted decision.

An absent value, unknown value, invalid value, and numerical zero are distinct. Identifiers preserve source namespaces. Timestamps identify clock and precision. Collections specify whether their order is semantically significant. Statistical summaries specify population, filters, denominators, and time window. Serialization decisions must survive a cross-language round trip without precision loss.

## Storage and migration

Immutable source evidence is stored separately from derived views. A migration names source and destination versions, checks prerequisites, and produces a validation report. The prior accepted artifact remains available until the replacement passes its checks. Changes to meaning or units require a new schema major version. A path rename does not alter content identity; a corrected input changes lineage even when the filename is unchanged.

## Retention and portability

Keep manifests and compact diagnostics for accepted runs. Large raw inputs may live outside Git and carry availability and redistribution metadata. An export includes a relative artifact index and integrity digests, avoiding machine-specific absolute paths. Reports clearly identify missing or restricted inputs. User-generated or private information is included only in deliberately selected export scopes.
