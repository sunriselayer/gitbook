# DA Fee Abstraction

Sunrise has "DA Fee Abstraction". This feature is realized by `x/blobgrant` module. Developers can use the blob spaces of Sunrise without fee only by providing liquidity to the liquidity pool on Sunrise.

## How it works

* Users register their address in the `x/blobgrant` module with a certain transaction format.
  * Users can designate another address for posting the blobs without a fee.
* Users will mint LP tokens in the `x/liquiditypool` module for the pool they like.
* Then the address for posting the blobs with [`x/blob`](blob.md) module will receive the DA usage grant.
  * The denomination of the grant token is `blobgrant/gas`.
  * The grant has an expiry block time to prevent spamming.
  * The grant is realized by using `x/feegrant` module of Cosmos SDK.
