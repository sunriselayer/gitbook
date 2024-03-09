# Interest Rate Swap

Gluon serves a functionality to swap interest rate.
It enables users to have fixed yield position or leveraged variable yield position for an interchain yield.

## Mechanism

The fixed yield rate will be realized by using zero coupon bond.
The basic mechanism is similar to Pendle finance.

## Strategies

Strategies can be extended by using CosmWasm smart contract.
For example, stATOM strategy that is implemented by CosmWasm smart contract can be used for the fixed yield position of ATOM staking reward.
