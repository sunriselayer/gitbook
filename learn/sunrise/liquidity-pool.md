# Liquidity Pool

The module `x/liquiditypool` is for liquidity poll with concentrated liquidity AMM mechanism.

## Pool

Each pool has these parameters

- `denom_base`
- `denom_quote`
- `fee_rate`
- `tick_params`

### Tick

There are two parameters in each pool

- `price_ratio`: typically `1.0001`
- `base_offset`: typically `0` otherwise in `[0, 1)`

The tick-price conversion formula is this:

$$
  \text{price}(\text{tick}) = \text{price\_ratio} ^ {\text{tick} - \text{base\_offset}}
$$

In the typiical case,

$$
  \text{price}(\text{tick}) = 1.0001 ^ {\text{tick}}
$$

and it is same to Uniswap V3.

## Position

Each position has these info

- `lower_tick`: Uniquely determine the min price of the range of the position
- `upper_tick`: Uniquely determine the max price of the range of the position

## MsgCollectFees

Users can claim fee rewards for providing liquidity.

- `position_ids`: The list of position ids to collect fees

## MsgCollectIncentives

Users can claim $SSR token as an incentive for providing liquidity.

- `position_ids`: The list of position ids to collect incentives

## Swap

For sending the tx for swapping tokens, use msgs in `x/swap` module.
