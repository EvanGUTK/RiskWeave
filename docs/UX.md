# RiskWeave — experience and visual direction

## Design thesis

Make policy arithmetic inspectable. The main object is a decision with its context and rule tree, not a generic account dashboard.

## Screen model

| Screen / surface | Primary task | Interaction and state |
| --- | --- | --- |
| Policy review | Validate and activate a revision | Show effective scope, unsupported rules, and changes |
| Decision inspector | Explain accept or reject | Expand inputs and arithmetic; link reservation lifecycle |
| Capacity ledger | Understand outstanding exposure | Show position, reserved, unknown, and available capacity separately |
| Policy comparison | Review changed behavior | Filter by rule and inspect the same context under both revisions |

## Visual system

The repository identity uses charcoal and violet structure, lavender trace connectors, aligned arithmetic, and explicit status labels. The application should develop this direction with readable typography and deliberate information hierarchy. Numbers align by scale and unit. Visual emphasis belongs to the active question, selected event, unresolved discrepancy, or next action. Avoid filling the opening view with interchangeable statistic cards.

## Interaction rules

Selection persists when the user changes a filter, or the UI explains why the selected object is now outside the view. Comparisons preserve each run's identity and configuration. Loading, empty, incomplete, invalid, stale, and successful states are distinct. A result panel keeps the evidence drawer available so the user can inspect source events without losing context.

Keyboard navigation covers the primary journey. Color is reinforced by text, symbols, or line patterns. Tooltips expand unfamiliar terms but do not hide required units or failure reasons. Text and chart axes remain readable at normal laptop sizes. Destructive local edits provide a review of their exact scope and preserve recoverable prior revisions where feasible.

## First demonstration storyboard

Submit two racing intents that exceed their shared remaining capacity. Expand the second request’s conflict and reevaluation, then partially fill and cancel the first. Show why capacity changes only when the lifecycle evidence permits it.

The first demo uses synthetic or explicitly redistributable material and carries an illustrative label until the runtime produces it. The committed SVG banner is an identity asset, not evidence of a working application. Future screenshots should come from the application at a recorded revision.
