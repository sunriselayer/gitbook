# Validator Node (Genesis)

Validator nodes allow you to participate in consensus in the Sunrise network.

{% hint style="info" %}
You can only join as a validator in this way before the network starts(genesis). If the network has already started, please see [this tutorial](validator-node.md).
{% endhint %}

## Hardware requirements

The following hardware minimum requirements are recommended for running the validator node:

* Memory: 8 GB RAM (minimum)
* CPU: 6 cores
* Disk: 500 GB SSD Storage
* Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Run the Node

First, follow the instructions on [setting up a full consensus node](full-consensus-node.md).

### Optional: Reset working directory

If you have already initialized a working directory for sunrised in the past, you must clean up before reinitialized a new directory. You can do so by running the following command:

```bash
sunrised tendermint unsafe-reset-all
```

### Initialize a working directory

Run the following command:

```bash
CHAIN_ID=sunrise-test-0.2
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

### Create a new key

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### Create the genesis transaction for new chain

```bash
STAKING_AMOUNT=1000000urise
sunrised genesis gentx $VALIDATOR_WALLET $STAKING_AMOUNT --chain-id $CHAIN_ID \
   --pubkey=$(sunrised tendermint show-validator) \
   --moniker=$MONIKER \
   --commission-rate=0.1 \
   --commission-max-rate=0.2 \
   --commission-max-change-rate=0.01 \
   --min-self-delegation=1 \
   --keyring-backend test
```

You will find the generated gentx JSON file inside `$HOME/.sunrised/config/gentx/gentx-*.json`

### Create Pull Request to register your gentx

To register your gentx, run the commands as follows and create a pull-request on GitHub.

```bash
 mv $HOME/.sunrised/config/gentx/gentx-*.json $HOME/.sunrised/config/gentx/gentx-${MONIKER}.json 
 git clone https://github.com/sunriselayer/public-testnet/
 cd public-testnet
 git checkout -b gentx/$MONIKER
 cp $HOME/.sunrised/config/gentx/gentx-${MONIKER}.json gentx/sunrise-testnet-1
 git add gentx/sunrise-testnet-1
 git commit -m "Add gentx: $MONIKER"
 git push origin $(git branch --show-current)
```
