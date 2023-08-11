# Build a Validator Node

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

## Send a transaction to register as a validator candidate

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
> `ununifid tx staking create-validator --help`

## Backup critical files

There are certain files that you need to backup to be able to restore your validator if, for some reason, it damaged or lost in some way. Please make a secure backup of the following files located in `~/.ununifi/config/`:

- `priv_validator_key.json`
- `node_key.json`

It is recommended that you encrypt the backup of these files.

## Additional incentives for validators

The core team will delegate GUU to validators who serve following services:

- IBC relayer
  - `100000000uguu` delegation per channel
- Node snapshot
  - `10000000000uguu` delegation
- REST API endpoints
  - `10000000000uguu` delegation
