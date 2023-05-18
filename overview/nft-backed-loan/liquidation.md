# Liquidation

If the borrowed tokens are not returned by the bid's expiration date, a liquidation of the auction occurs.

## Process

- The bidder must pay the liquidation amount (bid price - deposit price) by the payment deadline.
- If the bidder does not pay the liquidation amount, the deposit amount will be collected.
- The winning bidder is determined by verifying the payment in descending order of deposit amount (not bid price), and the winning bidder is established once the payment is confirmed.
- The guaranteed winning amount for the lister is only the total deposit price.
- Unsuccessful bidders will have their deposits returned.
- If interest accrues for the bidder, interest will be paid under the following conditions:
  - If deposit interest < (winning bid amount - winning bidder's deposit amount): the bidder receives the full interest amount
  - If deposit interest > (winning bid amount - winning bidder's deposit amount): the bidder receives a portion of the interest based on the proportion of all interest at the time of liquidation
- If no bidder pays the liquidation amount, the NFT and the total deposit amount become the property of the lister.