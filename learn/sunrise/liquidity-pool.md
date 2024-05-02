# Liquidity Pool

The module `x/liquiditypool` is for minting LP tokens of `XXX/SR` with AMM mechanism. LP tokens can be used for Proof of Liquidity for Sunrise L1, and also can be used for Sovereign Proof of Liquidity for L2s on Sunrise.

This module supports Concentrated Liquidity while the LP tokens are still fungible.

## Notions

### Pair

Before creating the pool, the pair of tokens have to be registered. The notion of `1` Pair will be linked to `N` Pools.

There are some restrictions for the pair registration while the pair consists of `base_token / quote_token`:

* `$SR` can't be the base token.
* If the quote token is not `$SR`, the pair  `quote_token / $SR` must be registered.

These rules enable the calculation of `$SR` converted value of LP tokens by using [TWAP](liquidity-pool.md#twap) to use them in [Proof of Liquidity](proof-of-liquidity.md).

### Pool

In contrast to Uniswap V3, each user can't designate the range of providing concentrated liquidity in the same pool. Each pool has a fixed range of liquidity provision, and users will decide which pool to provide liquidity. This design enables making the LP tokens fungible.

The range of the concentrated liquidity can be changed and the funds can be rebalanced by the governance in `x/group` module for each pool.

#### Mathematics

To mitigate the calculation cost on the chain, each pool `i` of token pair `X` and `Y` contains the information of the fuction

$$
\left\{ \begin{aligned}
  f_i^x(y_i, k_i) &= 0 \\
  f_i^y(x_i, k_i) &= 0 \\
  f_i^k(x_i, y_i) &= 0
\end{aligned}\right.
$$

where

* `x_i` is the amount of token `X` in the pool `i`
* `y_i` is the amount of token `Y` in the pool `i`
* `k_i` is the constant value of the pool `i`

All equations are the explicit form of the single implicit function

$$
  f_i(x_i, y_i, k_i) = 0
$$

where

* `f_i` is the function that uniquely determines the range and allocation of the liquidity in pool `i`.

Then, the change of token amounts can be described as below

$$
\begin{aligned}
  dx_i(y_i, dy_i, k_i) &= \left( f_i^x(y_i + dy_i, k_i) - f_i^x(y_i, k_i) \right) \\
  dy_i(x_i, dx_i, k_i) &= \left( f_i^y(x_i + dx_i, k_i) - f_i^y(x_i, k_i) \right)
\end{aligned}
$$

where

* `dx_i` is the change of token `X` amount in the pool `i`
* `dy_i` is the change of token `Y` amount in the pool `i`

To find the optimal weights `w_i` to maximize the amount to receive, the following optimization problem can be solved for each case with `r_i` that is the fee rate of the pool `i`

##### Send exact amount of token `X` to pools (`dx > 0`)

$$
  \mathbf{w}^* = \left\{ \begin{aligned}
    \argmax_{\mathbf{w}} & \ -(1-r_i)\sum_i dy_i(x_i, w_i dx, k_i) \\
    \text{s.t.} & \ \sum_i w_i = 1 \end{aligned}
  \right.
$$

##### Receive exact amount of token `X` from pools (`dx < 0`)

$$
  \mathbf{w}^* = \left\{ \begin{aligned}
    \argmin_{\mathbf{w}} & \ \sum_i dy_i(x_i, w_i dx / (1-r_i), k_i) \\
    \text{s.t.} & \ \sum_i w_i = 1 \end{aligned}
  \right.
$$

##### Send exact amount of token `Y` to pools (`dy > 0`)

$$
  \mathbf{w}^* = \left\{ \begin{aligned}
    \argmax_{\mathbf{w}} & \ -(1-r_i)\sum_i dx_i(y_i, w_i dy, k_i) \\
    \text{s.t.} & \ \sum_i w_i = 1 \end{aligned}
  \right.
$$

##### Receive exact amount of token `Y` from pools (`dy < 0`)

$$
  \mathbf{w}^* = \left\{ \begin{aligned}
    \argmin_{\mathbf{w}} & \ \sum_i dx_i(y_i, w_i dy / (1-r_i), k_i) \\
    \text{s.t.} & \ \sum_i w_i = 1 \end{aligned}
  \right.
$$

These calculation can be done in the client side, then the load on the chain can be reduced because the chain side only need to receive the weight `w` to execute the optimal swap.

### TWAP

Sunrise chain will record the last prices of the pool periodically, and they will be used for calculating Time Weighted Average Price. TWAP will be utilized for calculating the voting power from the LP tokens by using the price ratio to `$SR` token.

### Msgs

#### MsgSwapExactAmountIn

This message can contain the array of the pairs.

```yml
- sender: string
- input_amount: sdk.Int
- min_output_amount: sdk.Int
- pair_info: []SwapPairInfo
  - index
    - base_denom: string
    - quote_denom: string
    - pool_weights: []PoolWeight
      - index
        - pool_id: uint64
        - weight: sdk.LegacyDec
```

#### MsgSwapExactAmountOut

This message can't contain the array of the pairs.

```yml
- sender: string
- output_amount: sdk.Int
- max_input_amount: *sdk.Int
- pair_info: SwapPairInfo
  - base_denom: string
  - quote_denom: string
  - pool_weights: []PoolWeight
    - index
      - pool_id: uint64
      - weight: sdk.LegacyDec
```

#### MsgJoinPool

```yml
- sender: string
- pool_id: uint64
- base_amount: sdk.Coin
- quote_amount: sdk.Coin
- min_share_amount: sdk.Int
```

#### MsgExitPool

```yml
- sender: string
- pool_id: uint64
- share_amount: sdk.Int
- min_base_amount: sdk.Coin
- min_quote_amount: sdk.Coin
```

#### MsgCreatePool

```yml
- creator: string
- admin: string
- base_denom: string
- quote_denom: string
- fee_rate: sdk.LegacyDec
- f_x: string
- f_y: string
- f_k: string
```
