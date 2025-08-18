# OP Stack

Sunrise's Data Availability Layer supports Layer 2 blockchains created using [OP Stack](https://github.com/ethereum-optimism/optimism)

This is a guide to connecting an L2 chain created using OP Stack to Sunrise chain with [Sunrise Data](https://github.com/sunriselayer/sunrise-data). Data Availability layer is supported in Sunrise v0.3.0 and later.

## Sunrise Data

**Before optimism start, set up sunrise-data.** [Sunrise Data Document](sunrise-data.md)

It is recommended to run the full consensus node locally, without relying on an external RPC. [Sunrise Consensus Node Document](../../../run-a-sunrise-node/types/consensus/)

## OP Stack

Start your OP Stack L2 chain with [Alt-DA mode](https://docs.optimism.io/operators/chain-operators/features/alt-da-mode).

Follow the latest documentation. It may be necessary to have a local EVM chain to meet the requirements.

[OP Stack L2 Chain Document](op-stack.md)
