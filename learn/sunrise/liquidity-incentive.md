# Liquidity Incentive

The `x/liquidityincentive` module incentivizes liquidity providers by distributing rewards based on their contributions to liquidity pools. It uses an epoch-based reward system and a gauge voting mechanism to allocate rewards dynamically. This module ensures sustainable liquidity provisioning while allowing users to participate in governance through gauge voting.

See the [Bribes](./bribes.md) for more information on the bribe feature.

## Key Features

1. **Epoch-Based Reward Distribution**:
   - Rewards are distributed at the end of each epoch.
   - Lazy accounting minimizes computational overhead by calculating rewards only when claimed.
2. **Gauge Voting**:
   - Users can vote on which liquidity pools should receive incentives.
   - Voting power is determined by **`$vRISE`** tokens (non-transferable staking tokens).
3. **Lazy Accounting for Rewards**:
   - Rewards are tracked using accumulators and distributed only when users claim them.
   - This reduces the computational load on the network.
4. **Dynamic Incentive Allocation**:
   - Incentives are allocated based on pool weights (gauges) determined through voting.

## **Core Concepts**

### Epochs

> **Note:** The following section covers advanced topics intended for experienced users or developers.

- Two epochs exist concurrently:
  1. **Past Epoch**: The epoch that has ended.
  2. **Current Epoch**: The ongoing epoch.
- Each epoch has the following parameters:
  - **`id`**: The unique epoch ID.
  - **`start_block`**: The block where the epoch begins.
  - **`start_time`**: The Unix time where the epoch begins.
  - **`end_block`**: The block where the epoch ends.
  - **`gauges`**: A list of gauges (pool weights) for incentive distribution.

### Gauge

> **Note:** The following section covers advanced topics intended for experienced users or developers.

- A gauge represents a specific liquidity pool's weight in reward allocation.
- Parameters:
  - **`pool_id`**: The ID of the liquidity pool.
  - **`voting_power`**: The voting power allocated to this pool.

### Lazy Accounting

- Rewards are not distributed immediately but are calculated when claimed.
- Formula for calculating rewards:

$$
\text{ClaimAmount}_{ij} = \frac{\text{PositionUnclaimedAccumulation}_{ij}}{\text{PoolUnclaimedAccumulation}_{i}} \times \text{PoolUnclaimed}_{i}
$$

## Workflow

### BeginBlocker

1. Transfers a portion of inflation rewards from the Fee Collector account to the **`x/liquidityincentive`** module account.
1. Rewards are converted to **`$vRISE`** tokens (non-transferable staking tokens).
1. Rewards are accumulated in each pool's fee accumulator.

### MsgClaimRewards (`x/liquiditypool`)

- Users claim rewards by interacting with their positions in liquidity pools.

> **Note:**  
> The rewards discussed here are specifically **Gauge Voting rewards, allocated according to your vRISE voting power**.  
> These are distinct from standard LP rewards.  
> You claim Gauge Voting rewards by participating in Gauge Voting with your vRISE, which determines your share of the rewards for each pool per epoch.

## Sequence Diagram: Reward Distribution

> **Note:** The following section covers advanced topics intended for experienced users or developers.

```mermaid
sequenceDiagram
    participant User as Liquidity Provider
    participant LiquidityPool as x/liquiditypool Module
    participant IncentiveModule as x/liquidityincentive Module
    participant Distribution as x/distribution Module

    User->>LiquidityPool: Provide Liquidity
    LiquidityPool->>IncentiveModule: Track Position Accumulation
    IncentiveModule->>Distribution: Transfer Inflation Rewards
    User->>IncentiveModule: Claim Rewards
    IncentiveModule->>User: Calculate and Distribute Rewards
```

## Parameters

| Parameter            | Default | Units  | Description                                         |
| -------------------- | ------- | ------ | --------------------------------------------------- |
| epoch_blocks         | 4,320   | blocks | Number of blocks per epoch (approximately 12 days)  |
| staking_reward_ratio | 0.50    | ratio  | Ratio of vRISE allocated to staking (50%)           |
| bribe_claim_epochs   | 5       | epochs | Number of epochs during which bribes can be claimed |

### Parameter Details

1. **epoch_blocks**

   - Defines the length of each epoch in blocks
   - Default value is approximately 12 days (`DefaultParams().BlocksPerYear/365*12`)
   - Controls epoch start and end, determining reward distribution timing

2. **staking_reward_ratio**

   - Ratio of newly minted vRISE tokens allocated to staking rewards
   - Default value is 50% (`math.LegacyNewDecWithPrec(50, 2)`)
   - Remaining 50% is used for liquidity incentives

3. **bribe_claim_epochs**
   - Defines the period during which bribes can be claimed in epochs
   - Default value is 5 epochs
   - Bribes cannot be claimed after this period expires

These parameters can be updated through governance. Parameter changes can significantly impact system behavior and should be carefully considered.

## Messages

The module provides various message types:

- MsgUpdateParams: Update module parameters (governance operation)
- MsgStartNewEpoch: Start a new epoch
- MsgVoteGauge: Vote on pool weights for reward distribution
- MsgRegisterBribe: Register a bribe for a specific pool and epoch
- MsgClaimBribes: Claim accumulated bribes

## Queries

The module provides various query endpoints:

- Params: Query module parameters
- Epoch: Get details of a specific epoch
- Epochs: List all epochs
- Vote: Get voting information for a specific address
- Votes: List all votes
- Bribe: Get details of a specific bribe
- Bribes: List all bribes with optional filters
- BribeAllocation: Get bribe allocation for a specific address, epoch, and pool
- BribeAllocations: List all bribe allocations with optional filters
- TallyResult: Get the tally result for the next epoch

See [Github](https://github.com/sunriselayer/sunrise/tree/main/x/liquidityincentive) for details.
