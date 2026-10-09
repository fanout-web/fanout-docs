# System Architecture

The browser signs Soroban transactions with Freighter. It never sends a secret key to Fanout. The API serves indexed, non-authoritative read models and payment links. The indexer consumes events from configured agreement contracts and writes idempotently to PostgreSQL. The agreement contract remains the authority for recipients, status, governance, replay protection, and transfers.

## Components

| Component | Responsibility | Trust level |
| --- | --- | --- |
| Next.js web app | Agreement views, transaction preparation, split previews, and wallet interaction | Untrusted presentation layer |
| Freighter | Account access and local transaction signing | User-controlled wallet |
| Soroban agreement | Authorization, allocation, governance, replay protection, and token transfers | On-chain source of truth |
| Express API | Payment links and indexed query endpoints | Non-authoritative read model |
| Event indexer | Reads confirmed contract events and advances a durable checkpoint | Rebuildable infrastructure |
| PostgreSQL | Indexed agreements, transactions, and operational state | Cached application data |
| Stellar RPC | Simulation, submission, status, and ledger data | Network interface |

## Data flow

The browser reads an agreement, constructs a contract invocation, and hands it to Freighter. After user approval, the signed envelope is submitted to Stellar RPC. Soroban executes the agreement and token calls atomically. The indexer later consumes the resulting events and upserts them into PostgreSQL. API responses therefore may lag the latest ledger, while contract state does not depend on the API or database.

## Failure boundaries

- If the API is unavailable, existing contracts still operate through Stellar tooling.
- If the indexer falls behind, dashboard history can be stale without affecting settlement.
- If PostgreSQL is rebuilt, confirmed events can be replayed from the last trusted checkpoint.
- If the browser is compromised, Freighter still provides the final signing boundary; users must inspect its prompt carefully.

Production deployments must run the API and indexer as separate processes, use PostgreSQL with backups, restrict CORS, terminate TLS at the edge, and configure explicit contract IDs and Stellar network values.
