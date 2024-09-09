# Gluon Full Node

Full nodes are general instructions to join the Gluon mainnet after network genesis.

## Chain upgrades

For streamline chain upgrades and minimize downtime, you may want to set up [Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor) to manage your node.

Follow [the Cosmovisor tutorial](../../node/types/consensus/setup-cosmovisor.md)

To automate on-chain upgrades, set the following options.

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## Backups

If you are using a recent version of Cosmovisor, then the default configuration is that a state backup will be created before upgrades are applied. This can be turned off using [environment flags](https://docs.cosmos.network/main/build/tooling/cosmovisor#command-line-arguments-and-environment-variables).

## Alerting and monitoring

Alerting and monitoring are desirable as well - you are encouraged to explore solutions and find one that works for your setup. Prometheus is available out-of-the-box, and there are a variety of open-source tools.

## Hardware requirements

The following hardware minimum requirements are recommended for running the validator node:

- Memory: 32 GB RAM (or equivalent swap file set up)
- CPU: 8 cores (4 physical core) x86_64
- Disk: 1 TB SSD Storage (See below for details)
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

An archival node (pruning = "nothing") should have at least 64GB of dedicated memory

- An archival node (pruning = "nothing") grows at a rate of ~100 GB per month Current total disk usage is 6TB, so a larger disk would be necessary.
- A full pruning node (pruning = "everything") grows at a rate of ~5 GB per month
- A default pruning node (pruning = "default") grows at a rate of ~25 GB per month

## Dependencies

The tutorial is done on Ubuntu 22.04 (LTS).
Follow [the environment tutorial](../../node/resources/enviromant.md)

## Run the node

### Install

```bash
git clone https://github.com/UnUniFi/chain.git
cd chain
git checkout $TAG
make install
```

### Initialize

Set `chain-id` & `moniker`. `moniker` is just a name for your node.

```bash
CHAIN_ID=gluon-1
MONIKER="node-name"
gluond init "$MONIKER" --chain-id $CHAIN_ID
```

This will generate the following files in `~/.gluon/config/`

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## Download the genesis file

For mainnet:

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json -o ~/.gluon/config/genesis.json
```

For testnet:

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-test-v1/genesis.json -o ~/.gluon/config/genesis.json
```

## Option: Set persistent peers

Persistent peers will be required to tell your node where to connect to other nodes and join the network. To retrieve the peers for the chosen `chain-id`:

```Bash
# Set the base repo URL for mainnet & retrieve peers
echo "export PEERS=\"fa38d2a851de43d34d9602956cd907eb3942ae89@a.ununifi.cauchye.net:26656,404ea79bd31b1734caacced7a057d78ae5b60348@b.ununifi.cauchye.net:26656,1357ac5cd92b215b05253b25d78cf485dd899d55@[2600:1f1c:534:8f02:7bf:6b31:3702:2265]:26656,25006d6b85daeac2234bcb94dafaa73861b43ee3@[2600:1f1c:534:8f02:a407:b1c6:e8f5:94b]:26656,caf792ed396dd7e737574a030ae8eabe19ecdf5c@[2600:1f1c:534:8f02:b0a4:dbf6:e50b:d64e]:26656,796c62bb2af411c140cf24ddc409dff76d9d61cf@[2600:1f1c:534:8f02:ca0e:14e9:8e60:989e]:26656,cea8d05b6e01188cf6481c55b7d1bc2f31de0eed@[2600:1f1c:534:8f02:ba43:1f69:e23a:df6b]:26656\"" >> ~/.bash_profile
source .bash_profile
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.gluon/config/config.toml
```

### Set minimum gas prices

For RPC nodes and Validator nodes, we recommend setting the following minimum-gas-prices. As we are a permissionless wasm chain, this setting will help protect against contract spam and potential wasm contract attack vectors.

In `$HOME/.gluon/config/app.toml`, set minimum gas prices:

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uglu\"/" $HOME/.gluon/config/app.toml
```

### Option: Additional settings

If necessary, Edit config files `~/.gluon/config/app.toml`

- Enable defines if the API server should be enabled.

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' ~/.gluon/config/app.toml;
```

- EnableUnsafeCORS defines if CORS should be enabled (unsafe - use it at your own risk).

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' ~/.gluon/config/app.toml;
```

#### Accessing historical state

If you want to query the historical state — for example, you might want to know the balance of a wallet at a given height in the past — you should run an archive node with `pruning = "nothing"` in `app.toml`. Note that this configuration is resource-intensive and will require significant storage:

```toml
pruning = "nothing"
```

If you want to save on storage requirements, consider using `pruning = "everything"` in app.toml to prune everything.

```toml
pruning = "everything"
```

### Create (or restore) a local key pair

Either create a new key pair or restore an existing wallet for your validator:

```Bash
# Create new keypair
gluond keys add <your-key>
# Restore existing gluon wallet with mnemonic seed phrase.
# You will be prompted to enter mnemonic seed.
gluond keys add <your-key> --recover
# Query the keystore for your public address
gluond keys show <your-key> -a
```

### Get some GLU tokens

You will require some GLU tokens to bond to your validator. To be in the active set you will need to have enough tokens.

### Start the consensus node

Follow the instructions to set up Cosmovisor and start the node.

{% hint style='tip' %}
Using cosmovisor is completely optional. If you choose not to use cosmovisor, you will need to be sure to attend network upgrades to ensure your validator does not have downtime and get jailed.
{% endhint %}

If you are not using Cosmovisor, run the following:

```bash
gluond start
```

### Syncing the node

After starting the `gluond` daemon, the chain will begin to sync to the network. The time to sync to the network will vary depending on your setup and the current size of the blockchain but could take a very long time. To query the status of your node:

```Bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

This command returning `true` means that your node is still catching up. Otherwise, your node has caught up to the network's current block and you are safe to proceed to upgrade to a validator node.

If you want to shorten the time to catch up to the latest block, consider using snapshots from other nodes.

- [NodeStake](https://nodestake.top/ununifi)
- [NodeJumper](https://app.nodejumper.io/ununifi/sync)
- [Nodeist](https://nodeist.net/Ununifi/)
- [genznodes](https://genznodes.dev/services/)

If you want to catch up from 0 height, you have to upgrade `gluond` at each upgrade heights.
