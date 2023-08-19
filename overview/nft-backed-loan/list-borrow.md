# List and Borrow

## List NFT

The NFT owner who wants to collateralize NFT to borrow assets, lists their NFT. The deposited amount of bids is the amount of tokens that can be borrowed.

## Borrow

The lister can borrow tokens when there are bids for the NFT.
If the lister fail to to return borrowed tokens before the bid expires, liquidation process will be executed.

### Borrowable amount

To define the borrowable amount, we have to define the "maximal repayment amount" at first.
This is taking interest in consideration on the basis of borrowable amount.

Maximal repayment amount will be same to minimum settlement amount.
It means that,

Minimum settlement amount can be calculated by the following algorithm.
This is TypeScript-like pseudo code.

```typescript
function minimumSettlementAmount(bidsSortedByPrice: Bid[]) {
  if (bidsSortedByPrice.length === 0) {
    return 0;
  }
  let minimumSettlementAmount = 0;
  let forfeitedDeposit = 0;

  for (const bid of bidsSortedByPrice) {
    if (minimumSettlementAmount === 0 || bid.price + forfeitedDeposit < minimumSettlementAmount) {
        minimumSettlementAmount = bid.price + forfeitedDeposit;
    }
    forfeitedDeposit += bid.deposit;
  }
  if (forfeitedDeposit < minimumSettlementAmount) {
    minimumSettlementAmount = forfeitedDeposit;
  }

  return minimumSettlementAmount;
}
```

You can ignore the code. You don't need to understand it.
It means that, minimum settlement amount is the minimum amount that protocol can collect from bidders, in any case of whichever bidders respond to the settlement process.

Don't worry, the web app will show the maximum amount that you can borrow.
It is enough to know that there is a certain algorithm to calculate the maximum amount you can borrow.

### Selling decision

If you find a bid with good price, you can sell your NFT to the bidder immediately.

### Auto Re-refinancing

Auto Re-refinancing is a feature that automatically refinances the borrowed deposit of a listed bid when its expiration date is reached, preventing liquidation from occurring. This function requires another bid to be available, and the amount that can be borrowed from that bid must exceed the amount to be refinanced. The criteria for selecting the deposit to refinance is that the auto refinancing is performed in order of the lowest interest rate.
The lister sets this when listing.
