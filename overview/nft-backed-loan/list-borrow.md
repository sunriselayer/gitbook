# List and Borrow

## List NFT

The NFT owner who wants to collateralize NFT to borrow assets, lists their NFT. The deposited amount of bids is the amount of tokens that can be borrowed.

## Borrow

The lister can borrow tokens when there are bids for the NFT.
If the lister fail to to return borrowed tokens before the bid expires, liquidation process will be executed.

### Selling decision

If you find a bid with good price, you can sell your NFT to the bidder immediately.

### Auto Re-refinancing

Auto Re-refinancing is a feature that automatically refinances the borrowed deposit of a listed bid when its expiration date is reached, preventing liquidation from occurring. This function requires another bid to be available, and the amount that can be borrowed from that bid must exceed the amount to be refinanced. The criteria for selecting the deposit to refinance is that the auto refinancing is performed in order of the lowest interest rate.
The lister sets this when listing.
