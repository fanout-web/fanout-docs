# Deployment Status

Fanout's public submission environment uses Stellar Testnet. It is intended for evaluation and demonstration, not for Mainnet funds.

## Verified public services

| Component | Platform | Public location | Verification |
| --- | --- | --- | --- |
| Web application | Vercel | [fanout-labs.vercel.app](https://fanout-labs.vercel.app) | Returns the production Next.js application |
| REST API | Vercel service | [API health](https://fanout-labs.vercel.app/api/health) | Returns `status: ok`, `network: testnet`, and `storage: postgres` |
| Documentation | GitHub Pages | [fanout-web.github.io/fanout-docs](https://fanout-web.github.io/fanout-docs/) | Published from the `fanout-docs` main branch |
| Agreement contract | Stellar Testnet | [Contract explorer](https://stellar.expert/explorer/testnet/contract/CCAK6YBIECDQ2GFPMYLV3GWQPJN2DVGJGDHKY76ESZHI56DZMELSTPRV) | Deployment manifest and on-chain invocation history are public |
| Indexed payment | Stellar Testnet | [Transaction explorer](https://stellar.expert/explorer/testnet/tx/77e0a9b12362f48a2bdddaec9865aea82b36ab2116b777c892bf8beca3ada04c) | Appears in the public API payment history |

The documentation repository also includes `.gitbook.yaml` and `SUMMARY.md` for GitBook Git Sync. Publishing a GitBook domain requires the repository owner to connect `fanout-web/fanout-docs` to a GitBook space. GitHub Pages remains the verified public documentation URL until that account-level connection is published.

## Service topology

```text
Browser + Freighter
        |
        +---- signed transaction ----> Stellar RPC ----> Fanout contract
        |
        +---- HTTPS ----> Vercel web + REST API ----> PostgreSQL
                                                   ^
                                                   |
                         Render indexer worker -----+
                                  |
                                  +---- Soroban RPC events
```

The API is request-driven and can run as a Vercel service. The indexer cannot: it continuously polls Soroban RPC, so the supplied `render.yaml` deploys it as a Render background worker. The worker and API must share the same `DATABASE_URL`.

## Required production configuration

### Vercel

- Deploy the repository root using `vercel.json`.
- Do not manually set `FANOUT_API_URL`; Vercel's service binding supplies it.
- Keep `/api/*` routed to the Express service and all other paths routed to Next.js.

### Render

- Create the services from `render.yaml`.
- Set `DATABASE_URL` to the same PostgreSQL database used by the public API.
- Keep `FANOUT_CONTRACT_IDS` restricted to verified deployments.
- Confirm worker logs show the allowlisted contract count and advancing event checkpoints.

### Release verification

Before recording or submitting, verify:

```bash
curl --fail https://fanout-labs.vercel.app/api/health
curl --fail https://fanout-labs.vercel.app/api/v1/agreements
curl --fail https://fanout-labs.vercel.app/api/v1/payments/history
```

The health response proves API and database reachability. The agreement and payment responses prove that the deployed read model contains the documented contract and transaction. Render worker liveness is verified in its private service logs because a background worker has no public HTTP endpoint.
