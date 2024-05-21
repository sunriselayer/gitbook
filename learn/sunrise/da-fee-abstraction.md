# DA Fee Abstraction

Sunrise realizes "DA Fee Abstraction". Developers can use the blob spaces of Sunrise without fee only by providing liquidity to the liquidity pool on Sunrise.

## How it works

* Users will mint LP tokens in the `x/liquiditypool` module for the pool they like.
* Users will receive $SSR token for the reward.
* Users can use $SSR for the fee of `BlobTx`.
  * `BlobTx` is the only tx that is allowed to use as a fee in the protocol level.
  * For other txs, users need to pay the fee with $SR token.
