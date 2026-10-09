# How It Works

Fanout separates the authoritative payment path from the read-only application experience. Stellar and the Soroban contract settle funds; the web app, API, and indexer make that activity easier to initiate and inspect.

## 1. Create an agreement

A creator initializes an agreement with a display name, accepted Stellar asset contract, recipient addresses, allocations, and approval threshold. Allocations are expressed in basis points and must total 10,000.

## 2. Prepare a payment

A payer opens an agreement payment page and enters an amount. The application reads the current agreement configuration and shows the expected split before requesting a signature. This preview is informative; the contract repeats every important validation during execution.

## 3. Sign with Freighter

The browser requests access to the payer's public address and asks Freighter to sign the Soroban transaction. Secret keys remain inside the wallet. The payer should verify the Stellar network, contract, function, asset, amount, and recipient effects shown by Freighter.

## 4. Execute atomically

The payer submits `distribute` with a positive amount and unique payment reference. The contract verifies that the agreement is active, calculates integer payouts, rejects a previously used reference, and invokes the accepted token contract for each transfer. If any validation or transfer fails, the whole transaction fails.

## 5. Confirm and index

The application waits for a successful RPC result before presenting payment success. Contract events are then indexed into PostgreSQL for the dashboard and API. Consumers that need authoritative confirmation should verify the transaction against Stellar RPC or an explorer.

## 6. Change an allocation

An authorized participant can propose a new recipient list. Other authorized participants approve it until the configured threshold is met. Execution updates the agreement version, and proposals created against an older version can no longer execute.

Amounts use the asset's base unit. Allocations use basis points and must total 10,000.
