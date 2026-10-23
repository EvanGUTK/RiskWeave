# Policy and reservation lifecycle

## Decision states

An intent enters received, then validated or invalid. A valid intent is evaluated under a pinned policy and context. A proposed accept must still pass atomic revision checking. A revision conflict causes reevaluation, not a partial reservation. Accepted means the local reservation exists; it does not establish that an external venue accepted the order.

## Reservation states

Use reserved, routing, externally-open, partially-filled, external-outcome-unknown, and terminal states with explicit transition evidence. A failed network response can leave the external outcome unknown. Expiring a local timeout cannot establish that an order never reached the venue. Query by stable client order identity before deciding whether retrying would duplicate an order.

## Fill and cancel handling

A fill transfers the corresponding exposure from outstanding capacity to the supported position representation in one transaction. A cancellation request changes intent but not confirmed remaining exposure. Cancellation confirmation releases supported residual quantity after accounting for cumulative fills. An execution client presenting inconsistent cumulative values forces reconciliation.

## Policy changes

Compile and evaluate candidate policies against recorded contexts before activation. Activation records a revision boundary. Existing open orders remain visible under their original decisions. A tighter policy can prevent new orders while the operator or execution client decides how to handle existing exposure; the engine must not pretend the exposure disappeared.

## Scope of guarantees

Property tests establish invariants inside the declared state and valuation model. They do not establish complete market-risk coverage, reliable broker data, or the correctness of an unknown external state. Recovery and source completeness therefore belong to the policy acceptance boundary.
