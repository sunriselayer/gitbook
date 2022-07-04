Validating on Mainnet
=
Validators are responsible for committing new blocks in the blockchain. These validators participate in the consensus protocol by broadcasting votes which contain cryptographic signatures signed by each validator's private key.

Validators and their delegators earn GUU as block provisions and tokens as transaction fees through execution of the Tendermint consensus protocol. Note that validators can set a commission percentage on the fees their delegators receive as additional incentive.

Preparing your validator for mainnet involves a few extra considerations. They are detailed below, but a sensible checklist is:
- How will you handle chain upgrades?
  - consider: Cosmovisor
- How will you know your node is up?
  - consider: Monitoring and alerts
- How will you mitigate DDOS attacks?
  - consider: Sentry Nodes
- How much storage will you need?
## Chain upgrades
In order to streamline chain upgrades and minimise downtime, you may want to set up [cosmovisor](https://docs.cosmos.network/master/run-node/cosmovisor.html) to manage your node
## Backups
If you are using a recent version of Cosmovisor, then the default configuration is that a state backup will be created before upgrades are applied. This can be turned off using [environment flags](https://docs.cosmos.network/master/run-node/cosmovisor.html#command-line-arguments-and-environment-variables).
## Alerting and monitoring
Alerting and monitoring is desirable as well - you are encouraged to explore solutions and find one that works for your setup. Prometheus is available out-of-the box, and there are a variety of open-source tools. Recommended reading:
##### Alerting:
- Tenderduty: https://github.com/blockpane/tenderduty
- PANIC: https://github.com/SimplyVC/panic_cosmos
##### Monitoring:
- https://medium.com/solar-labs-team/cosmos-how-to-monitoring-your-validator-892a46298722
- https://medium.com/simply-vc/cosmos-monitoring-and-alerting-for-validators-8e3f016c9567
- https://chainflow.io/cosmos-validator-mission-control/
- https://medium.com/cypher-core/cosmos-how-to-set-up-your-own-network-monitoring-dashboard-fe49c63a8271
## Avoiding DDOS attacks
> If you are comfortable with server ops, you might want to build out a [Sentry Node Architecture](https://docs.tendermint.com/master/nodes/validators.html) validator to protect against DDOS attacks.

The current best practice for running mainnet nodes is a Sentry Node Architecture. There are various approaches, as detailed [here](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea). Some validators advocate co-locating all three nodes in virtual partitions on a single box, using Docker or other virtualisation tools. However, if in doubt, just run each node on a different server.

Bear in mind that Sentries can have pruning turned on, as outlined [here](https://hub.cosmos.network/main/hub-tutorials/join-mainnet.html#pruning-of-state). It is desirable, but not essential, to have pruning disabled on the validator node itself.
## Managing storage
> If you are using a cloud services provider, you may want to mount `$HOME` on an externally mountable storage volume, as you may need to shuffle the data onto a larger storage device later. You can specify the home directory in most commands, or just use symlinks.

Disk space is likely to fill up, so having a plan for managing storage is key.

If you are running sentry nodes:
- 1TB storage for the full node will give you a lot of runway
- 200GB each for the sentries with pruning should be sufficient

Managing backups is outside the scope of this documentation, but several validators keep public snapshots and backups.

It is anticipated that state-sync will soon work for wasm chains, although it does not currettly.

Joining Mainnet
=
General instructions to join the UnUniFi mainnet after network genesis.

## Configuration of Shell Variables
For this guide, we will be using shell variables. This will enable the use of the client commands verbatim. It is important to remember that shell commands are only valid for the current shell session, and if the shell session is closed, the shell variables will need to be re-defined.

If you want variables to persist for multiple sessions, then set them explicitly in your shell `.bash_profile`, as you did for the Go environment variables.

To clear a variable binding, use `unset $VARIABLE_NAME`. Shell variables should be named with ALL CAPS.

### Choose the required mainnet chain-id
The current UnUniFi Network `chain-id` is `ununifi-beta-v1`. Set the `CHAIN_ID`:
```Bash
CHAIN_ID=ununifi-beta-v1
```
### Set your moniker name
Choose your `<your-moniker>`, this can be any name of your choosing and will identify your validator in the explorer. Set the `MONIKER`:
```Bash
MONIKER=<your-moniker>
# Example
MONIKER="Validator 1"
```
### Set persistent peers
Persistent peers will be required to tell your node where to connect to other nodes and join the network. To retrieve the peers for the chosen `chain-id`:
```Bash
# Set the base repo URL for mainnet & retrieve peers
CHAIN_REPO=https://github.com/UnUniFi/chain && \
PEERS="fa38d2a851de43d34d9602956cd907eb3942ae89@a.ununifi.cauchye.net:26656,404ea79bd31b1734caacced7a057d78ae5b60348@b.ununifi.cauchye.net:26656,1357ac5cd92b215b05253b25d78cf485dd899d55@[2600:1f1c:534:8f02:7bf:6b31:3702:2265]:26656,25006d6b85daeac2234bcb94dafaa73861b43ee3@[2600:1f1c:534:8f02:a407:b1c6:e8f5:94b]:26656,caf792ed396dd7e737574a030ae8eabe19ecdf5c@[2600:1f1c:534:8f02:b0a4:dbf6:e50b:d64e]:26656,796c62bb2af411c140cf24ddc409dff76d9d61cf@[2600:1f1c:534:8f02:ca0e:14e9:8e60:989e]:26656,cea8d05b6e01188cf6481c55b7d1bc2f31de0eed@[2600:1f1c:534:8f02:ba43:1f69:e23a:df6b]:26656"
```
## Setting up the Node
These instructions will direct you on how to initialize your node, synchronize to the network and upgrade your node to a validator.
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
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json -o ~/.ununifi/config/genesis.json
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
You will require some UnUniFi tokens to bond to your validator. To be in the active set you will need to have enough tokens.
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
### Upgrade to a validator
> Do not attempt to upgrade your node to a validator until the node is fully in sync as per the previous step.

To upgrade the node to a validator, you will need to submit a create-validator transaction:
```Bash
ununifid tx staking create-validator \
  --amount 1000000uguu \
  --commission-max-change-rate "0.1" \
  --commission-max-rate "0.20" \
  --commission-rate "0.1" \
  --min-self-delegation "1" \
  --details "validators write bios too" \
  --pubkey=$(ununifid tendermint show-validator) \
  --moniker "$MONIKER" \
  --chain-id $CHAIN_ID \
  --gas-prices 0.025uguu \
  --from <your-key>
```
> The above transaction is just an example. There are many more flags that can be set to customise your validator, such as your validator website, or keybase.io id, etc. To see a full list:
`ununifid tx staking create-validator --help`
### Backup critical files
There are certain files that you need to backup to be able to restore your validator if, for some reason, it damaged or lost in some way. Please make a secure backup of the following files located in `~/.ununifi/config/`:
- `priv_validator_key.json`
- `node_key.json`

It is recommended that you encrypt the backup of these files.
