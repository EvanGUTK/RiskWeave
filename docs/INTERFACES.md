# RiskWeave — interfaces and integration specification

All interfaces below are proposed contracts. Names describe responsibilities rather than installed APIs.

| Boundary | Request / input | Response / output | Guarantee |
| --- | --- | --- | --- |
| ValidatePolicy | Rule specification | PolicyBundle or typed diagnostics | No activation on incomplete required semantics |
| Evaluate | Bundle + context + intent | Candidate rule outcomes | Pure and deterministic; does not grant routing authority |
| AcceptAndReserve | Candidate + expected state revision | Accepted trace/reservation or conflict | Atomic revision and journal update |
| ApplyLifecycle | Authoritative lifecycle event | New state revision or reconciliation requirement | Deduplicate before changing capacity |
| ComparePolicies | Scenario set + policy revisions | Decision changes and causes | Original contexts preserved |

## Domain-specific behavior

A caller routes only after accepted reservation, but the transport wrapper is not a security boundary by itself. The live client must make acceptance non-bypassable in its own routing architecture. The protocol distinguishes an explicit reject from a timeout and unknown result. Cross-language clients preserve exact decimal scales. A local process wrapper can evolve to an embedded or binary boundary only after profiling and equivalent fixture evidence.

## Import and export rules

Imports validate schema version, domain units, source identity, completeness, payload hash, and declared capabilities. An unsupported optional capability is surfaced to the caller; mandatory capability gaps reject the request. Exporters include contract version and a provenance manifest, and must not require direct access to an internal database.

Request identities are stable across retries. Repeated completed requests return the recorded result or an explicit duplicate result; requests with an existing identity and different content are rejected. Timeouts distinguish a known rejection from an unknown external outcome. Consumers cannot infer that an action did not happen merely because a response was lost.

## Shared conventions

Use [CONTRACTS.md](CONTRACTS.md) for envelope, time, precision, and compatibility conventions. File-based interoperability is the first integration target. Binary or local process protocols can follow after a measured need and a conformance test. A contract's ownership is recorded in [ECOSYSTEM.md](ECOSYSTEM.md).

## Consumer conformance checklist

The future adapter must demonstrate valid import, unsupported-version rejection, precision-preserving round trip, duplicate handling, corrupt-artifact rejection, and recovery from a truncated output. This checklist specifies future evidence; it does not assert that an adapter already exists.
