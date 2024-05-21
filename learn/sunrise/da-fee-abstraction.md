# DA Fee Abstraction

Sunrise realizes "DA Fee Abstraction". Developers can use the blob spaces of Sunrise without fee only by providing liquidity to the liquidity pool on Sunrise.

## How it works

* Users will mint LP tokens in the `x/liquiditypool` module for the pool they like.
* Users will receive $SSR token for the reward.
* Users can use the blob space by paying $SSR. The conversion to $SR token will be executed internally by `x/tokenconverter` module.
