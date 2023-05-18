# Liquidity Pool

In UnUniFi protocol, liquidity pool is managed through Liquidity Provider Tokens named **DLP**: through the purchase of DLPs, deposits are made into the pool, and through the sale of DLPs, withdrawals are made from the pool.

Derivatives' commission earnings are reflected in the DLP price, and users can be earned by selling the DLP.

## Liquidity Provider Token

Our liquidity provider token's ticker is `DLP`.  
In the backend, it has `udlp` denom, which is the micro unit of `DLP`.

DLP consists of an index of assets used for leverage trading. It can be minted using the assets which the protocol supports and burnt to redeem any index asset. The price for minting and redemption is calculated based on the formulas in the WhitePaper in the section "3.1.1".  
WhitePaper: <https://ununifi.io/assets/download/UnUniFi-Whitepaper.pdf>

Fees earned on the platform are directly added to the pool.　 Therefore, DLP holders can benefit from them as a reward through the increscent of the DLP price.

There's dynamic change of the minting and redemption fee rate at this moment. There's the static rate which is defined in the protocol. And, the actual fee rate also consider the difference of asset proportion between target and actual proportion. The static base fee rate can be modified through the governance voting.
The potential range of those fee rate are below:

```text
mintFeeRate is proportion to max(0, (actualAmountInPool[i] - targetAmount[i]) / targetAmount[i])
redeemFeeRate is proportion to max(0, -(actualAmountInPool[i] - targetAmount[i]) / targetAmount[i])
```

One thing to be noted is that the Liquidity Pool will take the counterpart position of a trader’s order, so, if traders get profit, the pool and at the same time liquidity providers get loss.