# Governance

The creator or a beneficiary may propose a new beneficiary list. Authorized participants approve it, and it becomes executable after reaching the agreement's configured quorum. Proposals are bound to the configuration version so an old proposal cannot overwrite a newer configuration.

## Proposal lifecycle

1. An authorized participant submits a complete replacement beneficiary list.
2. The contract validates addresses, allocation totals, beneficiary limits, and the current configuration version.
3. Authorized participants approve the proposal once each.
4. When the approval threshold is reached, the proposal can be executed.
5. Execution replaces the active allocation and increments the configuration version.

Approvals are explicit on-chain actions. Duplicate approvals do not increase the count, and a proposal created for an earlier configuration cannot execute after another proposal changes the agreement.

Governance controls future distributions only. It does not reverse completed payments or modify the event history.
