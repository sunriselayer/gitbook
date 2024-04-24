# Data Availability Nodes

## Overview

- [Bridge node](../data-availability/bridge-node.md): This node bridges blocks between the Data-Availability network and the Consensus network.
- [Full storage node](../data-availability/full-node.md): This node stores all the data but does not connect to Consensus.
- [Light node](../data-availability/light-node.md): Light clients conduct data availability sampling on the Data Availability network.

If you are looking to run a consensus node, please follow [the consensus node tutorial](../consensus/README.md).

:::note info
When running a validator node, a bridge node is required. See [this section](../data-availability/bridge-node.md).
:::

### Requirements

| Type         | CPU    | Mem    | Disk      | Bandwidth |
| ------------ | ------ | ------ | --------- | --------- |
| Bridge       | 6 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| Full Storage | 4 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| Light        | 2 Core | 500 MB | 50 GB SSD | 56 Kbps   |
