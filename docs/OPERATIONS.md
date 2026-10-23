# RiskWeave — operations and recovery plan

## Initial operating model

Begin with one local coordinator process and one durable journal. Activation and reconciliation commands are explicit operator actions. Back up the journal with its schema and policy bundles. On startup, reconcile outstanding and unknown external orders before accepting new exposure-increasing intents.

## Startup protocol

Load and validate the effective configuration; record its digest. Verify schema compatibility, output permissions, free storage, and required source availability. Recover or quarantine incomplete prior work before accepting new commands. A startup failure identifies the failed prerequisite and leaves accepted artifacts untouched. Show the exact active environment and mode in diagnostics.

## Failure handling

A missing price, incompatible scale, stale portfolio, journal write failure, or unsupported policy rule prevents acceptance when required for the decision. If an accepted intent times out while routing, its status becomes external-outcome-unknown and capacity remains reserved until reconciliation. A cancel request alone is insufficient to release capacity. Restart replays accepted journal events and compares against the execution client’s snapshot before reopening acceptance.

## Persistence and backup

Configuration, immutable manifests, and accepted outputs have distinct lifecycles. Before adopting a backup as valid, restore it into a separate location and verify artifact digests and a representative result. Checkpoint frequency is a measured tradeoff between storage and recoverable work. The application never assumes a process supervisor or the browser session is a durable state store.

## Diagnostics and resource boundaries

Logs record run, input, and correlation IDs. Counters distinguish attempts, accepted work, duplicates, failures, and retries. Disk exhaustion has a defined stop condition. Large files live outside Git. Credentials and user-private artifacts are excluded from logs and public diagnostics. External-service adapters record their endpoint class, permission needs, quotas, and recovery policy when implemented.

## Release lifecycle

Build from a recorded revision, validate setup in a clean environment, run the domain acceptance scenarios, and create release notes that identify known limitations. Schema migrations require a tested reverse or restore path. A rollback preserves raw evidence and records which derived outputs require recomputation. Public issue reports should use synthetic reproductions where possible.
