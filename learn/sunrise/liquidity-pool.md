# Liquidity Pool

This module is for minting LP tokens of `XXX/SR` with AMM mechanism.
LP tokens can be used for Proof of Liquidity for Sunrise L1, and also can be used for Sovereign Proof of Liquidity for L2s on Sunrise.

This module supports Concentrated Liquidity while the LP tokens are still fungible.

## Notions

### Pair

Before creating the pool, the pair of tokens have to be registered.
The notion of `1` Pair will be linked to `N` Pools.

### Pool

In contrast to Uniswap V3, each user can't designate the range of providing the concentrated liquidity in the same pool.
Each pool has a fixed range of liquidity provision, and users will decide which pool to provide liquidity.
This design enables making the LP tokens fungible.

The range of the concentrated liquidity can be changed and the funds can be rebalanced by the governance in `x/group` module for each pool.

#### Tick

It is similar to it of Uniswap V3.
The price $p$ with the tick index $i$ will be

$$
p(i) = 0.00001^i
$$

and users can provide liquidity in the range of

$$
[p(i), p(i+1))
$$

### TWAP

Sunrise chain will record the last prices of the pool periodically, and they will be used for calculating Time Weighted Average Price.
TWAP will be utilized for calculating the voting power from the LP tokens by using the price ratio to `$SR` token.
The LP token of `XXX/USDC` is also able to be used for Proof of Liquidity only if there is a pair of `USDC/SR` and the TWAP of `USDC/SR` is available.
