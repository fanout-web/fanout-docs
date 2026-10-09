# Security Model

Private keys stay in the user's wallet. The UI is untrusted presentation; the Soroban contract enforces authorization, status, allocation totals, governance, and replay protection. The API must validate every request and must not claim an unconfirmed transaction succeeded.

## Trust assumptions

- Users trust Freighter to protect signing keys and accurately display transaction requests.
- Users independently verify the application origin, Stellar network, contract, and asset.
- The contract depends on Stellar consensus and the accepted token contract behaving as specified.
- Indexed API data can be delayed or unavailable and must not override ledger state.
- Deployment operators protect database credentials, RPC configuration, contract allowlists, and release access.

## Operational controls

Production services should use restrictive CORS, TLS, request-size limits, rate limiting, structured audit logs, secret rotation, dependency monitoring, database backups, and alerts for indexer lag or failed submissions. Mainnet configuration must fail closed when network, passphrase, RPC URL, or contract identifiers are missing or inconsistent.

## User protections

Fanout never asks for a recovery phrase or raw secret key. Transaction success is reported only after confirmation, and high-value users should independently check the transaction hash with Stellar RPC or a block explorer.

Report vulnerabilities through GitHub's private security advisory flow. Do not include secrets, private keys, or exploit details in a public issue.
