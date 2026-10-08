# Contract Deployment

Build the optimized WASM, install it with the Stellar CLI, deploy a contract instance, and invoke `initialize` exactly once with reviewed addresses and allocations. Record the network passphrase, WASM hash, contract ID, transaction hash, and source tag in a deployment manifest.

Testnet and mainnet identifiers must never be mixed. Verify the deployed WASM hash before publishing an address.

## Current verified Testnet deployment

- Contract ID: `CCAK6YBIECDQ2GFPMYLV3GWQPJN2DVGJGDHKY76ESZHI56DZMELSTPRV`
- WASM SHA-256: `d5776eb00bbb58733c35cfa9d6e90b27eab3e306d67ecefb6478fdf18438ab33`
- [Contract explorer](https://stellar.expert/explorer/testnet/contract/CCAK6YBIECDQ2GFPMYLV3GWQPJN2DVGJGDHKY76ESZHI56DZMELSTPRV)
- [Initialization transaction](https://stellar.expert/explorer/testnet/tx/50fdf4c45b8b2e8e3b3680263534bbb51b1e2a7109922e91d0f7608791aa36fa)
- [Verified payment transaction](https://stellar.expert/explorer/testnet/tx/77e0a9b12362f48a2bdddaec9865aea82b36ab2116b777c892bf8beca3ada04c)
