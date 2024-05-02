# Sunrise

Sunrise is an L1 blockchain that serves Data Availability in the modular paradigm.

Sunrise DA layer has compatibility with Celestia's architecture. Rollup-as-a-Service (RaaS) providers who integrated Celestia can integrate Sunrise easily, and Rollup SDKs (e.g. OP stack, Polygon CDK, Rollkit, Sovereign SDK, and so on) which support Celestia, can also support Sunrise easily.

Celestia-compatible features:

* Blob Tx
* BlobStream

In addition, Sunrise has unique features:

* Proof of Liquidity
* DA Fee Abstraction
* Sovereign Proof of Liquidity (SPoL)
* Incentive for optional long term data availability

Sunrise utilizes Proof of Liquidity mechanism to enhance the security of Sunrise L1, and the liquidity and sovereignty of L2s on Sunrise. Sunrise also has a mechanism to incentivize DA network whereas other DA networks depend on altruism or voluntary contributions, hence Sunrise can enhance the throughput of the DA network. This feature and the incentive for optional long term data availability enables developers to build not only scalable L2s but also full-onchain new technologies like AI, Gaming, and so on.

Furthermore, Sunrise is IBC (Inter Blockchain Communication) compatible.

The protocol generates revenue through three distinct streams.

* Transaction fees
* Swap fees in the liquidity pool
* MEV captured with [Skip Protocol](https://docs.skip.money/blocksdk/overview/)

## Why should developers use Sunrise?

* Users can utilize DA by liquidity providing without the need for a fee.
* While numerous DEXs already exist, they offer limited differentiation for token issuers. L2 developers will always need to provide liquidity despite Sunrise's existence. However, by providing liquidity to Sunrise's DEX, token issuers gain access to additional utilities through Sunrise's DA, incentivizing them to choose Sunrise over other DA Layers and DEXs that lack comparable benefits.

## Integration stages

### Sunrise v1: Minimum Viable Product

* `x/blob` module
* `x/blobstream` module
* `x/liquiditypool` module
* `x/blobgrant` module
* Staking supports only `$SR`

### Sunrise v2: Security and Incentive

* `x/liquiditystaking` module
* `x/gauge` module
* `x/votingreward` module
* Sovereign Proof of Liquidity for Sovereign rollups

### Future possibility of the integration

* DasIncentive
* Long term data persistence
