# Upgrade

Sunrise is upgraded with on-chain governance.

## Soft Fork

In the case of a soft fork, the chain ID is not changed, and the binary version is changed. In addition, the upgrade handler will handle the process. The details will be described in each upgrade proposal.

Automatic upgrade is available when running Cosmovisor.
See [the Cosmovisor tutorial](setup-cosmovisor.md) for how to set up.

If you do not use CosmoVisor, please change the binaries yourself

## Hard Fork

A hard fork may be executed to apply changes that cannot be accommodated by a soft fork.

`genesis.json` is changed and the new block starts at height 1.
In many cases the chain ID will be changed.

## Testnet

When synchronizing chains from the genesis, follow this guide and use the binary version current at the time of the genesis.
<https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2>

## Mainnet

Coming soon
