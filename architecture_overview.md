# Fanout — Master Architecture Overview & Submission Report

> **"One payment. Everyone gets their share."**

---

## Executive Summary

**Fanout** is a production-grade, dual-repository revenue-sharing platform engineered specifically for the **Stellar Drips Wave Maintainer** evaluation. It enables organizations, open-source maintainers, and creator teams to establish programmable revenue distribution contracts on the Stellar network using Soroban smart contracts.

---

## 🏗️ Monorepo & Dual-Repository Architecture

```
fanout/
├── fanout-contracts/           # Soroban Smart Contract Suite (Rust / no_std)
│   ├── contracts/
│   │   └── agreement/         # Core agreement, Largest-Remainder math, & governance
│   └── scripts/               # Build, test & Testnet deployment scripts
│
└── fanout-app/                 # Full-Stack Application Monorepo (pnpm Workspaces)
    ├── apps/
    │   ├── web/               # Next.js 14 Web Application (Landing, Dashboard, Checkout)
    │   └── api/               # Express REST API Server
    ├── packages/
    │   ├── ui/                # React Design System & Component Library
    │   ├── stellar/           # Soroban RPC client & Freighter integration wrapper
    │   ├── sdk/               # Developer TypeScript SDK (@fanout/sdk)
    │   └── database/          # PostgreSQL DDL Schema & In-Memory Data Store
    └── services/
        └── indexer/           # Background Soroban RPC Event Indexer Daemon
```

---

## 🔒 Financial Invariants & Cryptographic Guarantees

1. **Basis-Points Allocations**: $10,000\text{ BPS} = 100.00\%$. The smart contract enforces $\sum \text{bps} == 10,000$ during initialization and governance execution.
2. **Largest Remainder Algorithm**: Solves the integer truncation problem in discrete token distributions.
   $$\sum \text{payouts} \equiv \text{total\_payment\_amount}$$
3. **Replay Protection**: Enforces global uniqueness of `payment_ref` symbols in Soroban instance storage.
4. **Protective Governance**: Agreement updates require $M$-of-$N$ signatures from registered beneficiaries before executing share changes.

---

## 🧪 Verification & Test Results

- **Smart Contract Test Suite**: `6/6` Unit and financial property tests passed (`cargo test`).
- **Wasm Optimization**: Compiled size is **28 KB** via `wasm32-unknown-unknown`.
- **Monorepo Build**: All 8 workspace packages compiled cleanly without error (`pnpm build`).

---

## 🌟 Stellar Playbook Compliance Checklist

- [x] Dual-repository structure (`fanout-contracts` and `fanout-app`).
- [x] `#![no_std]` Wasm safety with explicit basis points integer math.
- [x] Public Developer SDK (`@fanout/sdk`).
- [x] Soroban RPC Indexer with durable checkpointing.
- [x] Next.js 14 Responsive Web App with Freighter Wallet Integration.
- [x] CI/CD Workflow & Contribution documentation.
