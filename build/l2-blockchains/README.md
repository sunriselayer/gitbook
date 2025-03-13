# Supported L2 SDKs

- [Rollkit](./rollkit/README.md)
  - [Sunrise Data](./rollkit/sunrise-data.md)
  - [Rollkit L2 Chain](./rollkit/rollkit.md)

- [Optimism OP Stack](./optimism/README.md)
  - [Sunrise Data](./optimism/sunrise-data.md)
  - [OP Stack L2 Chain](./optimism/op-stack.md)

## Infrastructures

### Rollkit

- [Rollkit](https://rollkit.dev/learn/intro)
- [sunrised](https://github.com/sunriselayer/sunrise)
- [sunrise-data](https://github.com/sunriselayer/sunrise-data)

### OP Stack

- [Optimism](https://github.com/ethereum-optimism/optimism)
- [op-geth](https://github.com/ethereum-optimism/op-geth)
- EVM L1 Chain
- [sunrised](https://github.com/sunriselayer/sunrise)
- [sunrise-data](https://github.com/sunriselayer/sunrise-data)

The local EVM L1 chain is used primarily to fulfill formal requirements. The actual data is stored in Sunrise.

Please Use Ganache, Hardhat, Anvil or etc.

To run `sunrised` consensus node, please follow [the consensus node tutorial](../../node/types/consensus/README.md).

## Official Document

- [Rollkit](https://rollkit.dev/learn/intro)
  - [BeaconKit (option)](https://rollkit.dev/tutorials/execution/beaconkit): By combining BeaconKit and Rollkit, EVM compatible L2 blockchain is possible to develop.
- [OP Stack](https://docs.optimism.io/stack/getting-started)

## Requirements

| Type                    | CPU    | Mem   | Disk     | Bandwidth |
| ----------------------- | ------ | ----- | -------- | --------- |
| Rollkit + Sunrise Data  | 4 Core | 16 GB | 1 TB SSD | 1 Gbps    |
| OP Stack + Sunrise Data | 6 Core | 32 GB | 1 TB SSD | 1 Gbps    |
