# Proof of Liquidity

Proof of Liquidity sybil resistance mechanism utilizes the history of providing liquidity for the voting power in the network.

## Gauge voting

Many DEXs have a gauge voting system to incentivize the liquidity providers. Typically the incentive is given by the inflation of the native token of the DEX, and it is not sustainable.

There is an example of [Pancake Swap Docs](https://docs.pancakeswap.finance/products/vecake/gauges-voting)

## ve(3,3)

The model "ve(3,3)" is an enhanced version of the model "ve" by combining the idea of the model "(3,3)". It contains a gauge voting system with "ve" voting mechanism, but the novelty of this mechanism is that the voter for each pool can get a reward from the profit of the pool. This mechanism incentivizes stakers to vote for the pool which has the potential to get more profit.

## Berachain model

- `$BGT`: Non transferrable token for staking.
- `$BERA`: Transferrable token for a fee.

The blog [Flow of Value](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer) by Berachain is a good resource for understanding the model.

The important point of the model is

- By making the staking token `$BGT` non transferrable. It enables the utilization of the staking token purely for staking without the need for holding it for the fee.
- The inflation rewards will be distributed with `$BGT` token which doesn't lead to the dilution of `$BERA` token.
- There is no interest in dApps on Ethereum for the sustainability of the DEXs, whereas the dApps on Berachain are always interested in the engagement of Berachain PoL.

## Sunrise model

The Sunrise model incorporates and builds upon selected historical developments and evolutionary trajectories within its underlying architecture and design principles.

- `$vRISE`: Non transferrable token for staking.
- `$RISE`: STransferrable token for a fee.

The flow will be like this:

- Some users provide liquidity in the `x/liquiditypool` module.
  - They will get `$vRISE` for the reward.
- Some users stake `$vRISE` token in the `x/staking` module
- People who have voting power can vote for the pool in the `x/liquidityincentive` module which pool should get `$vRISE` for the incentive for liquidity providers.
- The voter for each pool will receive the reward from the profit of the pool.

Sunrise PoL inherits the perspective of Berachain that "dApps that use Sunrise DA are interested in the engagement of Sunrise PoL".

## How to stake $vRISE

- Sunrise Web App

## Specs

- Consensus algorithm: CometBFT (Tendermint)
  - Investigation for Mysticeti is in progress.
- Blockchain application framework: Cosmos SDK v0.50.2
- Maximum validator set size: 100

### Mysticeti

[Mysticeti](https://sui.io/mysticeti) is the latest consensus protocol adopted in the next version of Sui.

Our basic idea is same to the [article](https://www.paradigm.xyz/2022/07/experiment-narwhal-bullshark-cosmos-stack) which Paradigm tried PoC to use Narwhal and Bullshark with ABCI.

We are investigating the adoption of Mysticeti to ABCI and further Sunrise, to enhance the throughput of Sunrise.
