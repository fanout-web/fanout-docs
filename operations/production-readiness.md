# Production Readiness

Before a production deployment:

- verify the Neon PostgreSQL connection, migration history, and Soroban RPC indexer checkpoint before each release;
- require explicit mainnet configuration and an agreement-contract allowlist;
- confirm transactions from RPC before presenting success;
- apply schema migrations, backups, retention, and restore tests;
- enforce TLS, restrictive CORS, rate limits, request size limits, and structured logs;
- monitor API health, indexer lag, failed transactions, and database saturation;
- complete an independent contract security review and rehearse rollback procedures.

The tagged `v0.1.1` release is a Testnet submission candidate, not a mainnet security certification.

For the currently verified public endpoints, hosting responsibilities, and environment settings, see [Deployment Status](deployment-status.md). Use the [Submission Demo](submission-demo.md) runbook for the required end-to-end recording.
