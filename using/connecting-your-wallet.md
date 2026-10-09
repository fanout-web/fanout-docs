# Connecting Your Wallet

Install Freighter, select the same Stellar network configured by Fanout, and unlock the extension. Fanout asks Freighter for account access only when a wallet action begins. Review the contract ID, function, asset, amount, and network in the signing prompt.

Fanout never needs your recovery phrase or private key.

## Before connecting

1. Install Freighter from an official Stellar or browser-extension source.
2. Create or select a dedicated Testnet account.
3. In Freighter, set the network to **Testnet**.
4. Confirm that the address bar shows `https://fanout-labs.vercel.app`.
5. Fund the Testnet account with test assets only.

## Connect

Select **Connect wallet** in Fanout. Freighter may first ask whether the site can view the active public address and request transaction approvals. Approving access does not sign a payment and does not reveal the wallet's secret key.

If the first request remains pending, open the Freighter extension and complete the approval there. Fanout should then display a shortened version of the connected public address.

## Disconnect

Open Freighter's connected-sites settings, remove `fanout-labs.vercel.app`, and refresh the application. Disconnecting removes site access; it does not delete the Stellar account or reverse previous transactions.

## Safety checks

Do not continue if Freighter displays Mainnet, an unexpected contract, an unknown asset, or a security warning you have not independently resolved. Never paste a recovery phrase into Fanout, GitBook, a support message, or a transaction form.
