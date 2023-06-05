# Perpetual Futures

Perpetual futures are a type of cryptocurrency trading contract that allows traders to take positions on future price movements. These contracts have no expiration date, and traders are able to maintain positions indefinitely by depositing funds with the exchange.

## Positions

Users can open a perpetual futures position by sending `MsgOpenPosition` tx. There's no fee for opening a position.  
The position can be covered by two types of assets as margin, which are the tokens of the trading pair. If you trade `BTC/USDC` pair, you can deposit BTC or USDC as a margin. The profit will be distributed in the same token as the margin if there's some.  
The created position cannot be modified except for closing a whole in the current implementation.  
And, the liquidation is triggered against each position. The margin of the position cannot be added afterward now. But, this will be supported in the near future.  

The max leverage rate is defined in the params of the protocol for all trading pairs equally. This can be modified through governance voting.

When a position is created, the corresponding amount of token in the pool will be allocated to the position to assure the distribution of the profit for the position. (This could be considered as lending)  

### Liquidation

A position will be liquidated if the losses and fees reduce the margin to the point where:  

$$
RemainingMargin / (Price \times PositionSize / Leverage) \leq MarginMaintenanceRate
$$

MaintenanceMarginRate is defined as a parameter in the protocol. The default value of it is `0.5`.  
The values are all based on `QuoteTicker` of the protocol, in which the default value is `USD`.

This is achieved through any user sending a `MsgReportLiquidation` tx. If the liquidation is needed, The reporter gets a portion of the commission fee based on the remaining margin. The remaining margin is then returned to the position owner after deducting a commission fee.

$$
CommissionFee = RemainingMargin \times CommissionRate
$$

The default value of CommissionRate is `0.001`.

There's no penalty for reporting a position that is not needed to be liquidated.

### Levy Period

Levy Period is set to reduce the imbalance in the positions of the entire market.
If the Long positions are biased in the entire market, a imaginary funding fee will be deducted from the margin of the Long positions and added to the margin of the Short positions. At the same time, commission fees are also subtracted.

$$
ImaginaryFundingFee = PositionSize \times ImaginaryFundingRate
$$

$$
ImaginaryFundingRate = ImaginaryFundingCoefficient \times NetPosition (long - short) / TotalPosition (long + short)
$$

The default value of `imaginary_funding_coefficient` is `0.0005`.

The calculation method for a commission fee is the same as that for the Liquidation.

From the perspective of economics, it can be expressed that this model unifies the conventional funding rate and the time cost of waiting for matchmaking to the imaginary funding rate.

This is achieved through any user sending a `MsgReportLevyPeriod` tx.
If more than 8 hours have passed since the last levy period, this process occurs and the reporter gets a portion of the commission fee based on the remaining margin.

There's no penalty for reporting a position that is not needed to be levied.

## Price Feed

Prices for the accepting token are provided through our pricefeed module.  
Our pricefeed module takes the price data from the restricted addresses which are defined in the protocol in advance.  
The token price is calculated like below:
The price of BTC in the pair of USDC,  
 `price_BTC = price_BTC_USD / price_USDC_USD`  
So, the pricefeed module has the data of BTC price based on USD and USDC price based on USD in this case.  
Price is calculated as the median price of major exchanges for each token. Price will ideally be updated at every block. USDC or other stablecoins are not hard-coded in the protocol.

Price data is treated in this form:

```go
type CurrentPrice struct {
	  MarketId string                                 `protobuf:"bytes,1,opt,name=market_id,json=marketId,proto3" json:"market_id,omitempty" yaml:"market_id"`
	  Price    github_com_cosmos_cosmos_sdk_types.Dec `protobuf:"bytes,2,opt,name=price,proto3,customtype=github.com/cosmos/cosmos-sdk/types.Dec" json:"price" yaml:"price"`
}
```
