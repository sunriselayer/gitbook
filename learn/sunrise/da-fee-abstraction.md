# DA Fee Abstraction

Sunrise has "DA Fee Abstraction". This feature is realized by `x/blobgrant` module. Developers can use the blob spaces of Sunrise without fee only by providing liquidity to the liquidity pool on Sunrise.

## How it works

* Users register their address in the `x/blobgrant` module with the certain transaction format.
  * Users can designate the another address for posting the blobs without fee.
* Users will mint LP tokens in the `x/liquiditypool` module for the pool they like.
* Then the address for posting the blobs with [`x/blob`](blob.md) module will receive the DA usage grant token.
  * The denom of the grant token is `blobgrant/[expiry]`. It has an expiry date to prevent from the spamming.
  * This is non transferrable token.
