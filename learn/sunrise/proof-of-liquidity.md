# Proof of Liquidity

Proof of Liquidity enable to use LP tokens minted by Liquidity Pool for staking in Sunrise Proof of Stake.
`x/proofofliquidity` module will provide the functionality only for that but Proof of Liquidity ecosystem doesn't consist of itself only.
Proof of Liquidity ecosystem consists of modules `x/liquidityincentive` and `x/liquidityreward` to enhance the engagement of the users and sustainability of the ecosystem.

## Gauge voting

Many DEXs have a gauge voting system to incentivize the liquidity providers.
Typically the incentive is given by the inflation of the native token of the DEX, and it is not sustainable.

There is an example of [Pancake Swap Docs](https://docs.pancakeswap.finance/products/vecake/gauges-voting)

## ve(3,3)

The model "ve(3,3)" is an enhanced version of the model "ve" by combining the idea of the model "(3,3)".
It contains a gauge voting system with "ve" voting mechanism, but the novelty of this mechanism is that the voter for each pool can get reward from the profit of the pool.
This mechanism incentivizes the stakers to vote for the pool which has the potential to get more profit.

## Berachain model

- `$BGT`: Non transferrable token for staking.
- `$BERA`: Transferrable token for fee.

The blog of [Flow of Value](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer) by Berachain is a good resource to understand the model.

The important point of the model is

- Making the staking token `$BGT` non transferrable. It enables to utilize the all supply of the staking token purely for staking without the need for holding it for the fee.
- The inflation rewards will be distributed with `$BGT` token which doesn't lead to the dilution of `$BERA` token.
- There is no interest in dApps on Ethereum for the sustainability of the DEXs, whereas the dApps on Berachain are always interested in the engagement of Berachain PoL.

## Sunrise model

These histories of the evolution are partially intaken in Sunrise model.

- `$SR`: Sunrise native token for staking and fee as you know. It is a transferrable token.
- `$SRGM`: Sunrise governance multiplier. It is a non transferrable token. It multiplies the voting power and the proportion of receiving the profit of the protocol, for `$SR` staking.
- Feeless DA: [BlobGrant](./blobgrant.md) module distribute the grant token for DA usage without fee.

The flow will be like this:

- Some users mint LP tokens in the `x/liquiditypool` module.
- The users the LP tokens in the `x/proofofliquidity` module.
  - They will get `$SRGM` for the reward.
- Some users stake `$SR` token in the `x/staking` module
  - `$SRGM` multiplies the voting power of `$SR` staking (not for LP tokens staking).
- People who have voting power can vote for the pool in the `x/liquidityincentive` module which pool should get `$SRGM` for the incentive for liquidity providers.
- The voter for each pool will receive the reward from the profit of the pool.

We cut off the separation model of the staking token and the fee token because the fee token due to several reasons:

- To enable the native token to capture the large value, the native token should have the right to be used for the staking and governance. Only the utility for the fee is not enough for capturing the value.
- We can enable the Feeless DA for the usage of DA which is the most important feature of Sunrise.
- We can abstract the fee token in the future only if there is a on chain price ratio data of `$SR` token and other tokens to swap internally, and we have it in [Liquidity Pool](./liquidity-pool.md) module as TWAP.

Furthermore, we think the value of `$SR` can coexist with PoL by using `$SRGM` which doesn't enhance the voting power of LP token staking.
It means that `$SRGM` only enhance the voting power and the proportion of receiving the profit of the protocol, for `$SR` staking.

Sunrise PoL inherits the perspective of Berachain that "dApps that use Sunrise DA are interested in the engagement of Sunrise PoL".
