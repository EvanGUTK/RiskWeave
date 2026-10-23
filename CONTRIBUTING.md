# Contributing to RiskWeave

This is a documentation-first project. Architecture reviews, minimized scenarios, interface critiques, and bounded implementation proposals are useful contributions. Read [STATUS.md](STATUS.md), the [roadmap](docs/ROADMAP.md), and the [implementation handoff](docs/IMPLEMENTATION_HANDOFF.md) first.

## Propose a change

Describe the user problem, present scope, expected behavior, affected invariant, and acceptance evidence. Separate a platform fact from an assumption or proposal. Link primary documentation for external capabilities. Include one concrete example and one relevant failure case. Avoid introducing a service or dependency without identifying the requirement it satisfies.

## Review a change

Check units, identities, ordering, idempotency, recovery, compatibility, and reproducibility. Planned behavior remains labeled until working evidence exists. A documentation change should preserve local links and update contradictory sections. An implementation change must satisfy its bounded acceptance criteria and document material limits.

## Data and assets

Use synthetic examples by default. Do not commit account details, credentials, private inputs, restricted market data, personal wallet mappings, or unlicensed assets. Original artwork should have a clear source. Third-party material retains its own rights regardless of the repository license.

## Branches

The default branch is main. Use a focused feature branch when implementing a change. Do not introduce a second long-lived branch just to hold the blueprint. No runtime test or CI status is implied by the presence of review templates.
