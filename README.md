---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise

**Our documentation is under construction and is being updated regularly, please check back for updates.**

Sunrise is a specialized Data Availability (DA) Layer for Proof of Liquidity and Fee Abstraction, supporting the modular paradigm by allowing developers to build rollups/apps with enhanced security and liquidity.\
\
Sunrise extend's Berachain's Proof of Liquidity (PoL) model to rollups and L2s, while retaining compabitility with Celestia architecture. A modular cross-chain yield hub (Gluon) is deployed as a Sovereign Rollup (L2) onto the Sunrise L1 blockchain. This yield hub and Sunrise communicate directly to enable the provision of liquidity (replication of PoL) in exchange for blobspace, allowing for a scaling solution with less net-value extract than pre-existing AltDA providers. PoL on Sunrise mutually increases security and liquidity for both the rollup and Sunrise, a parrallel flywheel effect to PoL as seen on Berachain.

Compatibility with Celestia architecture minimizes onboarding difficulty for rollups. This also means that Sunrise is natively IBC compatible. Rollup-as-a-Service (RaaS) providers who integrated Celestia can integrate Sunrise easily, and Rollup SDKs (e.g. OP stack, Polygon CDK, Rollkit, Sovereign SDK, etc.) that support Celestia, will automatically be compatible with Sunrise.

## Sunrise Functions

Celestia-compatible functions:

* Blob Tx
* BlobStream

Sunrise unique functions:

* Proof of Liquidity (PoL)
* DA Fee Abstraction
* Off Chain Blob Data Availability (Sunrise DA v2)
* Sovereign Proof of Liquidity via Gluon

### Proof of Liquidity x Data Availability

Sunrise utilizes Proof of Liquidity to enhance the DA experience, while providing a mutually beneficial environment to increase the liquidity and sovereignty of both L2s on Sunrise, and the Sunrise L1 itself.

Sunrise can also incentivize the DA network whereas other DA networks depend on altruism or voluntary contributions, thus enabling Sunrise to enhance the throughput of the DA network. This feature and the incentive for optional long term data availability enables developers to build not only scalable L2s but also explore fully on-chain new technologies like AI, Gaming, and more.

### Why should developers use Sunrise?

* Users can utilize DA by liquidity providing without the need for a fee.
* While numerous DEXs already exist, they offer limited differentiation for token issuers. L2 developers will always need to provide liquidity despite Sunrise's existence. However, by providing liquidity to Sunrise's DEX, token issuers gain access to additional utilities through Sunrise's DA, incentivizing them to choose Sunrise over other DA Layers and DEXs that lack comparable benefits.

### Integration Stages

### Sunrise v1: Awakening

* `x/blob` module
* `x/blobstream` module
* `x/tokenconverter` module
* `x/liquiditypool` module
* `x/liquidityincentive` module
* `x/swap` module
* `x/fee` module

### Sunrise v2

* Off Chain Blob Data Availability (Sunrise DA v2)
* Sovereign Proof of Liquidity via Gluon

### Revenue (Fee Structure)

The protocol generates revenue through three distinct streams.

* Transaction fees
* Swap fees in the liquidity pool
* MEV captured with [Skip Protocol](https://docs.skip.money/)
