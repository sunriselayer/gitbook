# Validators

- [Validator Node](../../node/types/consensus/validator-node.md)
- [Data Availability Proof](./data-availability-proof.md)
- [Self Delegation](./self-delegation.md)

First, create a validator node. After the validator node is started, blocks are validated and generated.

In Sunrise, validators are responsible for validating data in the Data Availability Layer in addition to generating blocks.
sunrise-data includes code to automate this process, allowing validators to perform the validation work.

Therefore, the validator node must run the following 3 daemons

1. sunrised (Recommended to work with cosmovisor)
1. sunrise-data validator
1. IPFS Daemon
