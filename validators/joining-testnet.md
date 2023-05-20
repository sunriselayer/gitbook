# Joining Testnet

## Chain upgrades

In order to streamline chain upgrades and minimise downtime, you may want to set up [cosmovisor](https://docs.cosmos.network/master/run-node/cosmovisor.html) to manage your node

Joining Testnet
=
General instructions to join the UnUniFi testnet

## Configuration of Shell Variables

For this guide, we will be using shell variables. This will enable the use of the client commands verbatim. It is important to remember that shell commands are only valid for the current shell session, and if the shell session is closed, the shell variables will need to be re-defined.

If you want variables to persist for multiple sessions, then set them explicitly in your shell `.bash_profile`, as you did for the Go environment variables.

To clear a variable binding, use `unset $VARIABLE_NAME`. Shell variables should be named with ALL CAPS.

### Choose the required testnet chain-id

The current UnUniFi Normal TestNetwork's `chain-id` is `ununifi-test-v1`. Set the `CHAIN_ID`:

```Bash
CHAIN_ID=ununifi-test-v1
```

### Set your moniker name

Choose your `<your-moniker>`, this can be any name of your choosing and will identify your validator in the explorer. Set the `MONIKER`:

```Bash
MONIKER=<your-moniker>
# Example
MONIKER="node 1"
```

### Set persistent peers

Persistent peers will be required to tell your node where to connect to other nodes and join the network. To retrieve the peers for the chosen `chain-id`:

```Bash
# Set the base repo URL for mainnet & retrieve peers
echo "export PEERS=\"65710949120e28f8af12f81b75efd2a509280f70@a.ununifi-test-v1.cauchye.net:26656,b20e3aad6b1bf7dc2d1635c388f578f335b13466@b.ununifi-test-v1.cauchye.net:26656,a8d5662130dd127dfcf82314e7a5b379a95d9daf@c.ununifi-test-v1.cauchye.net:26656,59361cdca33b1abbf85b46adb62bb680c6d59768@d.ununifi-test-v1.cauchye.net:26656\"" >> ~/.bash_profile
source .bash_profile
```

## Setting up the Node

These instructions will direct you on how to initialize your node, synchronize to the network and upgrade your node to a validator.
For the install of `ununifid`, the binary of the our chain, see the [ununifid Installation and Setup](validators/ununifid-installation-and-setup.md).
The current testnet version is `v1.0.0-beta.1`.

### Initialize the chain

```Bash
ununifid init "$MONIKER" --chain-id $CHAIN_ID
```

This will generate the following files in `~/.ununifi/config/`

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

### Download the genesis file

```Bash
rm ~/.ununifi/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-test-v1/genesis.json -o ~/.ununifi/config/genesis.json
```

This will replace the genesis file created using `ununifid init` command with the mainnet `genesis.json`.

### Set persistent peers

Using the peers variable we set earlier, we can set the persistent_peers in `~/.ununifi/config/config.toml`:

```Bash
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.ununifi/config/config.toml
```

### Set minimum gas prices

For RPC nodes and Validator nodes we recommend setting the following minimum-gas-prices. As we are a permissionless wasm chain, this setting will help protect against contract spam and potential wasm contract attack vectors.

In `$HOME/.ununifi/config/app.toml`, set minimum gas prices:

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uguu\"/" $HOME/.ununifi/config/app.toml
```

### Additional settings

If you necessary, Edit config files `~/.ununifi/config/app.toml`

- `pruning`
- Enable defines if the API server should be enabled. `enable = true`
- EnableUnsafeCORS defines if CORS should be enabled (unsafe - use it at your own risk). `enabled-unsafe-cors = true`

### Create (or restore) a local key pair

Either create a new key pair, or restore an existing wallet for your validator:

```Bash
# Create new keypair
ununifid keys add <your-key>
# Restore existing ununifi wallet with mnemonic seed phrase.
# You will be prompted to enter mnemonic seed.
ununifid keys add <your-key> --recover
# Query the keystore for your public address
ununifid keys show <your-key> -a
```

Replace `<your-key>` with a key name of your choosing.

### Get some UnUniFi tokens

You will require some UnUniFi tokens to bond to your validator or pay the tx fee.

### Setup cosmovisor and start the node

Follow instructions to setup cosmovisor and start the node.
> Using cosmovisor is completely optional. If you choose not to use cosmovisor, you will need to be sure to attend network upgrades to ensure your validator does not have downtime and get jailed.

If you are not using Cosmovisor you can start node: `ununifid start`

### Syncing the node

After starting the `ununifid` daemon, the chain will begin to sync to the network. The time to sync to the network will vary depending on your setup and the current size of the blockchain, but could take a very long time. To query the status of your node:

```Bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

If this command returns `true` then your node is still catching up. If it returns `false` then your node has caught up to the network current block and you are safe to proceed to upgrade to a validator node.
