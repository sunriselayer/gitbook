---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise

Sunrise is a specialized Data Availability (DA) Layer for Fee Abstraction and Proof of Liquidity, supporting the modular paradigm by allowing developers to build rollups/apps with enhanced security and liquidity.\
\
Sunrise extend's Berachain's Proof of Liquidity (PoL) model to rollups and L2s, while retaining compabitility with Celestia architecture. A modular cross-chain yield hub (Gluon) is deployed as a Sovereign Rollup (L2) onto the Sunrise L1 blockchain. This yield hub and Sunrise communicate directly to enable the provision of liquidity (replication of PoL) in exchange for blobspace, allowing for a scaling solution with less net-value extract than pre-existing AltDA providers. PoL on Sunrise mutually increases security and liquidity for both the rollup and Sunrise, a parrallel flywheel effect to PoL as seen on Berachain.

Compatibility with Celestia architecture minimizes onboarding difficulty for rollups. This also means that Sunrise is natively IBC compatible. Rollup-as-a-Service (RaaS) providers who integrated Celestia can integrate Sunrise easily, and Rollup SDKs (e.g. OP stack, Polygon CDK, Rollkit, Sovereign SDK, etc.) that support Celestia, will automatically be compatible with Sunrise.

### Sunrise Functions:

Celestia-compatible functions:

* Blob Tx
* BlobStream

Sunrise unique functions:

* DA Fee Abstraction
* Proof of Liquidity (PoL)
* Sovereign Proof of Liquidity (SPoL)
* Incentivization for optional data storage

### Proof of Liquidity x Data Availability

As mentioned above, Sunrise utilizes Proof of Liquidity to enhance the security of the Sunrise L1, and the liquidity and sovereignty of L2s on Sunrise.

Sunrise also has a mechanism to incentivize DA network whereas other DA networks depend on altruism or voluntary contributions, hence Sunrise can enhance the throughput of the DA network. This feature and the incentive for optional long term data availability enables developers to build not only scalable L2s but also full-onchain new technologies like AI, Gaming, and so on.

### Revenue (Fee Structure)

The protocol generates revenue through three distinct streams.

* Transaction fees
* Swap fees in the liquidity pool
* MEV captured with [Skip Protocol](https://docs.skip.money/blocksdk/overview/)

### Why should developers use Sunrise?

* Users can utilize DA by liquidity providing without the need for a fee.
* While numerous DEXs already exist, they offer limited differentiation for token issuers. L2 developers will always need to provide liquidity despite Sunrise's existence. However, by providing liquidity to Sunrise's DEX, token issuers gain access to additional utilities through Sunrise's DA, incentivizing them to choose Sunrise over other DA Layers and DEXs that lack comparable benefits.

### Integration Stages

### Sunrise v1: Minimum Viable Product

* `x/blob` module
* `x/blobstream` module
* `x/liquiditypool` module
* `x/blobgrant` module

### Sunrise v2: Security and Incentive

* `x/liquiditystaking` module
* `x/gauge` module
* `x/votingreward` module
* Sovereign Proof of Liquidity for Sovereign rollups

### Future Integrations (Exploratory)

* DasIncentive
* Long term data persistence
