---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise

☀️ **The base layer for Inter‑liquid rollups**  
Sunrise fuses Data Availability with Proof‑of‑Liquidity, letting builders launch rollups that come pre‑loaded with deep liquidity and fee‑abstraction UX.

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

---
