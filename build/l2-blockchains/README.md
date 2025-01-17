# Supported L2 SDKs

- [Rollkit](https://rollkit.dev/learn/intro)
  - [Sunrise Data](https://github.com/sunriselayer/sunrise-data): The software for connecting Rollkit L2 blockchain and Sunrise L1 blockchain.
  - [BeaconKit (option)](https://rollkit.dev/tutorials/execution/beaconkit): By combining BeaconKit and Rollkit, EVM compatible L2 blockchain is possible to develop.
- [OP Stack](https://docs.optimism.io/stack/getting-started)
  - [Sunrise OP DA Server](https://github.com/sunriselayer/sunrise-op-da-server): The software for connecting OP Stack L2 blockchain and Sunrise L1 blockchain.
  - [Sunrise Data](https://github.com/sunriselayer/sunrise-data): Required for Sunrise OP DA Server to work.

If you are looking to run a consensus node, please follow [the consensus node tutorial](../../node/types/consensus/README.md).

## Requirements

| Type                                   | CPU    | Mem   | Disk     | Bandwidth |
| -------------------------------------- | ------ | ----- | -------- | --------- |
| Rollkit + Sunrise Data                 | 4 Core | 16 GB | 1 TB SSD | 1 Gbps    |
| OP Stack + OP DA Server + Sunrise Data | 6 Core | 32 GB | 1 TB SSD | 1 Gbps    |
