# RiskWeave — primary source register

Prepared 2026-10-23. References inform the proposal; upstream capabilities, entitlements, quotas, and versions must be rechecked when implementing an adapter. External documentation is not proof that this repository implements an integration.

| Primary reference | Design relevance |
| --- | --- |
| [Real World OCaml testing](https://dev.realworldocaml.org/testing.html) | Expect tests and property-based test design |
| [QCheck](https://github.com/c-cube/qcheck) | Property generation and failure minimization |
| [Alpaca paper trading](https://docs.alpaca.markets/us/docs/paper-trading) | Example simulated execution consumer; simulator limits remain external |

## Implementation verification tasks

Verify exact OCaml package versions and binding support when implementing. Check each execution adapter’s event identities, cumulative-fill semantics, cancel behavior, and reconciliation endpoints; no venue-independent order lifecycle is assumed without an adapter capability document.

## Evidence classification

Protocol or platform facts come from the linked primary documentation. Architecture, scope, component names, interface designs, and milestones are original proposals for this project. Future empirical claims must link their own input manifests and measurements. Do not copy provider examples, redistributable-looking data, or game art into the repository without checking the applicable license and attribution requirements.
