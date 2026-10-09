# Making a Payment

Open an agreement payment link, enter a positive amount, connect Freighter, and review the split preview. A successful screen must only be shown after Stellar RPC reports a successful transaction. A rejected, expired, or failed transaction does not count as payment.

## Payment checklist

1. Verify the payment link and agreement contract ID.
2. Confirm that Freighter and the agreement use Stellar Testnet.
3. Review the accepted asset, payment amount, and displayed recipients.
4. Connect the payer account and make sure it has enough balance for the payment and network fee.
5. Approve the `distribute` invocation in Freighter only after reviewing its effects.
6. Wait for confirmed success and open the explorer link to independently verify the transaction.

## Payment references

Every payment includes a unique reference. The agreement records processed references and rejects a replay, even if the same transaction is prepared again. Integrators should generate stable, collision-resistant references and retain the relationship between the reference, transaction hash, and business record.

## When a payment fails

A cancellation means the wallet did not authorize the transaction. A simulation error usually indicates invalid contract input, insufficient balance, an inactive agreement, or a network mismatch. A submitted transaction can also expire or fail during execution. Do not retry blindly with the same reference until you have checked the transaction status on Stellar.
