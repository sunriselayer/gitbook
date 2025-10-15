# Validator Node

Validator nodes allow you to participate in consensus in the Sunrise network.

## Hardware requirements

The following hardware minimum requirements are recommended for running the validator node:

- Memory: 8 GB RAM (minimum)
- CPU: 6 cores
- Disk: 500 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

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
CHAIN_ID=sunrise-1 # For mainnet
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

Check [our Github](https://github.com/sunriselayer/network) to know the current chain-id.

### Create a new key

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### Validator Public Key

The last thing needed before initializing the validator is to obtain your validator public key which was created when you first initialized your node. To obtain your validator pubkey:

```bash
sunrised tendermint show-validator
{"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZQweivhEkT/akg5RT6RWkElt43rr5cf+qu/QQ5jOpmQ="}
```

### Create Validator

A minimum of 1 vRISE is required to create a validator. vRISE is non-transferable, so if you have no balance in your account, please create a position in the Liquidity Pool to earn vRISE.

First, create validator config file [~/.sunrise/config/validator.json].

```json
{
  "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZQweivhEkT/akg5RT6RWkElt43rr5cf+qu/QQ5jOpmQ="},
  "amount": "1000000uvrise",
  "moniker": "your_validator's_name",
  "identity": "optional identity signature (ex. UPort or Keybase)",
  "website": "validator's (optional) website",
  "security": "validator's (optional) security contact email",
  "details": "validator's (optional) details",
  "commission-rate": "0.1",
  "commission-max-rate": "0.2",
  "commission-max-change-rate": "0.01",
  "min-self-delegation": "1"
}
```

Next, run the following command

```bash
sunrised tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

## Backup

There are certain files that you need to backup to be able to restore your validator if, for some reason, it is damaged or lost in some way. Please make a secure backup of the following files located in `~/.sunrise/config/`:

- `priv_validator_key.json`
- `node_key.json`

It is recommended that you encrypt the backup of these files.

## Additional incentives for validators

{% hint style="warning" %}
The application period for "Additional incentives for validators" closed on October 15th, 2025. The reopening date is undecided. For those who have already registered in the chain-registry and meet the requirements, the delegation has been completed.

Due to the depletion of the funding pool for the program, fulfilling the requirements now (e.g., enabling the tx indexer) will not make you eligible for additional delegation. Please be aware of this.
{% endhint %}

The core team will delegate more RISE to validators who serve the following services:

### RPC/API/gRPC

- **Delegation Amount:** 250,000 RISE for each service (RPC, API, gRPC), up to a maximum of 750,000 RISE.
- **Conditions:**
  - Your endpoint must be submitted via a pull request to [chain-registry](https://github.com/cosmos/chain-registry/blob/master/sunrise/chain.json) and get merged.
  - Transaction indexer and CORS must be enabled.

### Explorer

- **Delegation Amount:** 25,000 RISE.
- **Conditions:**
  - Your explorer must be submitted via a pull request to [chain-registry](https://github.com/cosmos/chain-registry/blob/master/sunrise/chain.json) and get merged.
- **Additional Delegation:**
  - We offer additional delegation if your explorer is used within the official Sunrise services. We will contact you individually.

Please note that the content of these incentives may change depending on the number of participants.
