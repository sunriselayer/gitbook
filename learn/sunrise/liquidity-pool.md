# Liquidity Pool

The module `x/liquiditypool` is for liquidity poll with concentrated liquidity AMM mechanism.

## Tick

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
