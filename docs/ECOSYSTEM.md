# Ecosystem and integration boundaries

## Independent products, explicit adapters

Every repository must deliver its own first useful scenario using local synthetic data. Integration starts after that vertical slice works. Repositories exchange versioned artifacts, not database tables or private implementation classes. A sibling's outage must not make local review impossible.

| Direction | Contract | Purpose | Ownership boundary |
| --- | --- | --- | --- |
| TapeForge → TrailLedger | ReplayManifest + metrics + artifact digests | Reproduce and compare a market replay experiment | TapeForge owns simulation semantics; TrailLedger owns evidence lineage |
| RiskWeave → replay/execution clients | PolicyBundle + DecisionTrace + ReservationEvent | Explain a decision and reserve outstanding exposure | The execution client reconciles external orders; RiskWeave owns policy state |
| EconomyLab → TrailLedger | SimulationManifest + cohort metrics | Compare economy configurations and seeds | EconomyLab defines game metrics; TrailLedger records experiments |
| Shiftcraft → EconomyLab | EconomyConfig + supported progression events | Tune rewards, purchases, and unlock pacing | EconomyLab does not simulate factory movement or station scheduling |
| WalletTrace → research/reporting clients | ReconciliationReport + coverage manifest | Review supported on-chain asset movements | WalletTrace does not provide brokerage positions, execution authority, or complete tax accounting |

## Suggested integration order

1. Establish synthetic manifests and independently runnable first slices.
2. Connect TapeForge experiment exports to TrailLedger; validate imports without either UI running.
3. Connect RiskWeave to one simulated execution adapter and test reservation races.
4. Connect EconomyLab experiment records to TrailLedger.
5. Add a narrow Shiftcraft economy mapping after its core production loop is playable.
6. Add WalletTrace reporting only where supported on-chain movement evidence is actually relevant.

Do not create a single universal strategy interface for game agents, trading models, and wallet classifications. Their shared needs are provenance and versioned evidence, while their state and correctness rules remain different.

## Public project directory

- [TapeForge](https://github.com/EvanGUTK/TapeForge)
- [RiskWeave](https://github.com/EvanGUTK/RiskWeave)
- [TrailLedger](https://github.com/EvanGUTK/TrailLedger)
- [WalletTrace](https://github.com/EvanGUTK/WalletTrace)
- [EconomyLab](https://github.com/EvanGUTK/EconomyLab)
- [Shiftcraft](https://github.com/EvanGUTK/Shiftcraft)
