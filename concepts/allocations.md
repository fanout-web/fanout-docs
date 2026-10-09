# Basis Points and Rounding

Each beneficiary receives an allocation in basis points: 100 basis points equals 1%, and all allocations must sum to 10,000. Fanout uses integer arithmetic. When division leaves base units, the contract assigns them by largest remainder so the payouts always sum exactly to the payment amount.

## Example

An allocation of 5,000 / 3,000 / 2,000 basis points represents 50% / 30% / 20%. For a payment of 101 base units, the exact fractional results cannot all be represented as integers. Fanout first assigns each recipient's whole-unit share, then distributes the remaining unit according to the largest fractional remainder with deterministic tie-breaking.

This guarantees two properties:

1. no value is created or lost during allocation; and
2. the same inputs always produce the same recipient amounts.

Application interfaces may display decimal asset amounts, but contract calls use integer base units. Integrations must apply the asset's declared precision exactly once and must not pass floating-point values to the contract.
