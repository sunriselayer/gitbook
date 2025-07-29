# Validators

In addition to producing and verifying blocks, validators on Sunrise play a crucial role in the security and stability of the network. This section provides an overview of a validator's responsibilities, setup, and related operations.

## How to Become a Validator

To become a validator on Sunrise, you must stake a minimum of **1 vRISE**. vRISE is a non-transferable governance token that can only be obtained as an incentive for providing liquidity.

For detailed instructions on creating and setting up a validator, please refer to the following document:

- [How to Become a Validator](./validator.md)

## Key Responsibilities and Setup

### Data Availability Verification

Beyond generating blocks, Sunrise validators have the critical duty of verifying data on the Data Availability (DA) layer that has been flagged as potentially fraudulent.

To automate this verification process, a validator node must constantly run the following three daemons:

1. `sunrised` (Integration with Cosmovisor is recommended)
2. `sunrise-data validator`
3. `IPFS Daemon`

For more details on the DA verification mechanism and setup, please see here:

- [Data Availability Proof](./data-availability-proof.md)

## Self-Delegating RISE

Validators can delegate their own RISE (from either a regular or a locked balance) to themselves. This self-delegation can increase their block production allocation and allow them to earn more staking rewards.

The specific methods for self-delegation are detailed in the following document:

- [Self Delegation](./self-delegation.md)
