# RiskWeave — architecture decision register

Status meanings: **proposed** is the current blueprint choice; **open** needs a bounded experiment before implementation. No choice here proves runtime behavior.

| ID | Status | Decision | Alternative / consequence |
| --- | --- | --- | --- |
| ADR-001 | Proposed | OCaml domain core | C++ remains possible for a different measured deployment; types and inspectable rules are the current purpose |
| ADR-002 | Proposed | Pure evaluation plus atomic acceptance | A boolean check alone cannot prevent concurrent oversubscription |
| ADR-003 | Proposed | External routing outside core | Keeps broker integration separate but requires a non-bypassable client design |
| ADR-004 | Proposed | Single coordinator initially | Simplifies serialization; distributed acceptance needs a separate consistency design |

## Open questions and resolution method

- **What precise long-only spot exposure model is sufficient for the first consumer?** Resolve with a minimal fixture, an explicit requirement, or a recorded compatibility check before expanding the corresponding milestone.
- **Which context sources and freshness bounds are authoritative?** Resolve with a minimal fixture, an explicit requirement, or a recorded compatibility check before expanding the corresponding milestone.
- **What local process and SQLite bindings meet the required support and performance needs?** Resolve with a minimal fixture, an explicit requirement, or a recorded compatibility check before expanding the corresponding milestone.

## Change protocol

Each new decision records context, considered alternatives, selected option, downside, acceptance evidence, and the condition that would trigger reconsideration. Superseded decisions remain in the register. A rejected alternative is recorded only when it explains a continuing tradeoff. Review decisions at milestone boundaries rather than changing foundational contracts incidentally during UI work.
