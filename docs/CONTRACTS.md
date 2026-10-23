# Exchange contract conventions — draft v0.1

These are proposed file and message contracts. No compatible runtime exists yet. Each producer owns its domain schema; consumers negotiate a specific schema version. Shared conventions do not make unrelated domain events interchangeable.

## Envelope

| Field | Meaning | Constraint |
| --- | --- | --- |
| schema_name / schema_version | Domain contract and semantic version | Unknown major versions are rejected |
| artifact_id | Stable identifier for the immutable artifact | Independent of its current file path |
| producer / producer_revision | Originating tool and source revision | Dirty worktrees are explicitly identified |
| run_id / parent_run_id | Experiment or session lineage | Parent may be absent; cycles are invalid |
| created_at | UTC creation timestamp | Metadata only; never establishes domain event ordering |
| payload_hash | Digest of canonical payload bytes | Canonicalization and hash algorithm are recorded |
| provenance | Inputs, rights, transforms, and known gaps | Missing information is represented explicitly |

## Time and numerical representation

Financial events preserve exchange time, local receive time, and a monotonic ordering key independently. A monotonic clock measures local elapsed time and cannot be compared directly across machines. A game simulation uses integer ticks or discrete-event time, with its time unit and engine version recorded. Wallet events use chain ID, block hash, transaction hash, and log position. None of these clocks is silently converted into another domain's ordering key.

Prices, balances, and inventory amounts carry units. Monetary values and quantities at decision boundaries use fixed-point integers or exact decimal representations with explicit scale. JSON transports large integers as decimal strings where necessary to avoid floating-point truncation. Statistical estimates may use floating point; tolerance, missing-value policy, and aggregation method belong in the result specification.

## Compatibility and failure behavior

Additive optional fields may be compatible within a major version, but changes to units, interpretation, ordering, or identifiers require a new major contract. An importer validates the entire manifest before mutating visible state. Invalid imports produce a diagnostic report and leave the previous accepted version available. A partial artifact stays incomplete and cannot masquerade as a completed run.

Delivery is assumed to be at least once where retries exist. Consumers deduplicate using stable domain identifiers plus revision context, not arrival time. Exact retry semantics are specified by each adapter. Revisions preserve earlier evidence and explain supersession; they do not silently rewrite history. No global exactly-once guarantee is claimed.

## Minimum interoperability acceptance

Producer and consumer maintain one shared synthetic fixture, an unsupported-version fixture, a corrupt-hash fixture, and a duplicate-delivery fixture. A contract change names the producer owner, consumer owner, migration direction, and compatibility evidence. Adapters use files or an explicit local process boundary initially. No repository requires a shared database, always-on central server, or another project's UI.
