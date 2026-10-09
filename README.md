# Fanout

Fanout is a non-custodial revenue-sharing protocol built on Stellar. It lets a team define a payout agreement once and distribute every incoming payment across multiple recipients in a single, atomic Soroban transaction.

Instead of collecting revenue in a shared wallet and reconciling payouts manually, Fanout makes the allocation rules explicit and enforceable on-chain. Freighter signs transactions locally, recipients receive funds directly, and the contract provides a verifiable record of the configuration and every completed distribution.

{% hint style="warning" %}
**Testnet release:** the current public deployment is intended for demonstration and evaluation on Stellar Testnet. Do not send Mainnet assets or use it as a substitute for an independently audited production deployment.
{% endhint %}

## What Fanout provides

- **Atomic distributions:** every recipient is paid, or the entire transaction fails.
- **Non-custodial execution:** Fanout never receives wallet secret keys and does not hold funds between payouts.
- **Deterministic allocation:** shares are stored in basis points and must total exactly 10,000 (100%).
- **Exact rounding:** integer remainders are assigned deterministically so payouts always equal the original amount.
- **Replay protection:** a payment reference can be processed only once by an agreement.
- **On-chain governance:** authorized participants can propose and approve allocation changes without silently rewriting history.
- **Queryable history:** the API and indexer expose confirmed contract activity for dashboards and integrations.

## Start here

| I want to… | Recommended guide |
| --- | --- |
| Understand the product and trust model | [What is Fanout?](introduction/what-is-fanout.md) |
| See the end-to-end payment lifecycle | [How it works](introduction/how-it-works.md) |
| Connect Freighter safely | [Connect a wallet](using/connecting-your-wallet.md) |
| Configure a revenue split | [Create an agreement](using/creating-an-agreement.md) |
| Pay an existing agreement | [Make a payment](using/making-a-payment.md) |
| Integrate the API or run locally | [Developer guide](developer/local-setup.md) |
| Review contract guarantees | [Security invariants](contract/security.md) |
| Evaluate deployment readiness | [Production readiness](operations/production-readiness.md) |

## How a payment moves

1. A creator initializes an agreement with an accepted Stellar asset, recipient addresses, allocations, and governance threshold.
2. A payer opens the agreement, connects Freighter, and reviews the proposed distribution.
3. Freighter signs a Soroban invocation containing the amount and a unique payment reference.
4. The contract validates the agreement and transfers the calculated share directly to every recipient.
5. Stellar finalizes the transaction; only then does Fanout show the payment as successful.
6. The indexer records confirmed events in PostgreSQL for the API and dashboard. Indexed data is convenient, but the contract remains the source of truth.

## Live Testnet deployment

- **Application:** [fanout-labs.vercel.app](https://fanout-labs.vercel.app)
- **API health:** [fanout-labs.vercel.app/api/health](https://fanout-labs.vercel.app/api/health)
- **Network:** Stellar Testnet
- **Contract:** [`CCAK6YBIECDQ2GFPMYLV3GWQPJN2DVGJGDHKY76ESZHI56DZMELSTPRV`](https://stellar.expert/explorer/testnet/contract/CCAK6YBIECDQ2GFPMYLV3GWQPJN2DVGJGDHKY76ESZHI56DZMELSTPRV)
- **Verified payment:** [`77e0a9b…a04c`](https://stellar.expert/explorer/testnet/tx/77e0a9b12362f48a2bdddaec9865aea82b36ab2116b777c892bf8beca3ada04c)

## Open-source repositories

- [fanout-app](https://github.com/fanout-web/fanout-app) — Next.js web app, Express API, TypeScript SDK, database adapter, and event indexer.
- [fanout-contracts](https://github.com/fanout-web/fanout-contracts) — Soroban agreement contract, tests, deployment artifacts, and security documentation.
- [fanout-docs](https://github.com/fanout-web/fanout-docs) — this documentation and its GitBook configuration.

See [Deployment Status](operations/deployment-status.md) for the verified Vercel, API, database, Render worker, contract, and GitBook/GitHub Pages configuration. Use the [Submission Demo](operations/submission-demo.md) runbook before applying to Drips.

## Security boundary

Fanout's web application and indexed API are convenience layers. They can prepare transactions and present confirmed activity, but they cannot bypass contract authorization or move funds without a wallet signature. Always verify the network, contract ID, asset, amount, and recipients in Freighter before approving a transaction.

For vulnerabilities, use the private security-advisory workflow in the affected GitHub repository. Never publish recovery phrases, private keys, database credentials, or exploit details in a public issue.
