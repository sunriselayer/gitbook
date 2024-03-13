# Interest Rate Swap

Gluon serves as a functionality to swap interest rates. It enables users to have a fixed yield position or leveraged variable yield position for an interchain yield.

## Mechanism

The fixed yield rate will be realized by using zero coupon bond. The basic mechanism is similar to Pendle finance.

## Strategies

Strategies can be extended by using the CosmWasm smart contract. For example, stATOM strategy that is implemented by the CosmWasm smart contract can be used for the fixed yield position of ATOM staking reward.
