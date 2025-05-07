# Gauges Voting

The `x/gauges` module is a protocol-level mechanism for managing liquidity incentives and voting power distribution within the Sunrise ecosystem. It provides a flexible and efficient way to allocate rewards and influence protocol decisions based on liquidity provision.

## Key Features

- **Liquidity-Based Voting:** Voting power determined by liquidity provision
- **Epoch-Based Rewards:** Time-based reward distribution periods
- **Flexible Gauge Types:** Support for different types of liquidity gauges
- **Economic Incentives:** Sustainable reward mechanisms

## Core Functionality

> **Note:** The following section covers advanced topics intended for experienced users or developers.

### Gauge Management

The module manages different types of gauges:

- **Liquidity Gauges:** For liquidity pool rewards
- **Staking Gauges:** For staking rewards
- **Custom Gauges:** For protocol-specific rewards

### Voting Power

Voting power is calculated based on:

- Liquidity provided
- Lock duration
- Gauge type
- User's total stake

### Reward Distribution

Rewards are distributed according to:

- Epoch schedule
- Gauge weights
- User's voting power
- Total liquidity in gauge

## Integration Points

### With Other Modules

- **x/liquidity:** For liquidity pool integration
- **x/staking:** For staking reward distribution
- **x/governance:** For gauge parameter management
- **x/rewards:** For reward token distribution

### With External Systems

- **DEXs:** For liquidity pool integration
- **Staking Platforms:** For staking reward distribution
- **Analytics:** For gauge performance tracking

## Parameters

The module's behavior is controlled by several parameters:

- `min_lock_duration`: Minimum duration for locking liquidity
- `max_lock_duration`: Maximum duration for locking liquidity
- `epoch_duration`: Duration of each reward epoch
- `min_voting_power`: Minimum voting power required
- `max_voting_power`: Maximum voting power cap
- `gauge_types`: Supported gauge types

## Example Usage

### Creating a Gauge

```go
// Create a new liquidity gauge
gauge := types.Gauge{
    Id:          "gauge-1",
    Type:        types.GaugeTypeLiquidity,
    StartTime:   ctx.BlockTime(),
    EndTime:     ctx.BlockTime().Add(epochDuration),
    Rewards:     rewards,
    TotalPower:  sdk.ZeroInt(),
    IsActive:    true,
}

err := k.CreateGauge(ctx, gauge)
if err != nil {
    return err
}
```

### Voting on a Gauge

```go
// Vote on a gauge with liquidity
vote := types.Vote{
    GaugeId:    "gauge-1",
    Voter:      voter,
    Power:      power,
    LockEnd:    ctx.BlockTime().Add(lockDuration),
}

err := k.Vote(ctx, vote)
if err != nil {
    return err
}
```

### Distributing Rewards

```go
// Distribute rewards for an epoch
err := k.DistributeRewards(ctx, "gauge-1")
if err != nil {
    return err
}
```

## Benefits

1. **Fair Distribution:** Rewards distributed based on actual contribution
2. **Flexible Incentives:** Support for various reward mechanisms
3. **Sustainable Economics:** Long-term incentive alignment
4. **Transparent Voting:** Clear voting power calculation
5. **Protocol Integration:** Seamless integration with other components

## Future Improvements

1. **Dynamic Gauge Weights:** Implement dynamic weight adjustment based on performance
2. **Advanced Voting Mechanisms:** Support for more complex voting strategies
3. **Cross-Chain Gauges:** Enable cross-chain liquidity incentives
4. **Gauge Analytics:** Better tracking and analysis of gauge performance
5. **User Preferences:** Allow users to set preferences for reward distribution
