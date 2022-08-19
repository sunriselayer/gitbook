---
description: >-
  Details of mainnet upgrades, installation block height and links to
  instructions.
---

# Mainnet Upgrades

Release procedures for validators and node operators are explained [here](https://github.com/UnUniFI/chain/blob/main/RELEASES.md). The `RELEASES.md` file in UnUniFi's GitHub repo is the canonical source of truth for release processes.

The UnUniFi Network mainnet is regularly upgraded to provide the latest security patches, Cosmos SDK module integrations and performance improvements.

Some upgrades are able to be undertaken automatically with Cosmovisor while other upgrades need to be manually installed at specified block heights. Others can be installed at any time after their predecessor.

## Upgrade types

There are two types of upgrades that happen on UnUniFi Network. They are:&#x20;

1. **Planned** feature upgrades or planned patches&#x20;
2. **Unplanned** security upgrades.

### Planned upgrade (via governance)

Planned upgrades, as the name suggests, are upgrades that are developed and proposed via governance. If approved by the community, these upgrades are undertaken by the chain automatically halting at the planned upgrade height.&#x20;

Node operators are then required to swap the binary for the planned upgrade binary. After all node operators have upgraded and started their nodes the network will continue in the upgraded state.

### Unplanned upgrade

Where emergency security patches are required, node operators are notified via the official discord validator channels. Node operators will be required to halt their nodes manually at the required upgrade height, swap the patched binary and restart their nodes. After all node operators have upgraded and started their nodes the network will continue in the upgraded state.

### Update Daemon for upgrade

If you want ununifid to upgrade automatically, do the following steps prior to the upgrade height:

```shell
export UPGRADE_NAME= # upgrade name
export NEW_VERSION= # release version for upgrade

mkdir -p $DAEMON_HOME/cosmovisor/upgrades/$UPGRADE_NAME/bin
cd $HOME/$CHAIN_REPO
git pull
git checkout $NEW_VERSION
make build
cp build/ununifid $DAEMON_HOME/cosmovisor/upgrades/$UPGRADE_NAME/bin
```

If you are setting true for automatic download in cosmosvisor, you don't need to do this. But, it's not recommended for validators.
