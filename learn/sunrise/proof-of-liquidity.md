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

|                      | Function                                |
| -------------------- | --------------------------------------- |
| x/liquiditypool      | Core AMM functionality                  |
| x/liquidityincentive | Gauge voting and incentive distribution |
| x/swap               | Token swap implementation               |
| x/staking            | vRISE staking management                |

### Gauge Voting System

The gauge voting system is the cornerstone of PoL implementations:

1. **Epoch-Based Voting**:

- Voting power is determined by staked $vRISE at epoch start
- Each epoch spans a predefined number of blocks (configurable via governance)
- Votes is cleared each time a new epoch is created

1. **Reward Distribution**:

$$
  \text{pool rewards} = \text{total rewards} \times \text{pool's voting power} / \text{total voting power of all pools}
$$

$$
  \text{user rewards} = \text{pool rewards} \times \text{user voting power} / \text{pool's voting power}
$$

- Emissions are calculated per block
- Distribution based on voted gauge weights and each user's voting power
- Rewards are accumulated in the user's position. Can be claimed at any time

### Consensus Implementation

Sunrise uses CometBFT (Tendermint) for consensus with the following specifications:

- **Maximum Validator Set**: 100 validators
- **Block Time**: ~10 seconds
- **Validator Selection**: Based on stake weight

Future plans include investigating Mysticeti integration to enhance throughput

## Technical Advantages

### Capital Efficiency

Unlike traditional PoS where staked tokens are idle, PoL enables:

- Active capital utilization through liquidity provision
- Dual earning opportunities (staking + liquidity fees)
- Lower opportunity cost for network security

### Economic Alignment

The technical design creates circular dependencies that align incentives:

- Validators need delegated $RISE/$vRISE to maximize rewards
- Applications need validator emissions for liquidity
- Users need to provide liquidity to earn governance tokens
- The inflation rewards will be distributed with $RISE which doesn't lead to the dilution of $vRISE (governance token)

<!-- Berachain-style summary table with icons and token names -->

| Function           | Token(s)                                                                     | Details                                                |
| ------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------ |
| Security           | ![RISE](../../images/RISE.png) RISE + ![vRISE](../../images/vRISE.png) vRISE | Both vRISE & RISE can be staked for Consensus          |
| Governance         | ![vRISE](../../images/vRISE.png) vRISE                                       | vRISE is used for On-chain governance and Gauge Voting |
| Security Emissions | ![RISE](../../images/RISE.png) RISE                                          | RISE is distributed for stakers as consensus rewards   |
| LP Emissions       | ![vRISE](../../images/vRISE.png) vRISE                                       | vRISE is distributed for LPs as incentives             |
| Fee                | Any (swapped to ![RISE](../../images/RISE.png) RISE)                         | RISE is used as a transaction fee                      |

**Legend:**  
![RISE](../../images/RISE.png) = RISE  
![vRISE](../../images/vRISE.png) = vRISE

> **Note:**  
> In Sunrise, the roles and rewards for each token are clearly defined.  
> This clear separation of functions helps prevent dilution of network security when governance or liquidity rewards are distributed.

### Security Considerations

The implementation includes several security measures:

- **Slashing Conditions**: Validators risk losing staked assets for misbehavior
- **Governance Safeguards**: Weighted voting prevents capture
- **Incentive Compatibility**: Economic design disincentivizes attacks

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
