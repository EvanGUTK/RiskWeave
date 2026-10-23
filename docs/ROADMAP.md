# RiskWeave — milestone roadmap

Milestones are ordered by dependencies, not promised calendar dates. No implementation milestone is complete in this blueprint revision.

| Milestone | Deliverable | Exit criteria |
| --- | --- | --- |
| M0 — Domain | Units, long-only exposure, order states | Hand-computed traces reviewed |
| M1 — Pure rules | Compiler and deterministic evaluator | Invalid policies rejected; rule properties pass |
| M2 — Reservations | Transactional coordinator | Concurrent oversubscription scenario fails safely |
| M3 — Lifecycle | Fill/cancel/reject/unknown reconciliation | Duplicate and race cases conserve exposure |
| M4 — Evidence | Trace inspector and policy diff | Reviewer reproduces changed decisions offline |
| M5 — Consumer | One simulated execution integration | Restart and external-timeout conformance demonstrated |

## Definition of done

A milestone has a bounded scope, implementation revision, synthetic reproduction input, expected output, validation evidence, and a short demonstration. Setup instructions work in a clean supported environment. Failure behavior is documented alongside the ordinary case. The project status file advances only when the exit criteria are met.

## Scope control

The first milestone cannot depend on a sibling project or hosted service. Optional integrations follow standalone correctness. Performance optimization follows a representative workload and a repeatable baseline. New UI surfaces require a demonstrated user task. Dependencies and licenses are recorded when adopted; exact versions are pinned with implementation.

## Work sequencing

Review [IMPLEMENTATION_HANDOFF.md](IMPLEMENTATION_HANDOFF.md) before creating worktrees. Keep contract changes separate from adapter changes where that allows a reviewer to understand compatibility. A change that invalidates an earlier milestone must update its acceptance evidence and status, not simply append a new roadmap item.

## Deferred expansion

No brokerage routing inside the core, regulatory certification, options portfolio margin, cross-venue netting, derivatives liquidation modeling, or claims of mathematically complete financial safety. Complex valuation and multi-currency conversion require separately specified sources and freshness rules.

Open decisions in [DECISIONS.md](DECISIONS.md) should be resolved by a small experiment or a documented requirement. They are not a reason to build every alternative.
