# RiskWeave — implementation handoff

## Read order

Read PRODUCT, DATA_MODEL, PIPELINE, and VALIDATION before selecting a work package. This repository currently contains documentation and original identity artwork only. Do not infer an executable stack from proposed folder names.

## Proposed module hierarchy

| Planned path | Responsibility | Dependency boundary |
| --- | --- | --- |
| core/ | Typed values, policy compiler, pure evaluator | No network or UI |
| journal/ | Reservation coordinator and lifecycle reducer | Owns accepted state transactions |
| adapters/ | Local process protocol and context translation | No implicit valuation changes |
| inspector/ | Trace and policy-diff views | Reads exported evidence |
| contracts/ | Decision and reservation specifications | Versioned cross-language boundary |
| fixtures/ | Hand-solved and generated scenarios | Independent of broker credentials |

## First work packages

| Package | Deliverable | Acceptance / review |
| --- | --- | --- |
| WP-01 | Supported units and order-state model | Review dimensions and missing-value behavior |
| WP-02 | Policy validation and one exposure rule | Hand-solved cases plus generated invariants |
| WP-03 | Atomic reservation coordinator | Two-order race and crash-after-commit fixture |
| WP-04 | Lifecycle reconciliation | Partial fill, cancel race, duplicate, and unknown outcome |
| WP-05 | Policy diff and local consumer | Same-context comparison and protocol conformance |

## Engineering discipline

Each work package should fit one reviewable behavior. Define the fixture and expected output before broadening the interface. Keep domain code independent of the UI and external adapters. Add meaningful tests for state transitions, failure recovery, and numerical semantics; avoid tests that simply restate an implementation. When a contract changes, update its fixture and every affected importer together or preserve a compatibility layer.

Use a short-lived feature branch from main. A worktree is optional and should correspond to a bounded task; no permanent development branch is required. Commit the smallest coherent change with its documentation and validation evidence. Merge only after the package's acceptance criteria are met. Do not add empty frameworks, unverified installation commands, dummy benchmark results, or success badges.

## First reviewer checklist

The reviewer can explain where canonical state lives, what event order means, which values carry units, how a retry is recognized, and how a partial result is rejected. The reviewer can reproduce the smallest scenario without credentials or another project. A larger implementation plan should be revised from the observed first slice rather than treating every proposed directory as a requirement.
