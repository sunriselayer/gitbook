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

  Set the interest rates.

- Expiration Date

  Bid expiration date. If the lister borrowed from this bid, it will be repaid by this deadline.

- Auto Payment (Default enable)

### Auto Payment

Auto Payment is a feature that automatically pays the liquidation amount when the auction's liquidation occurs for a bid.
The bidder sets this when bidding.
If there are insufficient balances at the time of liquidation, manual payment will be required.

## Definition

- $i \in I$: index of bids
- $n = |I|$: number of bids
- $\{p_i\}_{i \in I}$: the price of $i$ th bid
- $\{d_i\}_{i \in I}$: the deposit amount of $i$ th bid
- $\{r_i\}_{i \in I}$: the interest rate of $i$ th bid
- $\{t_i\}_{i \in I}$: the expiration date of $i$ th bid
- $q = \frac{1}{n} \sum_{i \in I} p_i$
- $s = \sum_{i \in I} d_i$: means the amount which lister can borrow with NFT as collateral
- $\{a_i\}_{i \in I}$: means the amount borrowed from $i$ th bid deposit
- $b = \sum_{i \in I} a_i$
- $i_p(j)$: means the index of the $j$ th highest price bid
- $i_d(j)$: means the index of the $j$ th highest deposit amount bid
- $i_r(j)$: means the index of the $j$ th lowest interest rate bid
- $i_t(j)$: means the index of the $j$ th farthest expiration date bid
- $c$: minimum deposit rate

## New bid formulation

When $$(p_{\text{new}}, d_{\text{new}}, r_{\text{new}}, t_{\text{new}})$$ will be added to the set of bids, the new bids sequence will be

- $I' = I \cup \{n+1\}$
- $n' = n + 1$
- $\{p_i'\}_{i \in I'} = \{p_i\}_{i \in I} \cup \{p_{\text{new}}\}$
- $\{d_i'\}_{i \in I'} = \{d_i\}_{i \in I} \cup \{d_{\text{new}}\}$
- $\{r_i'\}_{i \in I'} = \{r_i\}_{i \in I} \cup \{r_{\text{new}}\}$
- $\{t_i'\}_{i \in I'} = \{t_i\}_{i \in I} \cup \{t_{\text{new}}\}$
- $q' = \frac{1}{n'} \sum_{i \in I'} p_i'$
- $s' = \sum_{i \in I'} d_i'$

where the prime means the next state.

The constraint of $d_{n+1}'$ is

$$
  c p_{n+1}' \le d_{n+1}' \le q' - s
$$

In easy expression, it means

$$c p_{n+1}' \le d_{n+1}'$$
$$s' = s + d_{n+1}' \le q'$$

where $c$ means minimum deposit rate.
