---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise

**The base layer for Interliquid Networks.**

Sunrise is a next-generation Layer 1 blockchain that combines high-throughput data availability with a native liquidity hub. It integrates **Proof of Liquidity (PoL)** and **fee abstraction**, delivering immediate liquidity and flexible gas‑payment options to rollups and application chains. Validators secure the network by staking RISE and/or vRISE. Liquidity providers supply liquidity to pools and earn vRISE and trading fees. Sunrise interoperates with [Rollup and L2 Blockchain](./build/l2-blockchains/README.md), allowing developers to adopt Sunrise with minimal integration effort.

{% hint style="warning" %}
Feature requests or ideas? Open a thread on our [GitHub Discussions](https://github.com/orgs/sunriselayer/discussions).
{% endhint %}

## Key Features

| Feature                         | Description                                                                                                                                                                           |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Proof of Liquidity (PoL)**    | Validators secure the network by staking RISE and/or vRISE, aligning security _and_ liquidity. Liquidity providers earn vRISE and trading fees.                                       |
| **Fee Abstraction**             | Any token can pay gas; Sunrise swaps a tiny slice to $RISE under the hood. No need to hold multiple tokens for gas.                                                                   |
| **Off‑chain Data Availability** | Large data blobs are propagated and stored off-chain, while only a metadata URI pointing to these erasure-coded data shares are kept on-chain. Optimized for high-throughput rollups. |

## Blazing Fast Data Availability

Sunrise's off‑chain data availability design unlocks unmatched throughput and cost‑efficiency without sacrificing on‑chain security. Only metadata and coded shards are kept on-chain; full data blobs are distributed and stored off-chain.

1. **Off‑chain Erasure Coding**  
   → Dramatically cuts validator compute & storage: only coded shards live on chain, full data reconstruction happens off‑chain.

2. **Off‑chain Blob Propagation**  
   → Keeps the mempool lightweight and scales to **5 + MB/s**—validators sample availability while nodes fetch or prune blobs on demand.

3. **KZG Commitments**  
   → Cryptographic anchors on‑chain enable sub‑second proof verification and instant challenge resolution.

## Data Availability Features

Sunrise moves heavy data work off‑chain while keeping on‑chain proofs lean and verifiable.

1. **Off‑chain Erasure Coding**

   - Blob data is split and Reed–Solomon encoded outside the chain.
   - Validators store only the 32‑byte double‑hash per shard, cutting disk I/O and memory overhead.

2. **Off‑chain Blob Propagation**

   - Transactions carry only metadata (shard hashes) into the mempool.
   - Full blob payloads are P2P‑distributed via the blob network, supporting sustained **5 MB/s** throughput.
   - Nodes fetch or prune blobs on demand, giving you control over local storage.

3. **KZG Polynomial Commitments**
   - A single on‑chain KZG commitment binds all shards.
   - Verifiers check inclusion in **O(log n)** time with constant‑size proofs (~48 bytes).
   - Rapid challenge/response cycles (< 1 s) ensure data‑availability guarantees.

## Why build on Sunrise?

1. **Gasless onboarding** – Users don't need a special gas token; your project's token works.
2. **Instant liquidity** – Provide liquidity and earn vRISE gauge rewards and trading fees.
3. **Rollkit / OP‑Stack ready** – Drop‑in adapters for sovereign or Ethereum‑settled rollups.

## Core Modules

| Module                                                         | Purpose                                             |
| -------------------------------------------------------------- | --------------------------------------------------- |
| [`x/da`](learn/sunrise/data-availability.md)                   | Data Availlability layer data publication and proof |
| [`x/liquiditypool`](learn/sunrise/liquidity-pool.md)           | PoL pools & Providing liquidity                     |
| [`x/liquidityincentive`](learn/sunrise/liquidity-incentive.md) | Gauge Voting for vRISE allocations & Bribes         |
| [`x/swap`](learn/sunrise/swap.md)                              | AMM router supporting token swap                    |
| [`x/tokenconverter`](learn/sunrise/token-converter.md)         | Conversion from vRISE to RISE                       |
| [`x/fee`](learn/sunrise/fee.md)                                | fee abstraction & revenue split                     |
| [`x/lockup`](learn/sunrise/lockup.md)                          | Locking of RISE for a certain period                |
| [`x/shareclass`](learn/sunrise/shareclass.md)                  | Staking RISE to secure the network                  |

## Revenue Streams

- **Tx fees** – Paid by RISE on sending transactions
- **Swap fees** – Paid to liquidity providers
- **MEV share** – (planned) to be captured via [Skip Protocol](https://docs.skip.money/) (up to 90% of MEV)

## Next Steps

| Action                 | Link                                                    |
| ---------------------- | ------------------------------------------------------- |
| **Install a node**     | [Node Setup Guide](node/types/consensus/README.md)      |
| **Launch a rollup**    | [Rollkit Guide](build/l2-blockchains/rollkit/README.md) |
| **Become a validator** | [Validator Guide](build/validators/README.md)           |
| **Join Discord**       | [Discord Community](https://discord.gg/sunriselayer)    |
