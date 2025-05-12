---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

<p align="center">
  ☀️ <strong>The base layer for Inter‑liquid rollups</strong>
</p>

Sunrise is a modular **Data‑Availability (DA) platform** that integrates **Proof of Liquidity (PoL)** and **fee abstraction**, delivering immediate liquidity and flexible gas‑payment options to rollups and application chains. Liquidity providers stake LP tokens to secure the network and, in return, receive "blobspace" for data publication—aligning economic incentives with network security. Sunrise interoperates with both the [Rollkit](https://rollkit.dev/) framework for sovereign rollups and the [OP Stack](https://stack.optimism.io/) for Ethereum‑settled chains, allowing developers to adopt Sunrise DA with minimal integration effort.

The reference rollup **[Gluon](https://github.com/sunriselayer/gluon)** demonstrates Sunrise in production. Gluon functions as an order‑book rollup on the Sunrise L1, combining web‑style authentication, off‑chain order matching, on‑chain settlement, and IBC‑based asset transfer. Liquidity contributed to Gluon is reflected back into Sunrise through PoL, thereby increasing both liquidity depth and data‑availability capacity while reducing overall value extraction compared with traditional alternative‑DA solutions.

{% hint style="warning" %}
Feature requests or ideas? Open a thread on our <a href="https://github.com/orgs/sunriselayer/discussions" target="_blank">GitHub Discussions</a>.
{% endhint %}

## Key Features

| Feature | Description |
|---|---|
| **Proof of Liquidity (PoL)** | Validators stake LP tokens, not idle coins, aligning security *and* liquidity. Earn rewards from both staking and trading fees. |
| **Fee Abstraction** | Any token can pay gas; Sunrise swaps a tiny slice to \$RISE under the hood. No need to hold multiple tokens for gas. |
| **Off‑chain Blobspace** | Large blobs propagate off‑chain and reach availability in two blocks (< 15 s). Optimized for high‑throughput rollups. |

## Blazing Fast Data Availability

Sunrise’s off‑chain DA design unlocks unmatched throughput and cost‑efficiency without sacrificing on‑chain security.

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
2. **Instant liquidity** – Provide LP once and earn blobspace + vRISE gauge rewards.  
3. **Rollkit / OP‑Stack ready** – Drop‑in adapters for sovereign or Ethereum‑settled rollups.  

## Core Modules

| Module | Purpose |
|--------|---------|
| [`x/da`](learn/sunrise/data-availability.md) | blob publishing, sampling, proofs |
| [`x/liquiditypool`](learn/sunrise/liquidity-pool.md) | PoL pools & LP tokens |
| [`x/liquidityincentive`](learn/sunrise/liquidity-incentive.md) | vRISE gauges, emission schedule |
| [`x/swap`](learn/sunrise/swap.md) | AMM router used by fee‑swap |
| [`x/tokenconverter`](learn/sunrise/token-converter.md) | cross‑denom conversions, IBC hooks |
| [`x/fee`](learn/sunrise/fee.md) | fee abstraction & revenue split |

## Revenue Streams

- **Tx fees** – paid in \$RISE after auto‑swap (0.1% of transaction value)  
- **Swap fees** – accrued by PoL pools (0.3% per swap)  
- **MEV share** – captured via [Skip Protocol](https://docs.skip.money/) (up to 90% of MEV)  

> Gauge voters decide how each stream is split between LPs, stakers, and the treasury.

## Next Steps

| Action | Link |
|---|---|
| **Install a node** | [Node Setup Guide](node/types/consensus/README.md) |
| **Launch a rollup** | [Rollkit Guide](build/l2-blockchains/rollkit/README.md) |
| **Become a validator** | [Validator Guide](build/validators/README.md) |
| **Join Discord** | [Discord Community](https://discord.gg/sunriselayer) |
