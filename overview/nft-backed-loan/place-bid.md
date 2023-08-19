# Place Bid (NFT Backed Loan)

## Bid Parameters

- Bid Amount

  This is the asking price to purchase NFT. If the lister decides to sell at this price, you can buy at this price.

- Deposit Amount

  Deposit to be paid at the time of bidding. Must exceed minimum deposit rate.

  $$
  depositAmount \geq bidAmount \times minimumDepositRate
  $$

- Interest Rate

  Set the annual interest rate to lend.

- Expiration Date

  Bid expiration date. If the lister borrowed from this bid, it will be repaid by this deadline.

- Auto Payment (Default enable)

### Auto Payment

Auto Payment is a feature that automatically pays the liquidation amount when the auction's liquidation occurs for a bid.
The bidder sets this when bidding.
If there are insufficient balances at the time of liquidation, manual payment will be required.

## Liquidation process

If the borrowed tokens are not returned by the bid's expiration date, a liquidation of the auction occurs.

- The bidder must pay the remaining amount to settle (bid price - deposit price) by the payment deadline.
- If the bidder does not pay the remaining amount, the deposit amount will be forfeited.
- The winning bidder is determined by verifying the payment in descending order of deposit amount (not bid price), and the winning bidder is established once the payment is confirmed.
- The guaranteed winning amount for the lister is only the total deposit price.
- Unsuccessful bidders will have their deposits returned.
- If interest accrues for the bidder, interest will be paid under the following conditions:
  - If deposit interest < (winning bid amount - winning bidder's deposit amount): the bidder receives the full interest amount
  - If deposit interest > (winning bid amount - winning bidder's deposit amount): the bidder receives a portion of the interest based on the proportion of all interest at the time of liquidation
- If no bidder pays the liquidation amount, the NFT and the total deposit amount become the property of the lister.
