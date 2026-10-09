# The Problem

Revenue-sharing teams often calculate payouts in spreadsheets, hold funds in a central wallet, and perform several transfers manually. That creates custody risk, rounding errors, weak auditability, and uncertainty about which allocation rules applied.

Fanout moves the split into a contract. Payments either complete with every recipient transfer or fail as one transaction, and the payment reference prevents an accidental replay.

## Where manual settlement breaks down

- **One person controls the funds.** Participants must trust an operator to hold and forward revenue.
- **Rules drift over time.** A spreadsheet can change without a durable record of who approved the new split.
- **Partial payment is possible.** One transfer may succeed while another is forgotten or fails.
- **Rounding is inconsistent.** Percentage calculations can lose base units or distribute them differently between tools.
- **Reconciliation is expensive.** Teams must match invoices, wallet transfers, recipient lists, and exchange-rate assumptions by hand.

## Fanout's approach

An agreement makes the payout policy part of the transaction itself. The contract validates the active configuration, calculates each recipient's base-unit amount, rejects reused references, and performs every token transfer atomically. Governance proposals are tied to a configuration version so an outdated proposal cannot overwrite a newer agreement.

Fanout does not remove every operational responsibility. Teams must still verify recipient addresses, secure their wallets, select the correct network and asset, monitor contract activity, and complete an independent review before Mainnet use.
