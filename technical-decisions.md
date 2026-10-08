# Technical Decisions & Toolchain Verification

## 1. Verified Software Versions

| Tool / Dependency | Version | Verification Status |
| :--- | :--- | :--- |
| **Rust** | `1.97.1` | Verified locally via `rustc --version` |
| **Cargo** | `1.97.1` | Verified locally via `cargo --version` |
| **Wasm Target** | `wasm32-unknown-unknown` | Installed and verified via `rustup` |
| **Stellar CLI** | `28.0.0` | Verified locally via `stellar --version` |
| **Soroban SDK** | `22.0.1` | Target dependency version for Cargo |
| **Node.js** | `v20.20.1` | Verified locally via `node --version` |
| **pnpm** | `9.15.4` | Verified locally via `pnpm --version` |
| **Next.js** | `14.2.15` | Target framework for `fanout-app` |
| **TypeScript** | `5.6.3` | Target language version |
| **PostgreSQL** | `15` / `16` | Database engine for backend & indexer |

---

## 2. Architecture Overview

Fanout is structured as a dual-repository system inside the `/home/dell/drips/fanout` workspace:

1. **`fanout-contracts`**:
   - Pure Rust workspace housing Soroban smart contracts (`agreement` contract, shared crates).
   - Responsible for deterministic revenue distribution, basis points allocation math, proposal governance, and event emission.

2. **`fanout-app`**:
   - Next.js monorepo (`apps/web`, `apps/api`, `services/indexer`, `packages/sdk`, `packages/stellar`, `packages/database`).
   - Responsible for landing page, user dashboard, wallet signing (Freighter/SEP-0007), public payment links, REST API, Stellar RPC event indexing into PostgreSQL, and developer SDK.

---

## 3. Financial Invariants & Arithmetic Design

- **Basis Points Standard**: Allocations are defined in basis points where $10,000 \text{ BPS} = 100.00\%$.
- **Validation**:
  $$\sum_{i=1}^{N} \text{allocation\_bps}_i = 10,000$$
- **Rounding Algorithm**: Deterministic Largest Remainder Method.
  For an amount $A$ and BPS $B_i$:
  $$\text{base}_i = \lfloor \frac{A \times B_i}{10,000} \rfloor, \quad \text{remainder}_i = (A \times B_i) \pmod{10,000}$$
  The remaining base units $\Delta = A - \sum \text{base}_i$ are allocated $1$ unit each to the top $\Delta$ beneficiaries with the largest fractional remainders $\text{remainder}_i$ (tie-broken by recipient index).
- **Invariants**:
  - $\sum \text{distributed\_amounts} == \text{payment\_amount}$
  - No token truncation or residual funds locked in contract.
  - Zero floating point operations. All math uses `i128` integer base units.
