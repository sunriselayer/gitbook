# Full Consensus Node

Full consensus nodes allow you to sync blockchain history in the Sunrise consensus layer.

## Chain upgrades

For streamline chain upgrades and minimize downtime, you may want to set up [Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor) to manage your node.

Follow [Cosmovisor tutorial](setup-cosmovisor.md)

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

- Memory: 8 GB RAM (minimum)
- CPU: 4 cores
- Disk: 250 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

If you are not using pruning, you are running an archive node, and it is recommended to have 500 GB of SSD storage.

## Dependencies

The tutorial is done on Ubuntu 22.04 (LTS). Follow [the environment tutorial](../../resources/environment.md)

## Run the full consensus node

### Install

[Install Go](https://go.dev/doc/install) 1.24.2

```bash
git clone https://github.com/sunriselayer/sunrise.git
cd sunrise
git checkout $TAG
make install
```

{% hint style="info" %}
When synchronizing from the genesis, use the binary version as of the genesis.
If you are using snapshots, you must check the height of the snapshot and use the binary at that height.

See [upgrade doc](../../resources/upgrade.md) for more details.
{% endhint %}

### Initialize

Set `chain-id` & `moniker`. `moniker` is just a name for your node.

```bash
CHAIN_ID=sunrise-1 // mainnet
MONIKER="node-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

This will generate the following files in `~/.sunrise/config/`

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## Download the genesis file

Check the `genesis.json` of the currently running network on [our Github](https://github.com/sunriselayer/network)

Example: For mainnet:

```bash
rm ~/.sunrise/config/genesis.json
curl -L https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/genesis.json -o ~/.sunrise/config/genesis.json
```

### Set minimum gas prices

For RPC nodes and Validator nodes, we recommend setting the following minimum-gas-prices. As we are a permissionless wasm chain, this setting will help protect against contract spam and potential wasm contract attack vectors.

In `$HOME/.sunrise/config/app.toml`, set minimum gas prices:

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025urise\"/" $HOME/.sunrise/config/app.toml
```

{% hint style="warning" %}
Do NOT set too high gas prices. If you are a validator, your proposed block will not include transactions. This reduces the number of transactions the entire network can process.
{% endhint %}

### Option: Set seeds & persistent peers

- Seeds

"Seeds" provides a list of other validators that a newly joining validator should initially connect to.
Once a validator connects to the network, it primarily relies on `persistent_peers` for connections, reducing the importance of `seeds`.

```bash
SEEDS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/seeds.txt | tr '\n' ',')
echo $SEEDS
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/" $HOME/.sunrise/config/config.toml
```

- Persistent Peers

"Persistent Peers" is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```bash
PERSISTENT_PEERS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/peers.txt | tr '\n' ',')
echo $PERSISTENT_PEERS
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PERSISTENT_PEERS\"/" $HOME/.sunrise/config/config.toml
```

### Option: Additional settings

If necessary, Edit config files `$HOME/.sunrise/config/app.toml`

- Enable defines if the API server should be enabled.

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' $HOME/.sunrise/config/app.toml;
```

- EnableUnsafeCORS defines if CORS should be enabled (unsafe - use it at your own risk).

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' $HOME/.sunrise/config/app.toml;
```

- By default, RPC and REST are not public, so if you want to make it a public node, configure as follows

```bash
sed -i 's/address = "localhost:9090"/address = "0.0.0.0:9090"/' $HOME/.sunrise/config/app.toml;
sed -i 's#address = "tcp://localhost:1317"#address = "tcp://0.0.0.0:1317"#' $HOME/.sunrise/config/app.toml;
sed -i 's#laddr = "tcp://127.0.0.1:26657"#laddr = "tcp://0.0.0.0:26657"#' $HOME/.sunrise/config/config.toml;
```

### Storage and pruning configurations

If your consensus node is being connected to a sunrise-node bridge node, you will need to enable transaction indexing and retain all block data. This can be achieved with the following settings in `config.toml`.

#### Enable transaction indexing

```toml
indexer = "kv"
```

#### Retain all block data

And in `app.toml`, `min-retain-blocks` should remain as the default setting:

```toml
min-retain-blocks = 0
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
sunrised keys add <your-key>
# Restore existing sunrise wallet with mnemonic seed phrase.
# You will be prompted to enter mnemonic seed.
sunrised keys add <your-key> --recover
# Query the keystore for your public address
sunrised keys show <your-key> -a
```

Replace `<your-key>` with a key name of your choosing.

### Get some RISE tokens

You will require some vRISE tokens to bond to your validator (and some RISE tokens for fees). To be in the active set you will need to have enough tokens.

### Start the consensus node

Follow the instructions to set up Cosmovisor and start the node.
See [Cosmovisor tutorial](setup-cosmovisor.md)

{% hint style="info" %}
Using cosmovisor is completely optional. If you choose not to use cosmovisor, you will need to be sure to attend network upgrades to ensure your validator does not have downtime and get jailed.
{% endhint %}

If you are not using Cosmovisor, run the following:

```bash
sunrised start
```

### Syncing the node

After starting the `sunrised` daemon, the chain will begin to sync to the network. The time to sync to the network will vary depending on your setup and the current size of the blockchain but could take a very long time. To query the status of your node:

```Bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

This command returning `true` means that your node is still catching up. Otherwise, your node has caught up to the network's current block and you are safe to proceed to upgrade to a validator node.

If you want to shorten the time to catch up to the latest block, consider using snapshots from other nodes.

### Option: Use a snapshot

If you want to shorten the time to catch up to the latest block, consider using snapshots. Snapshots allow a node to be bootstrapped from a specific height, reducing the need to sync from genesis.

Our partner at [Polkachu](https://www.polkachu.com/tendermint_snapshots/sunrise) provides daily snapshots for the Sunrise network. Please visit their website to get the latest snapshot URL.
