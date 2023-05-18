# Place Bid (NFT Backed Loan)

## Bid Parameters

- Bid Amount
  This is the asking price to purchase NFT. If the lister decides to sell at this price, you can buy at this price.
- Deposit Amount
  Deposit to be paid at the time of bidding. Must exceed minimum deposit rate.
  {% math %}depositAmount >= bidAmount * minimumDepositRate{% endmath %}
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

- {% math %}i \in I{% endmath %}: index of bids
- {% math %}n = |I|{% endmath %}: number of bids
- {% math %}\{p_i\}_{i \in I}{% endmath %}: the price of {% math %}i{% endmath %} th bid
- {% math %}\{d_i\}_{i \in I}{% endmath %}: the deposit amount of {% math %}i{% endmath %} th bid
- {% math %}\{r_i\}_{i \in I}{% endmath %}: the interest rate of {% math %}i{% endmath %} th bid
- {% math %}\{t_i\}_{i \in I}{% endmath %}: the expiration date of {% math %}i{% endmath %} th bid
- {% math %}q = \frac{1}{n} \sum_{i \in I} p_i{% endmath %}
- {% math %}s = \sum_{i \in I} d_i{% endmath %}: means the amount which lister can borrow with NFT as collateral
- {% math %}\{a_i\}_{i \in I}{% endmath %}: means the amount borrowed from {% math %}i{% endmath %} th bid deposit
- {% math %}b = \sum_{i \in I} a_i{% endmath %}
- {% math %}i_p(j){% endmath %}: means the index of the {% math %}j{% endmath %} th highest price bid
- {% math %}i_d(j){% endmath %}: means the index of the {% math %}j{% endmath %} th highest deposit amount bid
- {% math %}i_r(j){% endmath %}: means the index of the {% math %}j{% endmath %} th lowest interest rate bid
- {% math %}i_t(j){% endmath %}: means the index of the {% math %}j{% endmath %} th farthest expiration date bid
- {% math %}c{% endmath %}: minimum deposit rate

## New bid formulation

When {% math %}(p_{\text{new}}, d_{\text{new}}, r_{\text{new}}, t_{\text{new}}){% endmath %} will be added to the set of bids, the new bids sequence will be

- {% math %}I' = I \cup \{n+1\}{% endmath %}
- {% math %}n' = n + 1{% endmath %}
- {% math %}\{p_i'\}_{i \in I'} = \{p_i\}_{i \in I} \cup \{p_{\text{new}}\}{% endmath %}
- {% math %}\{d_i'\}_{i \in I'} = \{d_i\}_{i \in I} \cup \{d_{\text{new}}\}{% endmath %}
- {% math %}\{r_i'\}_{i \in I'} = \{r_i\}_{i \in I} \cup \{r_{\text{new}}\}{% endmath %}
- {% math %}\{t_i'\}_{i \in I'} = \{t_i\}_{i \in I} \cup \{t_{\text{new}}\}{% endmath %}
- {% math %}q' = \frac{1}{n'} \sum_{i \in I'} p_i'{% endmath %}
- {% math %}s' = \sum_{i \in I'} d_i'{% endmath %}

where the prime means the next state.

The constraint of {% math %}d_{n+1}'{% endmath %} is

{% math %}
  c p_{n+1}' \le d_{n+1}' \le q' - s
{% endmath %}

In easy expression, it means

- {% math %}c p_{n+1}' \le d_{n+1}'{% endmath %}
- {% math %}s' = s + d_{n+1}' \le q'{% endmath %}

where {% math %}c{% endmath %} means minimum deposit rate.
