# Creating an Agreement

Choose a name, accepted Stellar asset contract, recipient addresses, allocations totaling 100%, and approval threshold. Deployment and initialization are on-chain operations. Save the resulting contract ID in the configured contract allowlist so the indexer can discover its events.

## Information you need

- a clear agreement name;
- the accepted asset contract for the selected Stellar network;
- one valid Stellar address for each recipient;
- an allocation for every recipient totaling exactly 10,000 basis points; and
- an approval threshold appropriate for the number of participants.

## Review before signing

Recipient addresses cannot be inferred from names and should be verified out of band. Confirm that the asset and every address belong to the same network, that the threshold is achievable, and that no single allocation was entered as a percentage when the interface expects basis points.

After initialization succeeds, record the deployed contract ID and initialization transaction. Add the contract ID to the indexer's explicit allowlist before expecting it to appear in indexed API results.

{% hint style="info" %}
Creating an agreement does not transfer revenue. Funds move only when a payer separately authorizes a distribution.
{% endhint %}
