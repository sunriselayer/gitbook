# DA Fee Abstraction

Sunrise realizes "DA Fee Abstraction". Developers can use the blob spaces of Sunrise without fee only by providing liquidity to the liquidity pool on Sunrise.

## How it works

- Users will mint LP tokens in the `x/liquiditypool` module for the pool they like.
- Users will receive $vRISE token for the reward.
- Users can use $vRISE for the fee of txs for Data Availability.
  - For other txs, users need to pay the fee with $RISE token.
