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
| **Off‑chain Blobspace** | Large blobs propagate off‑chain and reach availability in two blocks (< 15 s). Optimized for high-throughput rollups. |

## Why build on Sunrise?

1. **Gasless onboarding** – Users don't need a special gas token; your project's token works.  
2. **Instant liquidity** – Provide LP once and earn blobspace + vRISE gauge rewards.  
3. **Rollkit / OP‑Stack ready** – Drop‑in adapters for sovereign or Ethereum‑settled rollups.  

## Core Modules

<div style="display: flex; gap: 24px; flex-wrap: wrap;">
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/data-availability.md"><strong>x/da</strong></a>
    <p>blob publishing, sampling, proofs</p>
  </div>
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/liquidity-pool.md"><strong>x/liquiditypool</strong></a>
    <p>PoL pools & LP tokens</p>
  </div>
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/liquidity-incentive.md"><strong>x/liquidityincentive</strong></a>
    <p>vRISE gauges, emission schedule</p>
  </div>
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/swap.md"><strong>x/swap</strong></a>
    <p>AMM router used by fee‑swap</p>
  </div>
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/token-converter.md"><strong>x/tokenconverter</strong></a>
    <p>cross‑denom conversions, IBC hooks</p>
  </div>
  <div style="background: #181A20; border-radius: 16px; padding: 24px; width: 300px; box-shadow: 0 2px 8px #0002;">
    <a href="learn/sunrise/fee.md"><strong>x/fee</strong></a>
    <p>fee abstraction & revenue split</p>
  </div>
</div>

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

---
