# What is Fanout?

Fanout is a programmable payment-splitting protocol for teams that share revenue. A creator records recipient addresses, percentage allocations, an accepted Stellar asset, and governance rules in a Soroban agreement. Each payment is then divided by that agreement and delivered directly to the recipients.

## Why it exists

Collaborative projects often receive revenue into one person's wallet, calculate shares in a spreadsheet, and execute several transfers later. That process creates custody risk, operational delay, calculation mistakes, and an incomplete audit trail.

Fanout replaces that workflow with a deterministic contract call. The same allocation rules are applied to every payment, and all recipient transfers succeed or fail together.

## What is on-chain

The agreement contract is authoritative for:

- the accepted asset and recipient allocation;
- agreement status and configuration version;
- participant approvals and governance proposals;
- processed payment references and replay protection;
- total distributed value and transaction count;
- the token transfers performed by a distribution.

## What is off-chain

The web application prepares transactions and presents human-readable previews. The API and indexer store confirmed events for fast search, dashboards, and integrations. These services improve usability but are not trusted to authorize transfers or redefine an agreement.

## Intended users

Fanout is designed for creator teams, open-source collectives, digital agencies, protocol contributors, and other groups that need transparent, repeatable revenue allocation. The current deployment is a Stellar Testnet release for evaluation, not an audited Mainnet financial product.

Next, read [How it works](how-it-works.md) for the full transaction lifecycle or [Security invariants](../contract/security.md) for the rules enforced by the contract.
