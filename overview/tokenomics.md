# Tokenomics
## Governance Token Allocation

We absolutely do not do initial coin offerings or token sales. Every token will be distributed in return for your actions like being a validator.

| Usage                                | Percentage of usage / supply  |
| ------------------------------------ | ----------------------------- |
| **Ecosystem Development**            | 30%                           |
| **Assignment for validators**        | 15%                           |
| **Assignment for UnUniFi Project Contributors**      | 15%           |     
| **Assignment for UnUniFi Development Fund**          | 5%            |
| **Marketing**                        | 14%                           |
| **Advisor**                          | 1%                            |
| **Assignment for business partners** | 10%                           |
| **Treasury**                         | 10%                           |

## Protocol Revenue Allocation

### Transaction Fees

Fees will be accumulated in the `FeePool` of `distribution` module in Cosmos SDK.

We will burn all the GUU tokens in the pool via governance proposal.

### Core Module Comission Fees

- `nftbackedloan`
- `yieldaggregator`
- `derivatives`
- `nftfactory`

These module will have a commission fee for some types of transactions. The fee will be accumulated in the `ecosystemincentive` module of UnUniFi.

Generally this fee consists of not only GUU tokens. So it is a "real yield" for the ecosystem.

- 50%
  - Distributed via auction in the future. The auction participants will bid with GUU tokens, to buy the accumulated tokens in the `ecosystemincentive` module.
  - **The GUU tokens that are used to bid will be burned.**
  - Until this auction is ready, the tokens will be locked in the `ecosystemincentive` module.
- 30%
  - Distributed to the stakers (= validators + delegators).
- 10%
  - Distributed to the frontend app developers.
- 10%
  - Distributed to the active users that satisfy some conditions.
