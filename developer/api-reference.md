# API Reference

All application endpoints are under `/api/v1`. `GET /health` is intended for health checks. Agreement endpoints provide indexed agreement data. Payment-request endpoints create shareable links; they do not move assets. Payment history and analytics are derived from confirmed indexed events.

Clients must treat non-2xx responses as failures and should use an idempotency key for write requests. API data is a convenience read model; verify high-value state against Stellar RPC.

## Base URL and response shape

The public deployment exposes the API through the same origin as the web application. Successful resource responses use `{ "success": true, "data": ... }`; failures use `{ "success": false, "error": "..." }`. The health endpoint has its own operational response shape.

## Endpoints

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/api/health` | Database-backed service health, network, storage mode, and timestamp |
| `GET` | `/api/v1/agreements` | List indexed agreements |
| `GET` | `/api/v1/agreements/:id` | Read one indexed agreement |
| `POST` | `/api/v1/agreements` | Register validated agreement metadata in the read model |
| `POST` | `/api/v1/payments/requests` | Create a shareable payment URL; no asset transfer occurs |
| `GET` | `/api/v1/payments/history` | List recent indexed payments, optionally filtered by `agreementId` |
| `GET` | `/api/v1/analytics/summary` | Aggregate agreement and distribution counters |

## Important validation rules

Agreement creation accepts contract addresses beginning with `C`, account addresses beginning with `G`, one to twenty unique beneficiaries, positive allocations totaling 10,000 basis points, and an approval count between one and the beneficiary count. Payment requests accept a positive decimal string with at most seven fractional digits and a valid payer account.

Creating an API agreement record does not deploy or initialize a Soroban contract. Likewise, creating a payment request does not authorize or submit a Stellar transaction.
