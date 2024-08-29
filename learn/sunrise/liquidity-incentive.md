# Liquidity Incentive

The module `x/liquiditincentive` serves the functionalities to distirbute incentive rewards for liquidity providers in Liquidity Pools.

## Epoch

Each epoch has these parameters

* `start_block`
* `end_block`
* `gauges`

### Gauge

Each gauge is linked to a Liquidity pool with the following parameters.

* `pool_id`
* `previous_epoch_id`
* `ratio`

`previous_epoch_id` is usually the previous epoch. And, `ratio` is the Voting Power voted for that gauge.

## MsgVoteGauge

Users can vote for the gauge.

* `weights`: The list of what Percentage of voting power to vote for the gauge.

The sum of the weights must be less than or equal to 1 (100%).

## Tally of votes

The votes will be tallied at the start of each epoch.

1. Tally the votes by validators. The validator votes include delegated voting power.
1. Tally the non-validated ballots. If the address is delegated to a validator, its own voting power is deducted from the validator's votes.

### Example

#### Addresses

Validator A 1000vRISE
Delegator B 200vRISE (100vRISE delegated to Validator A)

#### Pools

Liquidity Pool #1
Liquidity Pool #2

#### Votes

A votes Pool #1 & #2 (50% & 50%)
B votes Pool #1 (100%)

#### Result

1. Only A voted
Pool #1's voting power: 550vRISE
Pool #2's voting power: 550vRISE

2. A & B voted
Pool #1's voting power: 700vRISE (500 + 200)
Pool #2's voting power: 650vRISE
