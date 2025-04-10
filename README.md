---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise

**Our documentation is under construction and is being updated regularly, please check back for updates.**

{% hint style="info" %}
For feature requests and suggestions, please visit our <a href="https://github.com/orgs/sunriselayer/discussions" target="_blank">GitHub Discussions page</a>
{% endhint %}

Sunrise is a specialized Data Availability (DA) Layer for Proof of Liquidity and Fee Abstraction, supporting the modular paradigm by allowing developers to build rollups/apps with enhanced security and liquidity.

Sunrise extends Berachain’s Proof of Liquidity (PoL) model to rollups and L2s, featuring a flexible modular design compatible with Rollkit and OP Stack. Gluon is deployed as a Sovereign Rollup (L2) onto the Sunrise L1 blockchain, functioning as an orderbook-style trading platform. It features web2-like user authentication, an off-chain order matching engine with on-chain settlement, and IBC-based deposit/withdrawal capabilities. Gluon and Sunrise communicate directly to enable the provision of liquidity (replication of PoL) in exchange for blobspace, allowing for a scaling solution with less net-value extract than pre-existing AltDA providers. PoL on Sunrise mutually increases security and liquidity for both the rollup and Sunrise, a parallel flywheel effect to PoL as seen on Berachain.

## Sunrise Functions

- Proof of Liquidity (PoL)
- DA Fee Abstraction
- Off Chain Blob Data Availability (Sunrise DA v2)

### Proof of Liquidity x Data Availability

Sunrise utilizes Proof of Liquidity to enhance the DA experience, while providing a mutually beneficial environment to increase the liquidity and sovereignty of both L2s on Sunrise, and the Sunrise L1 itself.

Sunrise incentivizes the data availability (DA) network primarily through its Proof of Liquidity (PoL) model rather than relying on purely altruistic or voluntary contributions. In practice, users or developers providing liquidity to certain whitelisted pools receive the right to publish data (i.e., blobspace) in return. This shifts DA fees from being paid in a single native token to a more flexible arrangement, where participants lock assets to earn blobspace. Because liquidity providers benefit financially, they have a direct stake in maintaining reliable and secure data availability, aligning incentives across the network.This feature and the incentive for optional long term data availability enables developers to build not only scalable L2s but also explore new fully on-chain  technologies like AI, Gaming, and more.

### Why should developers use Sunrise?

- Users can utilize DA by liquidity providing without the need for a fee.
- While numerous DEXs already exist, they offer limited differentiation for token issuers. L2 developers will always need to provide liquidity despite Sunrise's existence. However, by providing liquidity to Sunrise's DEX, token issuers gain access to additional utilities through Sunrise's DA, incentivizing them to choose Sunrise over other DA Layers and DEXs that lack comparable benefits.

### Modules

- `x/da` module
- `x/tokenconverter` module
- `x/liquiditypool` module
- `x/liquidityincentive` module
- `x/swap` module
- `x/fee` module

### Revenue (Fee Structure)

The protocol generates revenue through three distinct streams.

- Transaction fees
- Swap fees in the liquidity pool
- MEV captured with [Skip Protocol](https://docs.skip.money/)
