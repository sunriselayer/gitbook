# Supported L2 SDKs

## Sunrise Documents

- [Rollkit](./rollkit/README.md)
  - [Sunrise Data](./rollkit/sunrise-data.md)
  - [Rollkit L2 Chain](./rollkit/rollkit.md)
- [Optimism OP Stack](./optimism/README.md)
  - [Sunrise Data](./optimism/sunrise-data.md)
  - [OP Stack L2 Chain](./optimism/op-stack.md)

## How to create L2

It is recommended to run the full consensus node locally, without relying on an external RPC.

[Sunrise Consensus Node Document](../../../node/types/consensus/README.md)

### Rollkit

`sunrise-data`, and `rollkit` need to be run.

### OP Stack

`sunrise-data`, `optimism` and `op-geth` need to be run.

The local EVM L1 chain is only used to meet OP Stack requirements. The actual data (metadata) is stored in Sunrise.

Please Use Ganache, Hardhat, Anvil or etc as local L1 chain.

## Requirements

| Type                    | CPU    | Architecture | Mem   | Disk     | Bandwidth |
| ----------------------- | ------ | ------------ | ----- | -------- | --------- |
| Rollkit + Sunrise Data  | 4 Core | x86_64       | 16 GB | 1 TB SSD | 1 Gbps    |
| OP Stack + Sunrise Data | 6 Core | x86_64       | 32 GB | 1 TB SSD | 1 Gbps    |

## Official Document

- [Rollkit](https://rollkit.dev/learn/intro)
  - [BeaconKit (option)](https://rollkit.dev/tutorials/execution/beaconkit): By combining BeaconKit and Rollkit, EVM compatible L2 blockchain is possible to develop.
- [OP Stack](https://docs.optimism.io/stack/getting-started)
