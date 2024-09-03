# Overview to running nodes on Sunrise

There are many ways you can participate in the Sunrise [networks](../networks/README.md).
Sunrise node operators can run several options on the network.

## Consensus

- [Validator node](./consensus/build-validator-node.md): This type of node participates in consensus by producing and voting on blocks.
- [Full consensus node](./consensus/build-full-node.md): A sunrise-app Full node to sync blockchain history.

## Data Availability

- [Bridge node](./data-availability/bridge-node.md): This node bridges blocks between the Data-Availability network and the Consensus network.
- [Full storage node](./data-availability/full-node.md): This node stores all the data but does not connect to Consensus.
- [Light node](./data-availability/light-node.md): Light clients conduct data availability sampling on the Data Availability network.

## Requirements

| Type           | CPU    | Mem    | Disk       | Bandwidth |
| -------------- | ------ | ------ | ---------- | --------- |
| Light          | 2 Core | 500 MB | 50 GB SSD  | 56 Kbps   |
| Full Storage   | 4 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| Bridge         | 6 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| -------------- | ------ | ----   | ---------- | --------- |
| Validator      | 6 Core | 8 GB   | 500 GB SSD | 1 Gbps    |
| Full Consensus | 4 Core | 8 GB   | 250 GB SSD | 1 Gbps    |

You can learn more about how to set up each different node by going through each tutorial guide.
