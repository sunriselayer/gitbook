# NFT Backed Loan

{% hint style="info" %}
This feature is available on the testnet, but does not yet exist on the mainnet.
{% endhint %}

## What is the NFT Backed Loan?

UnUniFi’s NFT Backed Loans dApp allows users to collateralize their NFT assets to access liquidity, while delivering fast, efficient, cross-chain matching between lenders and borrowers. UnUniFi’s unique lending model provides advantages such as low transaction fees, competitive valuations, and support for any NFT. Cross-chain matching also enables liquidity aggregation across chains. Lastly, UnUniFi’s oracle-free valuation mechanism protects retail users against price manipulation and provides valuations with respect to rarity, all based on real-time demand data. This mechanism creates a reliable and scalable NFT valuation service not just for retail users but also for institutional users as well.

### List NFT

The NFT owner publishes the NFT in the Marketplace and collects bids. The deposited amount of bids is the amount of tokens that can be borrowed.

### Bid

In addition to the asking purchase price, you decide on deposit amounts, loan period, and interest rate.

Bidding is subject to restrictions. For more information, visit [Place Bid](nft-backed-loan/place-bid.md) page.

### Borrow

The lister can borrow tokens when there are bids for the NFT.  
Failure to return borrowed tokens before the bid expires will result in liquidation.

For more information about the liquidation, visit [Liquidation](nft-backed-loan/liquidation.md) page.

#### Auto Re-refinancing

Auto Re-refinancing is a feature that automatically refinances the borrowed deposit of a listed bid when its expiration date is reached, preventing liquidation from occurring. This function requires another bid to be available, and the amount that can be borrowed from that bid must exceed the amount to be refinanced. The criteria for selecting the deposit to refinance is that the auto refinancing is performed in order of the lowest interest rate.
The lister sets this when listing.
