# Revenue-sharing Agreements

An agreement records its creator, accepted asset, beneficiaries, governance threshold, lifecycle status, configuration version, total distributed amount, and transaction count. `Active` agreements accept payments and proposals. `Suspended` and `Closed` agreements reject distribution.

## Core fields

- **Creator:** the address authorized to initialize the agreement and manage its lifecycle status.
- **Accepted asset:** the Stellar token contract used for every distribution.
- **Beneficiaries:** recipient addresses paired with allocations in basis points.
- **Approval threshold:** the number of authorized approvals required to execute an allocation proposal.
- **Version:** a monotonically increasing configuration number used to invalidate stale proposals.
- **Counters:** lifetime distributed base units and completed distribution count.

## Lifecycle

An `Active` agreement can accept distributions and governance proposals. `Suspended` is a reversible operational pause: payments are rejected until the creator restores the active state. `Closed` is terminal and cannot be reopened. Status checks are enforced by the contract, not merely by the interface.

Each agreement deployment represents one isolated revenue-sharing policy. A payment link identifies that agreement by its contract ID; it does not create a new custodial account.
