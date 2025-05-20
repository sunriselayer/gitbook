# Proof of Liquidity

Proof of Liquidity (PoL) is a novel Sybil resistance mechanism that utilizes a user's history of providing liquidity as the basis for voting power in the network. This approach aligns economic incentives between validators, liquidity providers, and applications in a more sustainable way than traditional models.

## Core Concepts

### Theoretical Foundation

Proof of Liquidity builds upon established DeFi mechanisms while solving key issues:

1. **Beyond ve-Tokenomics**: While ve (vote-escrowed) models like Curve's allow governance participation, PoL integrates liquidity provision directly with network security
2. **Separation of Economic Activities**: PoL uses distinct tokens for consensus security, governance, and transaction fees
3. **Sustainable Incentives**: Unlike traditional DEX inflation models that dilute token value, PoL creates a circular economic system

## Implementation Models

### Berachain Implementation

Berachain pioneered the PoL model with a tri-token design:

- **$BERA**: Transferable token used for transaction fees and staking (security layer)
- **$BGT**: Non-transferable governance token earned by providing liquidity
- **$HONEY**: Stablecoin for value transfer within the ecosystem

**Key Technical Components:**

- Validators stake $BERA to join the consensus set
- Block rewards are paid in $BGT based on validator's "boost" percentage
- "Boost" is calculated from delegated $BGT from token holders
- Validators direct emissions to reward vaults, which distribute $BGT to liquidity providers

**Flow of Value:**

1. Validators stake $BERA as security bond
2. Validators receive $BGT rewards for block production
3. Validators direct $BGT rewards to protocol reward vaults
4. Liquidity providers stake receipt tokens in reward vaults to earn $BGT
5. $BGT holders delegate to validators to boost their rewards
6. Protocols provide incentives to validators to attract emissions

### Sunrise Implementation

Sunrise builds upon PoL concepts with its own architecture:

- **$vRISE**: Non-transferable token for staking and governance
- **$RISE**: Transferable token used as gas and fees

**Technical Implementation:**

- Liquidity providers in the `x/liquiditypool` module earn $vRISE
- $vRISE holders can stake in the `x/staking` module
- Stakers participate in gauge voting through the `x/liquidityincentive` module
- Gauge voters decide which pools receive $vRISE incentives
- Voters earn rewards from pool profits, aligning incentives

## Technical Architecture

### Sunrise Modules

The Sunrise implementation consists of several key modules that interact to create the PoL ecosystem:

```
├── x/liquiditypool     # Core AMM functionality
├── x/liquidityincentive # Gauge voting and incentive distribution
├── x/swap              # Token swap implementation
└── x/staking           # vRISE staking management
```

### Gauge Voting System

The gauge voting system is the cornerstone of PoL implementations:

1. **Epoch-Based Voting**:

- Voting power is determined by staked $vRISE at epoch start
- Each epoch spans a predefined number of blocks (configurable via governance)
- Votes is cleared each time a new epoch is created

1. **Reward Distribution**:

　```
  each_pool_rewards = total rewards (x/liquidityincentive) * pool's voting power / total voting power of all pools
  each_user_rewards = pool rewards * user voting power / pool's voting power
　```

- Emissions are calculated per block
- Distribution based on voted gauge weights and each user's voting power
- Rewards are accumulated in the user's position. Can be claimed at any time

### Consensus Implementation

Sunrise uses CometBFT (Tendermint) for consensus with the following specifications:

- **Maximum Validator Set**: 100 validators
- **Block Time**: ~2 seconds
- **Validator Selection**: Based on stake weight

Future plans include investigating Mysticeti integration to enhance throughput:

```
┌─────────────┐      ┌─────────────┐
│  Mysticeti  │ ──── │    ABCI     │
└─────────────┘      └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Sunrise App │
                    └─────────────┘
```

## Technical Advantages

### Capital Efficiency

Unlike traditional PoS where staked tokens are idle, PoL enables:

- Active capital utilization through liquidity provision
- Dual earning opportunities (staking + liquidity fees)
- Lower opportunity cost for network security

### Economic Alignment

The technical design creates circular dependencies that align incentives:

- Validators need delegated $vRISE/$BGT to maximize rewards
- Applications need validator emissions for liquidity
- Users need to provide liquidity to earn governance tokens

<!-- Berachain-style summary table with icons and token names -->
| Function            | Token(s)                                                                 |
|---------------------|--------------------------------------------------------------------------|
| Security            | <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE + <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE |
| Governance          | <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE |
| Security Emissions  | <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE |
| LP Emissions        | <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE |
| Fee                 | Any (swapped to <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE) |

<!-- Detailed token roles table with icons and token names -->
| Purpose                        | Token(s) Used                                                                 | Notes                                                      |
|--------------------------------|-------------------------------------------------------------------------------|------------------------------------------------------------|
| L1 consensus voting power      | <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE + <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE | Both can be staked for consensus/security                  |
| L1 consensus rewards           | <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE | RISE is distributed as staking rewards                     |
| Transaction fees               | Any (swapped to <img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> RISE) | All fees are ultimately paid in RISE via conversion        |
| Governance proposal voting     | <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE | vRISE is used for on-chain governance voting               |
| Gauge voting power (incentives)| <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE | vRISE is used to allocate liquidity incentives             |
| LP rewards                     | <img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> vRISE, BASE, QUOTE | LPs earn vRISE and swap fees in both pool tokens           |

**Legend:**  
<img src="https://github.com/sunriselayer/brand-kit/raw/main/logo_swarna_32.svg" height="20"/> = RISE  
<img src="https://github.com/sunriselayer/brand-kit/raw/main/vRISE.svg" height="20"/> = vRISE

> **Note:**  
> In Sunrise, the roles and rewards for each token are clearly defined.  
> This clear separation of functions helps prevent dilution of network security when governance or liquidity rewards are distributed.

### Security Considerations

The implementation includes several security measures:

- **Slashing Conditions**: Validators risk losing staked assets for misbehavior
- **Governance Safeguards**: Weighted voting prevents capture
- **Incentive Compatibility**: Economic design disincentivizes attacks

## Implementation Example: Voting Mechanism

Here's a simplified implementation of the gauge voting mechanism in Go:

```go
// Vote structure for gauge voting
type Vote struct {
    Voter      sdk.AccAddress
    GaugeID    uint64
    Percentage sdk.Dec  // 0-1 range representing percentage
}

// ProcessVotes calculates gauge weights for the epoch
func (k Keeper) ProcessVotes(ctx sdk.Context) {
    // Get all votes for the current epoch
    votes := k.GetAllVotes(ctx)
    
    // Calculate voting power per user based on vRISE balance
    votingPowers := make(map[string]sdk.Dec)
    for _, vote := range votes {
        voterAddr := vote.Voter.String()
        balance := k.stakingKeeper.GetBalance(ctx, vote.Voter, "vrise")
        votingPowers[voterAddr] = sdk.NewDecFromInt(balance)
    }
    
    // Calculate pool weights
    poolWeights := make(map[uint64]sdk.Dec)
    for _, vote := range votes {
        voterAddr := vote.Voter.String()
        votingPower := votingPowers[voterAddr]
        weight := votingPower.Mul(vote.Percentage)
        
        poolWeight := poolWeights[vote.GaugeID]
        poolWeight = poolWeight.Add(weight)
        poolWeights[vote.GaugeID] = poolWeight
    }
    
    // Store pool weights for the epoch
    k.SetPoolWeightsForEpoch(ctx, poolWeights)
}
```

## Integration with DeFi Ecosystem

The PoL mechanism integrates deeply with the DeFi ecosystem through:

1. **AMM Integration**: Liquidity pools serve dual purpose for trading and consensus
2. **Receipt Token Staking**: LP tokens become productive assets in reward vaults
3. **Protocol Competition**: Applications compete for emissions by offering incentives

This creates a competitive ecosystem where applications are motivated to provide better economics to attract liquidity, which in turn secures the network.

## Performance Considerations

PoL implementations must balance several performance factors:

- **Epoch Length**: Longer epochs reduce computational overhead but decrease responsiveness
- **Validator Set Size**: Larger sets increase decentralization but may impact consensus speed
- **Vote Processing**: Batch processing of votes at epoch boundaries to minimize gas costs
- **Receipt Token Calculations**: Optimized tracking of liquidity positions and reward distribution

## Future Directions

Several technical enhancements are being explored:

1. **Mysticeti Integration**: Investigating the adoption of Mysticeti consensus to enhance throughput
2. **Cross-Chain Gauges**: Enabling voting for liquidity on connected chains
3. **Dynamic Emission Schedules**: Algorithmic adjustment of emissions based on network metrics
4. **Advanced Reward Mechanisms**: More sophisticated reward distribution using bonding curves

## References

- [Berachain: Flow of Value](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer)
- [ve(3,3) Tokenomics](https://andrecronje.medium.com/ve-3-3-44466eaa088b)
- [Curve Finance ve-Token Model](https://curve.fi/files/CurveDAO.pdf)
- [Mysticeti Consensus](https://sui.io/mysticeti)
