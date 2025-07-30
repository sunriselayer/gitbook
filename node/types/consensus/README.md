# Consensus Nodes

## Overview

- [Validator node](../consensus/validator-node.md): This type of node participates in consensus by producing and voting on blocks.
- [Full consensus node](../consensus/full-consensus-node.md): A sunrise-app Full node to sync blockchain history.

{% hint style="info" %}
**Data Availability Layer**: In addition to standard consensus tasks, Validator Nodes on Sunrise are responsible for verifying data for the Data Availability (DA) layer. This requires running additional daemons alongside the main `sunrised` process. See the [validator documentation](../../../build/validators/README.md) for more details.
{% endhint %}

### Requirements

| Type           | CPU    | Architecture | Mem  | Disk       | Bandwidth |
| -------------- | ------ | ------------ | ---- | ---------- | --------- |
| Validator      | 6 Core | x86_64       | 8 GB | 500 GB SSD | 1 Gbps    |
| Full Consensus | 4 Core | x86_64       | 8 GB | 250 GB SSD | 1 Gbps    |
