# Gauges Voting

## What is a Gauge?

A Gauge means our product that issues vRISE.
The Gauge's first product in Sunrise is the Liquidity Pool.

vRISE holders use vRISE to vote and determine how much vRISE to allocate to which gauge.
More vRISE newly issued will be allocated to the liquidity pool linked to the gauge that has collected more vRISE voting power.

## How to Vote?

### Epoch

Gauges weight voting is conducted for each block determined by the parameters.
When the next Epoch begins, the votes that exist at that time are counted.

### Eligible

For voting gauges, vRISE must first be earned. vRISE is earned primarily by supplying liquidity to liquidity pools.

The valid vRISE balance at the start of the epoch will be used for voting. Locked vRISE will not be reflected.

{% hint style="info" %}
Voting is possible even if you do not have vRISE; your vRISE balance at the start of Epoch will be reflected.
{% endhint %}

### Current Voting Result

Go to "View Current Gauges Voting" on the Governance tab.

- Current Votes
  - Epoch Blocks
How many blocks the Epoch is updated. It is determined by on-chain governance.
  - Staking Rewards Ratio
What percentage of vRISE originally issued to Staking is allocated to gauges. It is determined by on-chain governance.
  - Votes Cast
How many people are voting.

- Current Epoch

  - Total Votes
  - Start
  - End
  - Previous Epoch

At the bottom, there is a complete list of every voting gauges.
"Votes" displays the voting power of each gauge and its percentage of the total.

{% hint style="warning" %}
Only two Epochs exist in the chain, "Current" and "Previous". The previous Epochs are deleted, so the information can no longer be referenced.
{% endhint %}

### Add gauges to vote

To vote on a gauge, click `My Votes`.
Click "Select Pool" and select any pool from the pop-up.

If you have already voted for gauges, your current voting status will be automatically filled in.
To stop voting for a gauge, click the delete button.

### Select how much % vRISE to vote on each gauges

Once you have added the gauges, you may select how much % of your vRISE goes to each of the gauges.

- vRISE balances fluctuate. Locking, incentive grants, and etc. The voter's balance at the start of each epoch is not known, so a percentage must be specified.
- It is troublesome to re-vote in every upcoming epoch. Therefore, gauges voting is designed to carry your voting decisions throughout all the upcoming epoch until you cast a new one.

"Preview Vote" displays the amount of votes for each gauge on the current balance.

Once you have confirmed your decision, click `Vote` to send the transaction.

### Update your vote

Once your vote is submitted, you may see your votes being updated to "My Gauge Votes".
Votes can be updated at any time and the latest vote will be applied at the start of the epoch.

To update your vote decision, click `Vote` to send the transaction again.
